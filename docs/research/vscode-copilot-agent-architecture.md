# Reverse-Engineering Mature Coding Agents

**VS Code / GitHub Copilot, Claude Code, and Codex — verified mechanisms, context strategy, and a design for the CS Visually ADE**

Research date: 2026-11-04  
Scope: local installed software and the user's own local session logs. No application code, infrastructure, or secrets were modified.

---

## Evidence legend

| Label | Meaning |
|---|---|
| **[S] Source-verified** | Read directly from an installed bundle, binary string, or shipped source artifact on this machine. Minified names can change between versions; version pins are given. |
| **[L] Local-log-verified** | Measured from the user's own session transcripts/event logs on this machine. Describes observed behavior, not a universal contract. |
| **[D] Documented** | Publicly documented behavior. Included only where it matches or explains what the artifacts show; documentation URLs are entry points, not proof of internal implementation. |
| **[I] Inference** | A design conclusion or recommendation drawn from the evidence. Not a claim about the vendor's internals. |
| **[U] Unknown / opaque** | Not established by the inspected artifacts. Includes model-side routing, hidden system prompts, hosted indexing/ranking, and proprietary service behavior. |

**What this report can and cannot claim.** The installed client code shows what the client sends, how it builds prompts, how it truncates and persists data, and how it decides to continue or stop. The session logs show what actually happened. Neither reveals the provider's private orchestration, model weights, prompt-cache internals, or account-level policy services.

---

## 0. What was inspected

| Product | What was read | Version observed | What it gives us |
|---|---|---|---|
| VS Code + Copilot Chat | `/Applications/Visual Studio Code.app/Contents/Resources/app/extensions/copilot/dist/extension.js` (≈19.7 MB minified), `package.json` | VS Code **1.144.1**, Copilot extension **0.72.0** | The actual tool-calling loop, prompt budget allocator, compaction thresholds, summarizer prompt, tool schemas, truncation behavior |
| Copilot agent session | `~/.copilot/session-state/<session-id>/events.jsonl`, `session.db`, `checkpoints/`, `workspace.yaml` | Copilot SDK/agent host, model `gpt-6-luna` | Real turn counts, tool mix, token usage, prompt-cache state, final summaries |
| Claude Code CLI | Native binary `~/.local/share/claude/versions/2.1.272` (≈201 MB, string-extracted) | **2.1.272** | System-prompt fragments, tool contracts, auto-compact semantics, overflow-to-file behavior, compaction prompt |
| Claude Code VS Code extension | `~/.vscode/extensions/anthropic.claude-code-2.1.318-darwin-arm64/extension.js` | **2.1.318** | Client-side integration behavior |
| Claude Code sessions | 34 `~/.claude/projects/*/*.jsonl` transcripts, 115 compaction boundaries | 2.1.197 – 2.1.275 | Compaction measurements, tool-result sizes, prompt-cache usage, subagent usage |
| Codex Desktop | 48 `~/.codex/sessions/**/rollout-*.jsonl` logs, 593 compaction events, `config.toml` | CLI **0.165.0-alpha.1.2**, model `gpt-6.1-sol` | Full base instructions, tool definitions, encrypted compaction payload, token usage, subagent protocol |
| CS Visually repo | `~/Desktop/dsa-visualizer` at `701b974` | React 18 + Vite + Monaco, FastAPI, PostgreSQL, Redis, Judge0 | Platform shell for the ADE comparison |

**Important scope limit for CS Visually.** The inspected repository contains the coding-challenge platform (React/Vite/Monaco frontend, FastAPI modular monolith, PostgreSQL, Redis, Judge0 execution). It does **not** contain the agent runtime described in the task (DeepSeek/Ollama tool-calling agents, Docker workspaces, hidden-test evaluator). Therefore Section 8 is a design comparison against the stated ADE stack, not a code audit of that runtime. Recommendations are written to be dropped into the existing FastAPI service.

---

## 1. Executive summary: the ten mechanisms that actually matter

1. **The transcript is not the prompt.** All three agents persist far more than they send. Each model call is a selected projection: stable system/tool prefix, immutable user goal, compact run state, recent turns, selected evidence, and a reserved output budget.
2. **Compaction is a first-class runtime feature, not a fallback.** Copilot triggers background summarization at **78–82%** of the model window, with an **emergency at 90%** and applies a completed summary only above **65%**. Claude compacts at roughly the top of a 1M window; observed medians were **967,748 → 24,168 tokens (97.5% reduction)**. Codex replaces history with an **encrypted compaction item** plus a curated prefix.
3. **Tool results are the dominant context cost, so they are bounded at the tool boundary.** Copilot computes a token cap of **0.5 × modelMaxPromptTokens**, middle-truncates **40% head / 60% tail**, and spills large results to disk with a `read_file` handle. Copilot's `read_file` caps at **2,000 lines**. Claude spills over-budget output to a file and tells the model to page it with `offset/limit`. Codex's orchestration tool caps direct output at **10,000 tokens** by default.
4. **Prompt caching is part of the architecture.** Copilot keeps a stable prefix, inserts cache breakpoints, and reported **98 tool schemas costing 10,537 tokens** with cache TTLs of **300 s** (Claude Haiku route) and **1,800 s** (GPT-6 Luna route). In the observed run, **212,445 of 213,030 input tokens** were cache reads. Claude's per-call usage was often **2 uncached tokens + ~488K cache reads**.
5. **Tool schemas are a budgeted resource.** Copilot does not merely append every tool; it allocates prompt space across prioritized elements with `flexGrow`, `flexBasis`, `flexReserve`, and per-element `tokenLimit`, raising `BudgetExceededError` when the projection cannot fit.
6. **The loop has explicit, finite budgets and a completion protocol.** Copilot's default request cap is **200** (`chat.agent.maxRequests`). Autopilot can extend the limit by **1.5× up to 200** and uses a **`task_complete`** tool; it also treats a non-empty text-only response as done. Retries are capped at **3** and exclude rate-limit/quota/cancel/refusal classes.
7. **Multi-agent work is isolated and review-oriented.** Claude launched **implement/review pairs** as background subagents with named tasks and a model override. Codex exposes `spawn_agent`, `followup_task`, `send_message`, `wait_agent`, and a mailbox protocol.
8. **Authorization is layered, not a single "allow" flag.** Capability registry, per-run allowlist, argument policy, approval, and execution sandbox are distinct. Claude has permission modes and denial recovery ("do not re-attempt the exact same call"). Codex records `approval_policy` and `sandbox_policy` per turn.
9. **Termination is a controller decision, not a test result.** A passing test suite is evidence, not completion. The controller must persist a terminal state, a validation record, and a final answer — or emit a deterministic fallback when the model cannot.
10. **Persistence is split into planes.** Editor/workspace state, session transcript, tool/job state, artifacts, prompt projection, and long-term instructions are separate stores. Restoring a chat does not restore a dead process or the exact byte-for-byte model context.

---

## 2. Architecture and process boundaries

### 2.1 Three planes

The artifacts support a three-plane model:

```
┌───────────────────────────────────────────────────────────────┐
│ Client plane        chat UI, Monaco, approvals, diff review   │
├───────────────────────────────────────────────────────────────┤
│ Harness plane       prompt assembly, model calls, tool loop,  │
│                     permissions, budgets, compaction, state   │
├───────────────────────────────────────────────────────────────┤
│ Execution plane     filesystem, terminal, tests, containers,  │
│                     external MCP/connectors                   │
└───────────────────────────────────────────────────────────────┘
                 ▲                                   │
                 │        tool results, artifacts ◄──┘
                 └──────── model text/tool calls ─────┘
```

**[S] Copilot has two observable harness paths on this machine.**

- The **VS Code chat extension** exposes workspace-native tools such as `read_file`, `apply_patch`, `grep_search`, `file_search`, `list_dir`, `run_in_terminal`, `get_errors`, `get_changed_files`, `semantic_search`, `create_file`, and `manage_todo_list`.
- The **Copilot SDK/agent host** session used a different surface: `view`, `apply_patch`, `create`, `rg`, `bash`, `glob`, `skill`, `web_search`, `web_fetch`, `tool_search_tool`, `ask_user`, and `set_workspace`.

The lesson for an ADE is not "copy the tool names." It is that **the harness owns the tool contract**, and the same model can be run with different tool surfaces for different products. Tool definitions, permission policy, and output handling must live in one versioned registry.

**[S] Claude Code** is a single CLI harness with permission modes, hooks, background tasks, subagents, and an SDK-facing tool schema (`sdk-tools.d.ts`). The explicit system text says: "The system will automatically compress prior messages in your conversation as it approaches context limits. This means your conversation with the user is not limited by the context window." It also states that tools run in a user-selected permission mode and that a denied call must not be retried unchanged.

**[S] Codex** wraps a large set of capabilities behind a JavaScript orchestration tool named `exec`:

- It runs in a fresh V8 isolate with no Node, filesystem, network, or console.
- Nested tools are available as `tools.<name>(...)`.
- It accepts raw JavaScript, not JSON.
- It defaults to **30,000 ms** yield and **10,000 output tokens**; `wait` resumes a cell with a default **10,000 ms** wait and **10,000 tokens**.
- Independent calls are encouraged via `Promise.allSettled`.

This is a meaningful alternative to one-tool-per-call: the model writes a small program that composes tools, and the runtime yields/waits on long operations instead of blocking the conversation.

### 2.2 What is public vs. proprietary

| Area | Status |
|---|---|
| Client tool loop, prompt composition, compaction thresholds, truncation, permission plumbing | **[S]** visible in installed bundles/binaries |
| Session persistence formats and token accounting | **[S]/[L]** visible |
| Provider routing, hidden system prompts, private ranking/indexing, hosted cache behavior, account policy | **[U]** not established |
| Exact production model behavior under every partial-stream condition | **[U]** no universal contract; provider adapters must be tested |

Do not put "Copilot does X internally" in a product design doc unless X is in the client artifact or a log. Use "the client harness does X; the provider's role is opaque."

---

## 3. The real agent loop

### 3.1 Copilot's `ToolCallingLoop` (source-verified)

The shipped extension contains a `ToolCallingLoop` class with an observable `_runLoop` / `runOne` structure. The essential control flow, reconstructed from the code, is:

```text
loop:
  if a previous round exists and roundCount >= toolCallLimit:
      if permissionLevel == "autopilot" and toolCallLimit < 200:
          toolCallLimit = min(round(toolCallLimit * 1.5), 200)
      else:
          show "Continue to iterate?" / mark maxToolCallsExceeded
          stop
  if cancelled or yieldRequested:
      stop
  round = runOne()
  append round to history
  if round has no tool calls or response is not successful:
      if cancelled: stop
      if retryable and retries < 3: retry
      else: stop
  else:
      execute tool calls; append results; continue
```

Verified constants and behaviors:

| Behavior | Value / detail | Evidence |
|---|---|---|
| Default maximum model requests | `chat.agent.maxRequests ?? 200` | **[S]** |
| Autopilot limit extension | `min(round(limit * 1.5), 200)` | **[S]** |
| Autopilot completion tool | `TASK_COMPLETE_TOOL_NAME = "task_complete"` | **[S]** |
| Autopilot retries | `MAX_AUTOPILOT_RETRIES = 3` | **[S]** |
| Autopilot iterations | `MAX_AUTOPILOT_ITERATIONS = 3` | **[S]** |
| Text-only completion | In autopilot, a round with **zero tool calls** and non-empty text is treated as done | **[S]** |
| Retry exclusions | `rateLimited`, `quotaExceeded`, `canceled`, `offTopic`, `refusal` are not auto-retried | **[S]** |
| Limit UI | Shows "Continue to iterate?" with a suggested next round limit of `round(limit * 1.5)` | **[S]** |
| Cancellation | Checked before/after prompt build and between rounds; `yieldRequested` is honored | **[S]** |
| Persistable state | Tool rounds, tool results, thinking, summaries, compaction metadata, hook context | **[S]** |

Two subtle but important details:

1. **The loop distinguishes "no tool calls" from "final answer."** In ordinary agent mode, a text-only response is a candidate final answer. In autopilot, it is explicitly treated as done unless the stop-hook logic says otherwise.
2. **`task_complete` is not universal.** It is added only for autopilot. A product should not require a model-generated completion tool as the only termination signal.

### 3.2 Claude Code's loop

**[S]** Claude Code's system text establishes:

- Tools execute under a user-selected permission mode.
- A denied tool call must not be retried unchanged; the model should diagnose the denial and change approach.
- Tool results may contain external data and possible prompt injection; the model is told to flag suspected injection.
- Prior messages are automatically compressed near context limits.

**[L]** The transcripts show the operational shape:

- A turn can contain many `tool_use` blocks, followed by `tool_result` entries.
- `Stop` hooks run at the end of a turn (`system` records with `subtype: "stop_hook_summary"`); hooks can block continuation, add context, or record output.
- Background subagents are launched with `run_in_background: true`, a `name`, a `description`, a `subagent_type`, and an optional `model` override.
- The observed workflow used **implement/review pairs**: separate `batchA-impl` and `batchA-review` agents, each with a written brief, and a later integration pass.

**[S]** Tool contracts are explicit about safe use: `Bash` is preferred only when a dedicated tool cannot do the job; `Read` requires an absolute path and reads up to a line cap; `Grep` is ripgrep-based; `Edit` requires an exact prior read; `Glob` returns files sorted by modification time; `WebFetch` upgrades HTTP to HTTPS, refuses dotless hosts, and does not follow cross-host redirects; `TodoWrite` replaces the full list and keeps one item `in_progress`.

### 3.3 Codex's loop

**[S]** Codex's base instructions define two channels: `commentary` for progress and `final` for the turn-ending answer. The final answer must be self-contained because commentary is collapsed. The loop is expected to continue across compactions as one logical chain.

**[L]** The observed rollout format contains:

- `session_meta` with the full `base_instructions.text` (≈21.8 KB in the sampled session).
- `turn_context` with `approval_policy`, `sandbox_policy`, `permission_profile`, model, and collaboration mode.
- `response_item` entries for `reasoning`, `function_call`, `custom_tool_call`, and their outputs.
- `event_msg` entries for `task_started`, `task_complete`, `turn_aborted`, and token updates.
- `token_usage_record` entries with per-call, per-turn, and per-thread accounting.

**[L]** `task_complete` is an event with `last_agent_message`, `started_at`, `completed_at`, `duration_ms`, and `time_to_first_token_ms`. `turn_aborted` carries a reason such as `interrupted`. This is a clean model for an ADE: make completion and interruption explicit events, not inferred UI states.

---

## 4. Context management — the part that decides whether the product works

### 4.1 The measured reality

| Metric | Copilot (observed) | Claude Code (observed) | Codex (observed) |
|---|---|---|---|
| Model window / cap | `maxPromptTokens = 272,000` | auto-compact window derived from model; 1M-class observed | ~245K–466K input at compaction |
| Input tokens per call | 30,363 – 213,030 | 2 uncached + up to ~488K cache reads | ~204K–245K typical |
| Cache reads | up to **212,445** | up to **488,623** | up to **244,224** |
| Tool schema cost | **98 tools / 10,537 tokens** | not directly measured; tool list is large | tool definitions embedded in `additional_tools` |
| Compaction | background + foreground | auto + manual | replacement history + encrypted summary |
| Observed compaction trigger | 78–82% warm, 90% emergency | near top of window | ~245K median |

**The single most important number:** in one observed Copilot call, **212,445 of 213,030 input tokens were cache reads**. The agent was not "re-sending 213K tokens of fresh tool history" every turn. It was re-sending a stable prefix that the provider could cache, plus a small delta. This is why a naive implementation that rebuilds a different prompt each turn feels 10× more expensive and slower than a mature agent.

### 4.2 Copilot's prompt budget allocator (source-verified)

Copilot does not concatenate strings until the window is full. It builds a **prioritized prompt tree**:

- Elements declare `priority`, `flexGrow`, `flexBasis`, `flexReserve`, and sometimes `tokenLimit`.
- The renderer computes `remainingTokenBudget`, reserves space for flexible children, and renders each child against a computed budget.
- If an element cannot fit, the renderer removes the lowest-priority child and re-counts. If it still cannot fit, it raises `BudgetExceededError`.
- The renderer records a **render epoch** with each element's token budget and reserved tokens. This is effectively a debuggable context ledger.
- `PrioritizedList` assigns descending priorities; `Expandable` elements can grow into remaining space.

Verified constants:

| Constant | Value | Meaning |
|---|---|---|
| `tro` | `0.5` | `maxToolResultLength = floor(modelMaxPromptTokens * 0.5)` |
| `F7e` | `{ warmJitterMin: 0.78, warmJitterSpan: 0.04, emergency: 0.9, applyMinRatio: 0.65 }` | Compaction policy |
| Background trigger | `ratio >= 0.78 + random()*0.04` | 78–82% of window |
| Emergency trigger | `ratio >= 0.90` | Hard pressure |
| Apply completed summary | `ratio >= 0.65` | Avoid applying a summary after a model switch or window override |

**[I]** The random jitter is a thundering-herd control: it prevents many sessions from compacting at exactly the same ratio. The `applyMinRatio` guard prevents a summary produced for a larger context window from being applied after the model switches to a smaller one.

### 4.3 Compaction prompts

**[S] Copilot** has two visible summarization paths:

- A **foreground/manual** path and a **background** path.
- The summarizer renders a special prompt with `triggerSummarize: true`, `forceSimpleSummary` in some paths, and `maxToolResultLength: Infinity` for manual compaction.
- The summary prompt says, in part:

  > "Your task is to create a comprehensive, detailed summary of the entire conversation that captures all essential information needed to seamlessly continue the work without any loss of context."

  It requires sections for chronology, intent mapping, technical inventory, code archaeology, progress, context validation, and **recent commands/tool results**. It explicitly asks for the last agent commands, key tool outcomes, immediate state, and the triggering context.
- The model must wrap the result in `<summary>...</summary>` and must **not call tools**.

**[S] Claude Code** has a similarly explicit compaction prompt, preserved in the binary. Its required sections include:

1. Primary Request and Intent
2. Key Technical Concepts
3. Files and Code Sections
4. Errors and fixes
5. Problem Solving
6. **All user messages** (not tool results), with security-relevant constraints preserved **verbatim**
7. Pending Tasks
8. Current Work
9. Optional Next Step

It also supports user-provided compaction instructions, and it distinguishes "recent messages only after the retained context" from a full summary. The system prompt tells the model: "The system will automatically compress prior messages... your conversation is not limited by the context window."

**[S] Codex** takes a different route. The `compacted` payload contains:

- `replacement_history` (a curated prefix)
- `replacement_history_metadata` (including a `compaction_model_hash`)
- `retained_context` (verified answers, user messages, assistant messages with revisions)
- `window_number`, `first_window_id`, `previous_window_id`, `window_id`
- `compaction_response_id`
- `latest_token_usage_record`
- `resume_metadata`
- a final `{"type": "compaction", "encrypted_content": "..."}` item

In the sampled logs, the **plaintext summary length was 0** and the compaction item was an encrypted blob (≈52 KB). The model sees a provider-managed compaction representation; the client stores the opaque item and a curated prefix. This is a strong hint that the summary can be provider-specific and is not guaranteed to be human-readable.

**[S] Codex base instructions** tell the model exactly how to behave across compaction:

> "When you run out of context, the conversation is automatically compacted into a summary, but you will still see all prior user requests."

> "Compaction does not end the task. Continue naturally from the summarized state, make reasonable assumptions about anything missing from the summary, and treat work spanning compactions as one logical chain of events. Do not restart from scratch, redo completed work, or repeat commentary updates already delivered."

**[I]** This is the behavioral contract an ADE must encode. Compaction is not just a token trick; it is a promise that the run continues and that the original goal survives.

### 4.4 Tool-output containment

Each product bounds tool output at a different layer:

**Copilot (VS Code harness) — [S]:**

- `read_file` schema: "This tool will truncate its output at 2000 lines and may be called repeatedly with offset and limit parameters to read larger files in chunks. Binary files use offset/limit as byte offsets."
- Large tool results: when a configurable threshold is exceeded (`LargeToolResultsToDiskEnabled` / `LargeToolResultsToDiskThreshold`), the harness writes the content to a session resource directory and returns a pointer: "Large tool result (NKB) written to file. Use the read_file tool to access the content at: `<path>`." If JSON, it also writes `schema.json`.
- Text truncation: it estimates chars/token from the tokenizer, reserves room for a marker, keeps **40% head** and **60% tail**, and inserts:

  > `[Tool response was too long and was truncated.]`

- It uses the same mechanism for images, with a shared image budget and a placeholder when exceeded.

**Copilot (observed CLI session) — [L]:**

- Tool completion payloads in the event log were capped near **19.4 KB**; the median was **≈5.5 KB**. The `create` tool telemetry recorded `truncateBasedOn: "tokenCount"` and `truncateStyle: "middle"`.
- Treat the exact cap as harness-specific, not a universal number.

**Claude Code — [S]:**

- Over-budget tool output is persisted to a file with a message of the form: "characters across ... exceeds maximum allowed tokens. Output has been saved to ...".
- The model is instructed to use `offset` and `limit`, `grep`, `jq`, or character spans to read the file in pieces, and to read **all** of it before summarizing or analyzing.
- If the persisted file hits a byte limit, the model is told the saved file may be truncated and may fail a whole-file parse.

**Codex — [S]:**

- `exec` has a direct-result token budget: `max_output_tokens` default **10,000**.
- `wait` returns only new output since the last yield, with `max_tokens` default **10,000**.
- Long-running work yields with a `cell_id` instead of blocking.

**[I]** The reusable rule: **never let a tool result enter the prompt unbounded.** Persist the full result as an artifact; return a structured summary, exact matched ranges/counts, and a handle. The model can page the artifact when it needs more. This is the single biggest fix for a 100K-window runtime.

### 4.5 Prompt caching and prefix stability

**[S] Copilot** contains cache-breakpoint logic (`CacheBreakpoint` content parts, a maximum of four breakpoints, and a rule that avoids inserting breakpoints into certain tool/user shapes). Its usage checkpoints record:

- `modelCacheState`: model ID, expiry, TTL (**300 s** for `claude-haiku-4.5`, **1,800 s** for `gpt-6-luna`).
- `promptCacheBreakState`: model, vendor, model-call ID, request ID, endpoint, transport, `tool_count`, `tool_tokens` (**98 / 10,537**), and per-tool schema hashes.

**[L] Claude Code** usage records show the same pattern from the other side: `input_tokens: 2`, `cache_read_input_tokens: 486,218`, `cache_creation_input_tokens: 1,747`, `ephemeral_1h_input_tokens`. A stable prefix plus a small delta is the normal case.

**[I]** For CS Visually:

- Keep the prefix stable within a run: system policy, tool definitions (sorted, versioned), immutable user goal, and acceptance criteria.
- Append new turns; do not rewrite old ones.
- Put volatile content (fresh tool results, timestamps, random IDs) **after** the stable prefix.
- Use provider-native prompt caching where available (Anthropic `cache_control`, DeepSeek context caching, Ollama prefix reuse).
- Invalidate deliberately when the tool set or model changes. A schema hash is a good cache key.

### 4.6 Preventing repeated searches without progress

The mature agents do not rely on a single "read guard." They combine:

1. **Search tools with explicit scopes** (`grep_search` for exact text, `file_search` for names, `semantic_search` for concepts, `list_dir` for structure).
2. **Bounded reads** (`read_file` 2,000-line cap; offset/limit paging).
3. **Prompt guidance** to read large sections once rather than many micro-reads, to batch independent calls, and not to call `semantic_search` in parallel.
4. **A controller that can stop.** Copilot's tool-call limit, autopilot retry/iteration caps, and cancellation are the backstop.
5. **Subagents for isolated exploration** (Claude `Agent`, Codex `spawn_agent`, Copilot `search_subagent` / `explore_subagent`), so a broad search does not permanently pollute the parent context.

**[I]** The missing piece in most home-grown ADEs is (4) plus an **evidence ledger**. Add a run-scoped ledger:

```text
fingerprint = hash(tool_name, normalized_args, workspace_revision)
entry = {
  fingerprint,
  first_seen_at,
  result_artifact_id,
  result_digest,
  files_or_ranges_examined,
  conclusion
}
```

If the same fingerprint is requested again with the same workspace revision and the result digest is unchanged, return a short message:

> "This exact query already ran at turn N. Result handle: `artifact://...`. It found X, Y, Z. Choose a different hypothesis, narrow the path, or read one of those files."

After a second identical repeat, require a changed argument or a stop. After a third, stop with `blocked` and a final summary. This is deterministic and testable — unlike hoping the model "notices" it is looping.

### 4.7 The context assembly recipe

A concrete projection order that mirrors the verified behavior:

```text
1. Stable system policy + safety + identity
2. Tool schemas (only tools enabled for this run; sorted; versioned)
3. Immutable user goal + acceptance criteria + constraints
4. Run-state snapshot (phase, plan, completed, changed files, validations, open risks)
5. Carryover summary (if any), bounded
6. Recent turns (last N, or last K tokens)
7. Selected evidence (file ranges, search hits, artifact previews)
8. Current user message / steering delta
9. Reserved output + finalization budget
```

The reserve must be explicit. Copilot's `flexReserve` and `maxToolResultLength` are two forms of the same idea. Claude's compaction and Codex's windowing are the backstop when the projection still does not fit.

---

## 5. Tools, authorization, and workspace interaction

### 5.1 Tool surfaces

| Category | Copilot examples | Claude Code examples | Codex examples |
|---|---|---|---|
| Structure | `list_dir`, `file_search`, `read_project_structure` | `Glob`, `Bash` (`ls`) | `exec` nested tools |
| Read | `read_file` (2,000-line cap, offset/limit) | `Read` (line cap, images, PDFs, notebooks) | `read_file` / nested tools |
| Search | `grep_search`, `semantic_search` | `Grep` (ripgrep), `Glob` | `rg` via `exec_command` |
| Edit | `apply_patch`, `replace_string_in_file`, `multi_replace_string_in_file`, `insert_edit_into_file`, `create_file` | `Edit` (exact replacement), `Write`, `NotebookEdit` | `apply_patch` / nested edit tools |
| Execute | `run_in_terminal`, `execution_subagent` | `Bash` (persistent cwd, non-persistent shell state) | `exec` JS + `exec_command`; `wait` for cells |
| Verify | `get_errors`, `get_changed_files`, tests via terminal | `Bash`, test tools, `Read` | `exec` nested test commands |
| Plan | `manage_todo_list` | `TodoWrite`, `TaskCreate/Update/List` | `update_plan` / commentary |
| Delegate | `search_subagent`, `explore_subagent`, `execution_subagent` | `Agent` (`run_in_background`, `name`, `model`) | `spawn_agent`, `followup_task`, `send_message`, `wait_agent` |
| External | MCP tools, `fetch_webpage` | MCP tools, `WebFetch`, `WebSearch`, `ToolSearch` | MCP, `web.run`, apps/connectors |

**[S]** Claude's `ToolSearch` loads deferred tool schemas on demand; Copilot has a similar `tool_search_tool` and a "deferred tools" prompt section. This is a tool-schema cost control: don't ship every MCP schema in every request.

### 5.2 Authorization model

The verified model has five layers:

1. **Capability registry** — what the runtime can do at all.
2. **Per-run allowlist** — which tools are exposed to this model call.
3. **Argument/path policy** — whether this exact action is permitted (workspace root, excluded paths, symlinks, command class).
4. **Approval** — whether the user must approve this exact action.
5. **Execution sandbox** — what the process/container can reach even if approved.

**[S] Claude Code** states that tools run in a user-selected permission mode and prompts for actions not automatically allowed. It also says denial recovery must change the approach, not repeat the call.

**[S] Codex** records `approval_policy`, `approvals_reviewer`, `sandbox_policy` (`danger-full-access` in the sampled session), `permission_profile`, and `active_permission_profile` per turn. It also distinguishes commentary and final channels and requires explanation when an approval reviewer rejects an action.

**[S] Copilot** distinguishes permission levels (`autopilot`, `autoApprove`, and others), tool availability, and terminal sandboxing. Its session log recorded **247 permission requests** across the whole run and **217** in the B.Com→B.Sc phase, which is a lot of interactive friction; a product should make read-only exploration pre-approved and reserve prompts for writes, destructive commands, and network access.

### 5.3 Read guards that block legitimate work

Do not "fix" a bad read guard by disabling path protection. Classify paths explicitly:

```text
inside_workspace      -> allow read (subject to exclusions)
generated/vendor      -> deny by default, allow explicit override
outside_workspace     -> deny with "outside workspace; request approval"
nonexistent           -> "not found; did you mean <nearby path>?"
symlink/escape        -> resolve, re-check at execution time
```

Return **typed, actionable** errors. A generic "access denied" teaches the model nothing and sends it searching again. A denial should include the allowed root, the requested path, and the nearest allowed alternative.

**[S]** Copilot's `toolUtils` and file-resolution code path contains explicit workspace/external checks; its `read_file` contract uses absolute paths. The failure mode to avoid is treating a nonexistent in-workspace path as "external" and then refusing all nearby exploration.

### 5.4 Editor reflection

All three products route edits through a workspace service, not by letting the model write into the editor process. For a browser IDE:

- Make the **workspace filesystem the single source of truth** for agent edits.
- Apply edits transactionally and emit a file-change event with `path`, `old_hash`, `new_hash`, and a diff.
- Reconcile Monaco documents against the new content; do not keep a separate "model-visible file" copy.
- Record edits in a change set so the user can review/undo.
- Run path and permission checks **inside** the execution environment, immediately before the write.

---

## 6. Termination: how a mature agent actually stops

### 6.1 The signals

| Signal | Copilot | Claude Code | Codex |
|---|---|---|---|
| Model returns text, no tool calls | Candidate final; in autopilot, treated as done | Final turn text | `final` channel ends the turn |
| Explicit completion tool | `task_complete` (autopilot only) | `ExitPlanMode` for plan approval, not task completion | `task_complete` event |
| Tool budget exhausted | `hitToolCallLimit` / `maxToolCallsExceeded` | Turn/tool limits; compaction then continue | Turn/budget controls; `turn_aborted` |
| Cancellation | `isCancellationRequested`, `yieldRequested` | User interrupt; hooks; `canceled` | `turn_aborted` reason `interrupted` |
| Failed tool call | Recorded result; model decides | `is_error` result; model decides | `function_call_output` with error |
| Stop hook | Hook can block stop and add context | `Stop` hook (`stop_hook_summary`) | Not observed as a user-facing hook |
| Provider partial/incomplete | Response type classification + bounded retry | Provider error handling + retry | Response status + abort |
| Final summary at limit | Model final text or UI limit message | Compaction + continue; final summary | `task_complete.last_agent_message` |

### 6.2 The completion contract an ADE should enforce

A run is **completed** only when all of the following are persisted:

1. A terminal `run_status` (`completed`, `failed`, `blocked`, `cancelled`, `budget_exhausted`).
2. A `stop_reason` (`model_final`, `task_complete`, `tool_limit`, `deadline`, `provider_error`, `user_cancel`, `no_progress`).
3. A validation record: commands, exit codes, scope, and whether each required check ran (`passed`, `failed`, `not_run`, `blocked`).
4. A changed-file summary with hashes.
5. A final user-facing message, either model-authored or runtime-generated.
6. No pending tool/job without a terminal state.

**Never** mark a run successful because tests passed, or because the model called a completion tool. Tests are one fact. Completion is a lifecycle state.

### 6.3 Partial provider responses

Normalize every provider into a small set of outcomes:

```text
complete_text
complete_tool_calls
incomplete
provider_error
rate_limited
cancelled
refused
```

Rules:

- Execute a tool call only when its **name and full argument object** are complete and schema-valid.
- Persist the raw request/response IDs and any partial output for diagnosis.
- Retry only transient classes, with a cap and exponential backoff.
- Do not auto-retry `rate_limited`, `quota_exceeded`, `cancelled`, `refusal`, or policy-filtered content.
- Make side-effecting tools idempotent via a key derived from `(run_id, step_id, tool_name, normalized_args)`.

### 6.4 Finalization reserve

Reserve a small budget up front, for example:

```text
finalization_reserve = max(2,048, 8% of model window)
```

When the budget or tool limit is reached:

1. Stop scheduling new tools.
2. Transition to `finalizing`.
3. Make one bounded call using the compact run-state snapshot (no raw tool history).
4. If that fails or no budget remains, emit a deterministic runtime message:

   > "Run stopped at the tool limit. Files changed: ... Tests: ... Unresolved: ... This summary was generated by the platform, not the model."

This is the only reliable answer to "agent reached tool limit without a final summary."

---

## 7. Persistence: separate the planes

### 7.1 What the products store

**[S]/[L] Copilot**

- `events.jsonl`: append-only event log (session start, model calls, tool starts/completes, permissions, usage records, summaries).
- `session.db`: SQLite tables for workflow/factory runs, phases, agents, journal, progress.
- `checkpoints/`: Markdown checkpoints (`001-...md`, `002-...md`, `index.md`).
- `workspace.yaml`: session ID, cwd, client name, title, summary count, timestamps.
- UI checkpoints can restore affected workspace files and conversation, but not external side effects.

**[S]/[L] Claude Code**

- `~/.claude/projects/<encoded-cwd>/<session>.jsonl`: append-only transcript with user/assistant/system/attachment entries, `toolUseResult`, `parentUuid`, and `isSidechain`.
- `system` entries with `subtype: "compact_boundary"` carry `preTokens`, `postTokens`, `cumulativeDroppedTokens`, `durationMs`, `preservedSegment`, and `preservedMessages`.
- `~/.claude/file-history/`, `~/.claude/sessions/`, and `~/.claude/history.jsonl` hold editor/file and session metadata.
- Compaction inserts a continuation user message (`"This session is being continued..."`) plus `compact_file_reference` tombstones for files that were read but are too large to include.

**[S]/[L] Codex**

- `~/.codex/sessions/YYYY/MM/DD/rollout-*.jsonl`: `session_meta`, `world_state`, `turn_context`, `response_item`, `event_msg`, `token_usage_record`, `compacted`.
- `session_meta.payload.base_instructions.text`: the full base prompt.
- `compacted.payload.replacement_history`: the curated prefix; the summary itself is an encrypted `compaction` item.
- `resume_metadata` and window IDs support continuation.

### 7.2 The five stores an ADE needs

| Store | Contents | Authority |
|---|---|---|
| Workspace | files, branches/worktrees, build artifacts | Git/filesystem |
| Session transcript | messages, tool calls, permissions, usage, events | Append-only DB |
| Run state | phase, budgets, plan, evidence, validations, stop reason | DB (source of truth) |
| Artifacts | full tool outputs, file snapshots, logs, diffs | Object/file store |
| Prompt projection | the exact bounded context for the next call | Derived, disposable |

Plus **long-term instructions/memory**, which are not the same as conversation context.

**[I]** PostgreSQL should own runs, events, tool calls, jobs, artifacts metadata, and checkpoints. Redis should coordinate leases, cancellation signals, and notifications — never be the only copy of a terminal state. The container/job ID and last heartbeat must be durable so a reconnect can distinguish "still running," "recovered," and "lost with host."

---

## 8. Verified vs. inferred vs. unknown

| Claim | Status |
|---|---|
| Copilot's client harness has a tool-calling loop with a default 200-request cap and autopilot `task_complete` | **Verified [S]** in the installed extension |
| Copilot compacts at 78–82%, emergency 90%, applies at 65% | **Verified [S]** |
| Copilot caps tool-result rendering at 0.5× the model window and middle-truncates 40/60 | **Verified [S]** |
| Copilot `read_file` truncates at 2,000 lines | **Verified [S]** |
| Copilot spills large tool results to disk and returns a read handle | **Verified [S]** |
| Copilot's observed model window was 272K and cache reads dominated input | **Observed [L]** |
| Claude Code auto-compacts near the window limit and inserts a structured summary | **Verified [S]/[L]** |
| Claude's observed median compaction was ~968K → ~24K tokens (97.5%) | **Observed [L]** |
| Claude spills over-budget tool output to a file and tells the model to page it | **Verified [S]** |
| Codex stores a curated replacement history plus an encrypted compaction item | **Verified [L]** |
| Codex's compaction summary is plaintext and portable | **Unknown** — observed plaintext length was 0; item was encrypted |
| Provider routing, hidden prompts, index ranking, cache internals | **Unknown / opaque** |
| A specific universal token limit for all providers/tools | **Unknown** — values are version- and harness-specific |

---

## 9. Case study: the B.Com → B.Sc CS content rewrite

This is the run the user asked to inspect. It is useful because it is a real multi-file content migration, not a toy.

**[L] Observed facts** (from `~/.copilot/session-state/<session-id>/events.jsonl`):

- User steering message at 14:27: "This training is for B.Sc CS students, not for B.Com students, so make it better and correct."
- The model changed from `claude-haiku-4.5` to `gpt-6-luna` at that point.
- From 13:00 to 15:58: **151 assistant turns**, **283 tool executions**, **217 permission requests**.
- Tool mix: `view` 77, `apply_patch` 62, `rg` 26, `bash` 14, `create` 3, plus `glob`, `tool_search_tool`, `ask_user`, `set_workspace`.
- **16 distinct files** edited; repeated patches to the same files (e.g., `Days3-5-Summary.md` 8 edits, `Quick-Start-Guide.md` 7, `Day1-Content.md` 6).
- Only **4 timestamps** had two parallel tool calls; this harness was mostly sequential, not a parallel fan-out.
- Token usage: input **30,363–213,030**, cache reads up to **212,445**, model window **272,000**.
- Final message at 15:52 reported the B.Sc. adaptation, the Day 1 slide deck, projects, and index. It also stated: "I also checked the slide count and presenter notes, validated the embedded JavaScript syntax, and checked local Markdown links."
- Verification commands included:
  - `node -e '... vm ...'` to syntax-check the slide HTML's embedded JavaScript.
  - A Python script to scan Markdown links.
- The final summary was **short and outcome-oriented**, not a replay of every tool call.

**[I] Why this matters for the ADE.** The mature behavior was not a magic model. It was:

1. A clear user correction treated as steering, not a new task.
2. Many small, bounded tool calls against one workspace.
3. Repeated targeted patches rather than one giant rewrite.
4. An explicit verification pass before the final answer.
5. A final message that names changed artifacts and the checks performed.

The 217 permission requests are a warning: interactive friction at that volume is a product problem. Pre-approve reads and local searches; prompt only for writes, destructive commands, and network/egress.

---

## 10. CS Visually ADE comparison and fixes

The following assumes the stack described in the task: React + Monaco, FastAPI, PostgreSQL, Redis, isolated Docker workspaces, DeepSeek/Ollama, tool-calling agents, independent hidden tests. The repo inspection did not find that runtime, so these are architecture changes for the described system.

### 10.1 Problem → pattern → implementation

| Problem | What mature agents do | Reusable pattern | FastAPI implementation | Trade-offs / failure modes |
|---|---|---|---|---|
| **1. Tool history exhausts 100K** | Copilot builds a prioritized projection; compacts at 78–90%; caps tool results at 0.5× window; spills large results to disk. Claude compacts ~968K→24K and spills output to files. Codex uses a curated replacement history. | Durable transcript + disposable prompt projection + artifact store + compaction. | `prompt_projector.py`: token-count each section; stable prefix; recent window; evidence excerpts; artifact handles. `artifacts.py`: write full output, return `{artifact_id, preview, ranges}`. Compaction at 0.78–0.82, emergency 0.90. | Summaries can lose exact constraints; keep the immutable goal/acceptance criteria outside the summary. Token counts differ by provider; use the provider's counter when available. |
| **2. Repeated searches, no progress** | Copilot has tool budgets and subagents; Claude tells the model not to duplicate a subagent's work; Codex uses one `exec` program for independent searches. | Fingerprint + evidence ledger + no-progress detector + subagent isolation. | `progress.py`: hash `(tool, args, workspace_rev)`, store result digest. On repeat, return prior evidence and require a changed argument. After 3, stop with `blocked`. | Aggressive dedupe can hide legitimate re-checks after edits; invalidate on workspace revision/hash. |
| **3. Read guards block exploration** | Copilot resolves workspace paths and has explicit external checks; Claude instructs diagnosis after denial, not a repeat. | Typed path classification + least privilege + actionable denials. | `path_policy.py`: `inside`, `excluded`, `outside`, `missing`, `symlink_escape`. Denial payload includes root, requested path, nearest allowed alternative. Re-check inside the container. | Symlinks/mounts/races; resolve at execution time and keep the workspace root authoritative. |
| **4. Tool limit reached without final summary** | Copilot shows a limit message and can continue; autopilot uses `task_complete`; Codex emits `task_complete` with `last_agent_message`. | Run budget + `finalizing` phase + reserved finalization call + deterministic fallback. | `finalizer.py`: reserve `max(2048, 8%)`; on limit, one bounded summary call; if it fails, generate a platform summary from `RunState`. | The finalization call can also fail; the fallback must be clearly labeled and must not claim success. |
| **5. Provider incomplete responses** | Copilot classifies response types, retries selected transient errors, and excludes rate-limit/quota/cancel/refusal. | Provider adapter with explicit outcomes and validated tool-call assembly. | `providers/base.py` returns `complete_text | complete_tool_calls | incomplete | provider_error | rate_limited | cancelled`. Never execute partial arguments. Retry only transient, max 3. | Providers differ in finish reasons; conformance tests per model/provider are mandatory. |
| **6. Tests pass, agent does not terminate** | Claude/Codex treat completion as a separate event; Copilot treats a text-only round as done but still tracks limits. | Separate `test_status` from `run_status`; explicit terminal event; watchdog. | `runs` table with `phase`, `stop_reason`, `final_message_id`; `jobs` table with heartbeat; idempotent terminal transition. | A watchdog can race with a slow job; use leases and compare-and-set transitions. |

### 10.2 Target runtime shape

```text
POST /v1/runs
  -> create run (queued)
  -> orchestrator leases run
  -> planning -> executing <-> verifying -> finalizing -> completed
                         |            |
                         +-> blocked  +-> failed
  any active -> cancelled | budget_exhausted | interrupted

Every transition writes run_events + updates runs atomically.
Every model call writes a model_calls row (prompt hash, tokens, cache, latency).
Every tool call writes a tool_calls row + artifact rows for large output.
Every terminal state writes a final_message row (model or platform).
```

### 10.3 Data model (minimum)

```sql
runs(id, user_id, workspace_id, goal, acceptance_criteria jsonb,
     phase, stop_reason, model, provider, workspace_revision,
     started_at, deadline_at, completed_at, final_message_id)

run_events(id, run_id, seq, type, payload jsonb, created_at)

model_calls(id, run_id, turn_id, model, prompt_hash, input_tokens,
            cached_tokens, output_tokens, latency_ms, provider_request_id,
            outcome, created_at)

tool_calls(id, run_id, turn_id, tool_name, args jsonb, args_hash,
           workspace_revision, status, result_artifact_id, result_digest,
           error_class, started_at, completed_at)

artifacts(id, run_id, kind, content_path, bytes, sha256, created_at)

jobs(id, run_id, kind, command, status, exit_code, output_artifact_id,
     heartbeat_at, lease_expires_at, cancel_requested_at)

compactions(id, run_id, window_number, pre_tokens, post_tokens,
            summary_artifact_id, model, duration_ms, created_at)

checkpoints(id, run_id, workspace_revision, diff_artifact_id, created_at)
```

Redis keys:

```text
run:{id}:lease          -> worker id, TTL
run:{id}:cancel         -> signal
run:{id}:events         -> pub/sub channel (not the source of truth)
job:{id}:heartbeat      -> TTL
```

### 10.4 Prompt projector (P0)

```python
from dataclasses import dataclass

@dataclass
class Budget:
    window: int
    reserved_output: int
    reserved_finalize: int

    @property
    def usable(self) -> int:
        return self.window - self.reserved_output - self.reserved_finalize

def project(run, recent_turns, evidence, tools, budget, counter):
    sections = [
        ("system",  system_policy(),                 1.00),
        ("tools",   render_tool_schemas(tools),      1.00),
        ("goal",    run.goal + run.acceptance,       1.00),  # never summarized away
        ("state",   run_state_snapshot(run),         0.60),
        ("summary", run.carryover_summary or "",     0.50),
        ("recent",  render_recent(recent_turns),     0.80),
        ("evidence",render_evidence(evidence),       0.40),
    ]
    # Trim from the bottom priority upward until it fits.
    # Never trim: system, tools, goal.
    # Evidence is already artifact-backed and range-bounded.
    ...
```

Rules:

- Count tokens **after** rendering, not before.
- Keep the stable prefix (system, tools, goal) byte-identical between calls where possible.
- Put timestamps/random IDs in trailing sections.
- If the projection cannot fit, compact or fail loudly; do not silently truncate the goal.

### 10.5 Artifact-backed tool results (P0)

```python
async def handle_tool_result(run, call, raw: str):
    tokens = counter.count(raw)
    if tokens <= TOOL_RESULT_INLINE_TOKENS:       # e.g. 2_000
        return {"kind": "inline", "text": raw}

    artifact = await artifacts.put(run.id, raw)
    preview = head_tail(raw, head=0.4, tail=0.6,
                        max_tokens=TOOL_RESULT_PREVIEW_TOKENS)
    return {
        "kind": "artifact",
        "artifact_id": artifact.id,
        "bytes": len(raw),
        "preview": preview,
        "note": "Full output stored. Use read_artifact(artifact_id, offset, limit)."
    }
```

The model gets a **handle**, not the whole output. A `read_artifact` tool pages it. This is the direct analogue of Copilot's "large tool result written to file" and Claude's "output has been saved to ..." behavior.

### 10.6 Compaction service (P0)

```python
WARM_MIN, WARM_JITTER = 0.78, 0.04
EMERGENCY = 0.90
APPLY_MIN = 0.65

def should_compact(pre_render_tokens, window, random_value):
    ratio = pre_render_tokens / window
    return ratio >= (WARM_MIN + random_value * WARM_JITTER)

async def compact(run):
    summary = await model_call(
        model=run.compaction_model,
        messages=build_summary_prompt(run),
        temperature=0,
        tools=[],
        tool_choice="none",
        max_tokens=SUMMARY_MAX_TOKENS,
    )
    await compactions.insert(run.id, pre=..., post=..., summary=...)
    await runs.update(run.id, carryover_summary=summary.text)
```

Summary prompt requirements (adapt from the verified prompts):

- Immutable user goal and acceptance criteria.
- All user messages, including corrections and security constraints (verbatim where security-relevant).
- Files read/changed with hashes.
- Errors and fixes.
- Completed vs. pending.
- Exact next step, quoted from the most recent user message.
- Recent tool commands/results (bounded).

Do **not** let the summary replace the original user goal in the database. The goal is immutable; the summary is a projection aid.

### 10.7 No-progress detector (P0)

```python
def fingerprint(tool_name, args, workspace_revision):
    normalized = normalize(args)          # sort keys, strip volatile fields
    return sha256(f"{tool_name}:{normalized}:{workspace_revision}")

async def before_tool(run, call):
    fp = fingerprint(call.name, call.args, run.workspace_revision)
    prior = await evidence.get(run.id, fp)
    if prior and prior.result_digest == await current_digest(call):
        run.repeat_count[fp] += 1
        if run.repeat_count[fp] >= 2:
            return Deny(
                reason="repeat_no_progress",
                message=(
                    f"You already ran this exact query at turn {prior.turn}. "
                    f"Result: {prior.summary}. Choose a different hypothesis, "
                    f"narrow the path, or read {prior.files[0]}."
                ),
            )
    return Allow()
```

After the third repeat, stop the run with `stop_reason = "no_progress"` and a deterministic final summary. This is the behavior that prevents "agents passing tests but failing to terminate cleanly."

### 10.8 Path policy (P1)

```python
class PathClass(Enum):
    INSIDE = "inside"
    EXCLUDED = "excluded"
    OUTSIDE = "outside"
    MISSING = "missing"
    SYMLINK_ESCAPE = "symlink_escape"

def classify(path, workspace_root, exclusions):
    resolved = realpath(path)
    if is_relative_to(resolved, workspace_root):
        if matches_any(resolved, exclusions):
            return PathClass.EXCLUDED
        return PathClass.INSIDE
    if not exists(resolved):
        return PathClass.MISSING
    return PathClass.OUTSIDE
```

Return errors that include the workspace root and a suggested allowed path. Never return a bare "denied."

### 10.9 Job lifecycle (P1)

Terminal commands and tests must be jobs:

```text
POST /v1/runs/{run_id}/jobs -> {job_id}
GET  /v1/jobs/{job_id}      -> {status, exit_code, output_artifact_id, tail}
POST /v1/jobs/{job_id}/cancel
```

Persist:

- `job_id`, command, cwd, env allowlist
- `status` (`queued`, `running`, `completed`, `failed`, `cancelled`, `lost`)
- `heartbeat_at`, `lease_expires_at`
- `exit_code`, `output_artifact_id`
- `idempotency_key`

On browser disconnect, the job keeps running. On reconnect, the client reads the same job state instead of re-running the command.

### 10.10 Provider adapter (P0)

```python
@dataclass
class ModelOutcome:
    kind: Literal["complete_text", "complete_tool_calls",
                  "incomplete", "provider_error", "rate_limited",
                  "cancelled", "refused"]
    text: str | None
    tool_calls: list[ToolCall] | None
    usage: Usage | None
    request_id: str | None
```

Rules:

- Parse streamed tool arguments into a complete JSON object before execution.
- If the stream ends mid-argument, return `incomplete`; do not execute.
- Map provider error codes to the small outcome set.
- Retry only transient classes; cap at 3; record the request ID.
- Run conformance tests for DeepSeek, Ollama, and any hosted provider: complete text, complete tool call, truncated tool call, rate limit, timeout, cancellation, refusal.

### 10.11 Finalizer (P0)

```python
async def finalize(run, reason):
    await runs.set_phase(run.id, "finalizing")
    snapshot = run_state_snapshot(run)
    if budget_remaining(run) >= MIN_FINALIZE_TOKENS:
        try:
            msg = await model_call(finalize_prompt(snapshot))
            await persist_final(run, msg.text, source="model")
            await runs.complete(run.id, reason)
            return
        except Exception:
            pass
    msg = render_platform_summary(snapshot)   # deterministic
    await persist_final(run, msg, source="platform")
    await runs.complete(run.id, reason)
```

The platform summary must state:

- What was attempted.
- What changed (files).
- What was validated (commands/exit codes, or "not run").
- What remains unresolved.
- That it was generated by the platform, not the model.

### 10.12 Observability

Log per run:

- prompt composition (section → tokens, truncated sections)
- model call (model, prompt hash, input/cached/output tokens, latency, TTFT, request ID, outcome)
- tool call (name, args hash, workspace revision, duration, result bytes, truncation/artifact)
- compaction (pre/post tokens, model, duration, apply/skip reason)
- repeat/no-progress events
- terminal state and stop reason

Expose a UI timeline from durable events, not from client-side reconstruction. This is what makes "why did it stop?" answerable.

---

## 11. Prioritized implementation plan

### P0 — Stop the bleeding

- [ ] **Prompt projector**: stable prefix + immutable goal + run state + recent turns + artifact handles; token ledger per section.
- [ ] **Artifact-backed tool output**: persist large results; return preview + `artifact_id`; add `read_artifact(offset, limit)`.
- [ ] **Run state machine**: `queued → planning → executing → verifying → finalizing → terminal`; persist `stop_reason`.
- [ ] **Budgets**: global tool-call cap (default 200), per-tool caps, wall-clock deadline, retry cap (3), finalization reserve.
- [ ] **Compaction**: trigger at 78–82%, emergency 90%, apply at 65%; structured summary prompt; keep the original goal outside the summary.
- [ ] **Provider adapter**: explicit outcomes; never execute partial tool arguments; conformance tests.
- [ ] **No-progress detector**: fingerprint + evidence ledger; repeat → redirect; third repeat → stop with summary.
- [ ] **Finalizer**: reserved finalization call + deterministic platform fallback.

**Acceptance tests**

- Force tool-limit exhaustion after a file edit → run terminates, edit persisted, validation accurate, final message exists.
- Simulate provider truncation mid-arguments → no side effect, run records `incomplete`.
- Return identical search results repeatedly → agent does not issue the same call indefinitely.
- Force context above 80% → compaction runs; the original user goal is still present verbatim in the next prompt.

### P1 — Make exploration and recovery reliable

- [ ] Search/evidence ledger scoped to `workspace_revision` and file hashes.
- [ ] `list`, text/semantic search, symbol lookup, bounded read, diff-aware tools with consistent workspace identity.
- [ ] Typed path errors (`inside`, `excluded`, `outside`, `missing`, `symlink_escape`) with suggestions.
- [ ] Re-check path/command permissions inside the container at execution time.
- [ ] Jobs with `job_id`, heartbeat, output tail, exit code, cancellation, reconnect.
- [ ] Stale-worker recovery and idempotent terminal transitions.
- [ ] Subagents for independent exploration/review, with isolated context and a bounded report.

**Acceptance tests**

- Disconnect the browser during a test run → reconnect shows the same job state, no rerun.
- Resolve an in-workspace file and an out-of-root symlink → legitimate read works, boundary read is blocked with an actionable error.
- Launch two subagents on independent directories → parent context does not receive their raw tool history, only their reports.

### P2 — Explainability and collaboration

- [ ] UI timeline from durable events: model call → tool proposal → authorization → execution → artifact → validation → final status.
- [ ] User-reviewed checkpoints and workspace diffs; document what rollback cannot undo.
- [ ] Context/memory provenance and invalidation by workspace revision.
- [ ] Provider conformance suite with exact stop/retry/truncation behavior.
- [ ] Metrics: tokens per run, tool output bytes, repeat-call rate, incomplete-response rate, budget-exhaustion rate, "tests passed but not finalized" rate.

---

## 12. Concrete changes to the FastAPI runtime

A minimal file layout that fits the existing modular monolith:

```text
backend/modules/agent/
  __init__.py
  api.py              # POST /v1/runs, GET /v1/runs/{id}, events, cancel
  orchestrator.py     # lease, phase machine, loop
  prompt_projector.py # budgeted context assembly
  compaction.py       # trigger, summary prompt, apply
  tools/
    registry.py       # capability registry + per-run allowlist
    fs.py             # read/list/search/patch/create
    terminal.py       # jobs: run, poll, cancel
    artifacts.py      # put/get/preview/page
  providers/
    base.py           # ModelOutcome + ToolCall
    deepseek.py
    ollama.py
  progress.py         # fingerprint + evidence ledger
  path_policy.py      # typed path classification
  finalizer.py        # reserved finalization + platform summary
  models.py           # SQLAlchemy tables
  events.py           # append-only run events + pub/sub
```

Integration points with the existing server:

- Keep Judge0 / hidden-test evaluation as an independent verifier. The agent may run visible checks; hidden tests remain a separate signal.
- Use PostgreSQL for `runs`, `run_events`, `tool_calls`, `jobs`, `artifacts`, `compactions`, `checkpoints`.
- Use Redis only for leases, cancellation, and notifications.
- Keep Monaco/React and Docker workspaces. The evidence does not justify rebuilding them; the failures are in orchestration, context, tool-result handling, provider adapters, and completion state.

---

## 13. Checklist for CS Visually

**Context**

- [ ] The original user goal and acceptance criteria are stored immutably and included in every prompt.
- [ ] Every model call has a section-level token ledger.
- [ ] Tool schemas are versioned; only enabled tools are sent.
- [ ] Large tool outputs are artifacts, not prompt text.
- [ ] Compaction triggers at 78–82%, emergency at 90%, applies at 65%.
- [ ] The summary preserves all user messages and security constraints verbatim.
- [ ] Stable prefix ordering enables provider caching.
- [ ] Repeated search calls are detected and redirected.

**Tools**

- [ ] Read, write, terminal, and network are separate capabilities.
- [ ] Path classification is typed and actionable.
- [ ] Reads are pre-approved; writes/destructive commands/egress require approval.
- [ ] `read_file` has an explicit line/byte cap and offset/limit.
- [ ] Terminal/tests are jobs with IDs, heartbeats, and cancellation.
- [ ] File edits go through one workspace-authoritative path and emit diffs.

**Termination**

- [ ] `run_status` and `test_status` are separate.
- [ ] Every terminal path has a `stop_reason`.
- [ ] A finalization budget is reserved.
- [ ] The platform can emit a truthful final summary when the model cannot.
- [ ] Provider partial responses never trigger tool side effects.
- [ ] Retries are capped and exclude non-transient classes.
- [ ] A watchdog reconciles stale `running` runs.

**Persistence**

- [ ] The transcript is append-only.
- [ ] The prompt projection is disposable and reproducible from run state.
- [ ] Artifacts have hashes and retrieval handles.
- [ ] Checkpoints record workspace revision and change set.
- [ ] Redis is not the only copy of any terminal state.

**Observability**

- [ ] Every model call, tool call, job, compaction, and terminal transition is traceable by `run_id`/`turn_id`.
- [ ] The UI timeline is built from durable events.
- [ ] Metrics cover tokens, repeats, incompletes, budget exhaustion, and unfinalized runs.

---

## 14. References

### Local primary artifacts (authoritative for the versions observed)

- `Applications/Visual Studio Code.app/Contents/Resources/app/extensions/copilot/dist/extension.js` — Copilot Chat 0.72.0 / VS Code 1.144.1. Key symbols: `ToolCallingLoop`, `TASK_COMPLETE_TOOL_NAME`, `MAX_AUTOPILOT_RETRIES`, `MAX_AUTOPILOT_ITERATIONS`, `F7e`, `tro`, `read_file` schema, `$v` truncation, `D8n` summarization prompt.
- `~/.copilot/session-state/<session-id>/events.jsonl`, `session.db`, `checkpoints/`, `workspace.yaml` — Copilot SDK/agent host run.
- `~/.local/share/claude/versions/2.1.272` — Claude Code CLI. String-extracted system prompt, tool contracts, auto-compact text, compaction prompt, overflow-to-file text.
- `~/.vscode/extensions/anthropic.claude-code-2.1.318-darwin-arm64/extension.js` — Claude Code VS Code integration.
- `~/.claude/projects/*/*.jsonl` — Claude Code transcripts; `compact_boundary` records.
- `~/.codex/sessions/**/rollout-*.jsonl` — Codex rollouts; `session_meta.payload.base_instructions`, `compacted.payload.replacement_history`, `token_usage_record`, `task_complete`.
- `~/.codex/config.toml` — model, approval/sandbox, plugins, MCP configuration (secrets deliberately not reproduced).
- `~/Desktop/dsa-visualizer` at `701b974` — CS Visually platform repo; `docs/architecture.md` for the React/Vite/Monaco + FastAPI + PostgreSQL + Redis + Judge0 stack.

### Official documentation and public source entry points

- VS Code AI tools API: https://code.visualstudio.com/api/extension-guides/ai/tools
- VS Code extension API reference: https://code.visualstudio.com/api/references/vscode-api
- VS Code Copilot extension source: https://github.com/microsoft/vscode/tree/main/extensions/copilot
- VS Code chat sample: https://github.com/microsoft/vscode-extension-samples/tree/main/chat-sample
- GitHub Copilot documentation: https://docs.github.com/en/copilot
- Claude Code documentation: https://docs.anthropic.com/en/docs/claude-code
- Codex repository: https://github.com/openai/codex

### Method note

Commands used were read-only local inspections: `rg`, `strings` on the user's installed binaries, `json` parsing of the user's own logs, and file reads. No network calls, credential files, or secret values were accessed or reproduced. Version-specific constants should be re-verified after an upgrade; minified symbol names and thresholds are not a stable API.

---

## 15. Bottom line

The mature agents are not winning because of a better model. They are winning because the harness:

- keeps a **small, stable, cacheable prefix**;
- treats raw tool output as **artifacts**, not prompt text;
- **compacts on a measured ratio** before the window is full;
- maintains **explicit budgets** and a **completion protocol**;
- makes **termination a controller state**, not a model mood;
- separates **transcript, run state, workspace state, and prompt projection**.

For CS Visually, the highest-leverage change is a **prompt projector + artifact-backed tool results + a run state machine with a reserved finalization step**. Keep React/Monaco, FastAPI, PostgreSQL, Redis, Docker workspaces, DeepSeek/Ollama, and independent hidden tests. Fix the orchestration layer; do not rebuild the IDE.
