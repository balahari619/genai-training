# Day 2: Prompt Engineering & AI for Computer Science

**Theme:** From asking questions to directing and evaluating AI

**Audience:** B.Sc. Computer Science students

**Duration:** 4 scheduled hours, including a 15-minute break

**Approach:** 45 minutes concepts + 135 minutes guided hands-on + 45 minutes activities

**Prerequisites:** Day 1 AI literacy; programming experience is helpful, not required

## Instructor materials

- [Detailed Tanglish speaker notes](./Speaker-Notes-Day2.md) — what to say, questions to ask, and transitions
- [Day 2 activity workbook](../activities/Day2-Activities.md) — student tasks, submission template, and facilitator answer checks
- [Prompt engineering reference](../resources/Prompt-Engineering-Guide.md)

This file is the teaching plan and demonstration reference. The separate speaker-notes file is the delivery script. The presentation outline below is a storyboard, not an existing Day 2 HTML slide deck.

## 1. Outcomes and take-home deliverables

By the end of Day 2, students should be able to:

1. Turn an unclear request into a specific task with useful context and a checkable output.
2. Use constraints, examples, and structured output without assuming they guarantee correctness.
3. Ask AI for code explanations, bug hypotheses, test cases, and documentation.
4. Verify a generated explanation with a trace, a test, or a trusted source.
5. Refine a prompt based on an observed mismatch, rather than repeatedly saying “try again.”
6. Use AI for study and career preparation without inventing qualifications or disclosing private information.

Each student or pair leaves with:

- A reusable toolkit of **five prompts**: concept tutor, code explainer, debugging helper, test designer, and study/career helper.
- One completed **before → after → verification** record.
- A worksheet containing test inputs and expected outputs for a toy function.
- A final challenge response with evidence and one acknowledged limitation.

These are activities, not a mandatory third workshop project. Students without account access can use the printed fallback responses below.

## 2. Exact run of show

| Time | Duration | Segment | Learning mode |
|---|---:|---|---|
| 09:00–09:30 | 30 min | Recap, prompt anatomy, first demonstration | Concepts and discussion |
| 09:30–09:45 | 15 min | Task, audience, and useful context | Guided hands-on |
| 09:45–10:00 | 15 min | Constraints and structured output | Guided hands-on |
| 10:00–10:15 | 15 min | Few-shot prompting | Guided hands-on |
| 10:15–10:30 | 15 min | Code explanation and trace table | Guided hands-on |
| 10:30–10:45 | 15 min | Debugging and test design | Guided hands-on |
| 10:45–11:00 | 15 min | Break | — |
| 11:00–11:15 | 15 min | Checkable evidence, uncertainty, and iteration | Concepts |
| 11:15–11:30 | 15 min | Refine a response using a specific defect | Guided hands-on |
| 11:30–11:45 | 15 min | Source-based CS study helper | Guided hands-on |
| 11:45–12:00 | 15 min | Honest project description and mock interview | Guided hands-on |
| 12:00–12:15 | 15 min | Assemble and peer-test a five-prompt toolkit | Guided hands-on |
| 12:15–12:45 | 30 min | Prompt challenge: design, generate, verify | Activities |
| 12:45–12:55 | 10 min | Share-back and peer review | Activities |
| 12:55–13:00 | 5 min | Exit ticket and Day 3 bridge | Activities |

Do not add lecture time on top of these blocks. The long practice blocks include student work, instructor coaching, and short debriefs.

## 3. Preparation and access

### Before the session

- Test one institution-approved chat assistant and a backup. Comparing products is optional.
- Prepare printed copies of the workbook and fallback outputs.
- Have a timer, plain-text editor, and an approved environment for the optional Python demonstration.
- Use the synthetic profile and original source note in this file; do not request students' actual resumes or college records.
- Check assignment rules and explain what assistance/disclosure is allowed.
- Prepare a visible table with columns: **Task / Prompt / Output / Verification / Limitation**.

### Participation paths

| Situation | Participation |
|---|---|
| Students have approved access | Work individually or in pairs |
| Only facilitator has access | Pairs write prompts; facilitator runs selected prompts |
| No AI access/internet | Critique prepared responses; write improved prompts; manually trace code |
| Students do not know Python | Use the pseudocode and trace worksheet; executing code is optional |

Never require paid plans, personal account creation, API keys, or a particular upload feature. Do not upload restricted code, credentials, private student information, or unapproved copyrighted material.

## 4. Prompting foundations — 30 minutes

### Definition

A prompt is an instruction and the context supplied to an AI system. Prompt engineering here means designing, testing, and refining those instructions for a task. It is not a magic formula that makes all answers correct.

### A practical prompt checklist

| Element | Question | Example |
|---|---|---|
| Task | What do I want? | Explain binary search |
| Audience/context | What does the learner already know? | First-year CS student familiar with arrays |
| Constraints | What must be included or avoided? | State the sorted-input requirement; under 180 words |
| Output | How will I use/check the answer? | Definition, trace, misconception, two questions |
| Evidence/check | How will I verify it? | Compare the trace with a small sorted array |

A role such as “CS tutor” can set tone. It does not grant real expertise. Examples can clarify a pattern, but they are optional when unnecessary. Review a prompt for its suitability for the task, not how many elements it contains.

### Demonstration: vague → clearer → checkable

**Vague**

```text
Explain binary search.
```

**Clearer**

```text
Explain binary search to a first-year CS student who knows arrays
but has not studied searching algorithms.
```

**Checkable**

```text
Explain binary search to a first-year CS student who knows arrays.
Include the sorted-input requirement, a short definition, and a trace
for finding 11 in [2, 5, 8, 11, 14].
Use zero-based indexes and choose mid = floor((low + high) / 2).
Then list one common misconception and two practice questions.
Keep the explanation under 180 words. Do not claim to have run code.
```

**Facilitator check:** With inclusive `low/high`, start at `0/4`: midpoint 2 gives 8, then search indexes 3–4; midpoint 3 gives 11. The array must be sorted under the same ordering used for comparisons.

Do not promise that the third prompt always produces a correct trace or exact word count. Check the actual response against the requested fields.

## 5. Guided prompting workshop — 75 minutes

### Lab 1 — Task, context, and role (15 minutes)

**Task:** Improve “Teach me recursion.”

1. Instructor models the difference between a role and useful context (3 min).
2. Pairs write a prompt with learner background and a specific learning goal (7 min).
3. Run/inspect one response or critique the fallback (3 min).
4. Record one check (2 min).

**Example prompt**

```text
Help me learn recursion. I understand loops, but recursive calls are new.
Use the role of a patient CS tutor.
Explain the base case and recursive case with factorial of 3.
Show the calls and return values, then ask me two questions.
Keep language simple, but do not say recursion always saves time.
```

**Answer checks:** `factorial(3) = 3 × 2 × 1 = 6`; a base case stops this example's recursive chain. Recursive code is not automatically faster or simpler.

**Discussion:** Extra personal details and invented expert credentials are not useful context. Add information only if it changes the answer needed.

### Lab 2 — Constraints and structured output (15 minutes)

**Task:** Compare arrays and singly linked lists.

```text
Compare a fixed-size array with a singly linked list for a CS study sheet.
Assume unsorted data; for linked-list operations, distinguish whether
the relevant node/predecessor is already known or must be found.
Use a table: Aspect | Array | Singly linked list | Assumption.
Include indexed access, searching, insertion, deletion, and memory layout.
Explain in one sentence why insertion is not always O(1).
Do not treat Python lists as identical to fixed-size arrays.
```

**Answer checks**

- Array indexed access: typically O(1); unsorted search: O(n).
- Linked-list indexed access/search: O(n).
- Linked-list insertion can be O(1) given the necessary node/reference, but finding the position can cost O(n).
- Singly linked-list deletion may need a predecessor; do not claim arbitrary-node deletion is universally O(1).
- Arrays generally use contiguous element storage; linked lists use nodes with links and allocation overhead.

**Teaching point:** A nicely formatted but incorrect table is still incorrect. Structure improves usability, not truth.

### Lab 3 — Few-shot prompting (15 minutes)

**Task:** Apply an output pattern to new inputs.

```text
Classify these toy bug reports using only one label:
validation, calculation, or display.

Examples:
"Blank name is accepted" -> validation
"Total is added incorrectly" -> calculation
"Button text is cut off" -> display

Now classify:
1. Negative age is accepted.
2. Final price uses the wrong tax percentage.
3. A heading overlaps the menu.

Return: number | label | brief reason.
If a report is ambiguous, say what detail is missing.
```

**Expected labels:** validation, calculation, display. Reasons must match each report.

**Extension:** “Page crashes when I press submit” cannot reliably be assigned to one of those categories without more evidence. Asking for missing detail is acceptable.

**Teaching point:** Examples guide output during the request. They do not retrain or fine-tune model parameters. Bad examples can teach the wrong pattern.

### Lab 4 — Explain and trace code (15 minutes)

Use this original toy function:

```python
def count_even(numbers):
    count = 0
    for index in range(len(numbers) - 1):
        if numbers[index] % 2 == 0:
            count += 1
    return count
```

For students unfamiliar with Python:

```text
count starts at 0
visit indexes from 0 up to, but not including, length(numbers) - 1
if the number at the index is even, increase count by 1
return count
```

```text
Explain this function without changing it.
Trace count_even([2, 3, 4]) in a table:
index | value checked | count after this iteration.
State the actual return value and the intended count of even numbers.
Explain any mismatch. Treat the input as a list of integers.
Do not claim you executed the function.
[paste the toy function]
```

**Facilitator answer:** It visits indexes 0 and 1, not 2. Count becomes 1, then stays 1; actual return is 1, intended count is 2. The final item is skipped.

**Teaching point:** A trace is a generated explanation, not execution evidence. Verify it manually or run the function in an approved environment.

### Lab 5 — Debugging and test design (15 minutes)

```text
The intended behavior is to count all even integers in the supplied list.
For [2, 3, 4], the function returns 1 but should return 2.
First explain the likely cause. Then suggest the smallest fix.
Give tests for empty input, one item, mixed values, and a negative even value.
Return input | expected output | what the test checks.
Do not invent execution results.
[paste the toy function]
```

**Minimal fix:** Change `range(len(numbers) - 1)` to `range(len(numbers))`. Direct iteration over values is another valid solution, but is not the smallest textual change.

| Input | Expected corrected result | Reason |
|---|---:|---|
| `[]` | 0 | Empty input |
| `[2]` | 1 | A single even item must not be skipped |
| `[3]` | 0 | A single odd item |
| `[2, 3, 4]` | 2 | Mixed input with an even final item |
| `[-2, 1, 0]` | 2 | Negative even integers and zero |

Ask students why `[2, 3]` alone is a weak regression test: the buggy and corrected functions both return 1 because the omitted final item is odd.

**Optional execution:** Run the original, apply the minimal fix, and run these inputs again. Record actual output separately from expected output. Do not install packages; the toy example uses standard Python only.

## 6. Checkable explanations and iteration — 30 minutes

### Explain the evidence ladder (15 minutes concepts)

| What you have | What it establishes |
|---|---|
| Fluent answer | The response sounds plausible |
| Assumptions and trace | A proposed explanation you can inspect |
| Source passage | Evidence for a source-specific claim, if the passage supports it |
| Actual test output | Behavior on the tested inputs in that environment |
| Broader tests and review | More confidence, not a universal guarantee |

Do not ask for hidden reasoning or assume a long “step-by-step” answer proves correctness. Ask for concise explanations, explicit assumptions, trace tables, references, or tests that you can inspect.

### Run the refinement exercise (15 minutes hands-on)

**Defective prepared response**

> “Binary search works on any list. For `[2, 5, 8, 11, 14]`, it checks 8, then 14, then 11. It is always O(1).”

Students should identify:

1. Standard binary search needs sorted data.
2. The stated trace does not follow the midpoint rule used in the demonstration.
3. Binary search has O(log n) worst-case comparisons on a sorted random-access array, not universally O(1).

**Specific refinement**

```text
Your answer says binary search works on any list and is always O(1).
Correct those claims. For an ascending sorted random-access array,
state the worst-case comparison complexity.
Trace target 11 in [2, 5, 8, 11, 14], using zero-based indexes,
inclusive low/high bounds, and mid = floor((low + high) / 2).
Show low | high | mid | value | decision.
Flag uncertainty rather than guessing.
```

**Check:** Rows `0 | 4 | 2 | 8 | search right`, then `3 | 4 | 3 | 11 | found`.

**Stop rule:** Try one targeted revision and check again. If still wrong, use course notes or a trusted source and document the unresolved issue. Do not spend the whole class prompting indefinitely.

## 7. CS study and career preparation — 45 minutes

### A. Source-based study helper (15 minutes)

Use this original, permitted classroom note:

> A stack follows last in, first out (LIFO). Push adds an item to the top; pop removes the top item. Starting with an empty stack, push A, push B, then pop removes B, leaving A. A queue follows first in, first out (FIFO). Enqueue adds an item at the rear; dequeue removes the oldest item at the front. Starting with an empty queue, enqueue A, enqueue B, then dequeue removes A, leaving B.

```text
Use only the classroom note below.
Create a study sheet with:
1. A stack/queue comparison table.
2. One traced example for each.
3. Two practice questions, with answers in a separate section.
4. A section called "Not covered by this note".
Do not invent exam dates, syllabus topics, or implementation complexities.
[paste the classroom note]
```

**Checks:** Stack removes B; queue removes A. The note does not specify exam dates, course requirements, or operation complexities.

**Out-of-source test:** “When is my data structures exam?” The assistant should say the supplied note does not provide it, not invent a date.

**Bridge to Day 3:** Supplying a short note in a prompt introduces source grounding. A document workspace can manage more sources, but neither method eliminates the need to check answers.

### B. Honest project description and mock interview (15 minutes)

**Synthetic profile**

- Final-year B.Sc. CS student.
- Knows basic Python and SQL; no internship experience.
- Built a command-line library tracker as a course project.
- Personal contribution: menu handling and input validation.
- Project testing: five manual test cases; no measured user or business impact.

```text
Using only the synthetic profile below, write two resume bullets
for an entry-level software internship.
Do not invent internships, expert-level skills, usage numbers,
awards, or performance improvements.
If evidence is missing, ask a question rather than adding a metric.
[paste the profile]
```

**Acceptable example**

- Implemented menu handling and input validation for a command-line library tracker course project.
- Checked project behavior using five manual test cases.

**Reject:** “Improved library operations by 40%” or “Led production deployment for 500 users.” The profile does not support those claims.

**Interview prompt**

```text
Help me practice an entry-level CS interview using the synthetic profile.
Ask one question at a time about input validation or my project contribution.
Wait for my answer before giving brief feedback.
Then ask one follow-up question.
Do not pretend this is an actual hiring decision.
```

Role recommendations and career plans are suggestions to check against actual job postings, not promises of employment. No resume formatting or “ATS” claim guarantees selection.

### C. Assemble and peer-test the toolkit (15 minutes)

Students save five reusable prompts with placeholders:

| Prompt | Required placeholders/check |
|---|---|
| Concept tutor | Topic, learner level, example, understanding check |
| Code explainer | Safe snippet, input, trace, no invented execution |
| Debugging helper | Intended behavior, actual behavior, smallest fix |
| Test designer | Behavior contract, edge cases, expected results |
| Study/career helper | Permitted source or verified profile, unsupported-claim constraint |

Peer-test one prompt by changing the topic/input. A reusable prompt should not accidentally depend on facts from an earlier conversation. Include the necessary input again when starting a fresh chat.

## 8. Final prompt challenge — 45 minutes

Follow the [workbook](../activities/Day2-Activities.md).

### Choose one task

- Explain an API to a beginner with an analogy and its limitation.
- Produce a study sheet from the stack/queue note, with a separate answer key.
- Diagnose the toy counting bug and propose discriminating tests.

### Timing

- 5 min: Choose task and write acceptance criteria.
- 10 min: Draft prompt and obtain/inspect an output.
- 10 min: Verify a claim or result and make one targeted revision.
- 5 min: Document final response and remaining limitation.
- 10 min: Share-back and peer review.
- 5 min: Exit ticket.

### Peer-feedback checklist

- Does the prompt match the task and audience?
- Are necessary assumptions and constraints explicit?
- Can the response be checked?
- Did the team actually verify something?
- Are limitations and missing evidence acknowledged?

Focus feedback on usefulness and verification, not prompt length, more roles, paid tool access, or a prettier output.

## 9. Presentation storyboard

These teaching beats match the separate speaking script:

1. Welcome back: generate, then evaluate.
2. What students will create today.
3. A prompt is a task description, not a magic spell.
4. Vague → clearer → checkable.
5. Roles and useful context.
6. Constraints and structured responses.
7. Few-shot examples: patterns, not retraining.
8. Code explanation: inspect a trace.
9. Debugging: intended versus actual.
10. Test cases that reveal a bug.
11. Evidence and targeted refinement.
12. Study using supplied sources.
13. Honest career assistance and interview practice.
14. Build a five-prompt toolkit.
15. Challenge and share-back.
16. Recap and the Day 3 source-grounded project.

## 10. Completion checklist

- [ ] Student completed a before/after prompt record.
- [ ] Student verified at least one technical claim, source claim, or test result.
- [ ] Test worksheet includes expected outputs and an edge case.
- [ ] Toolkit contains five reusable prompts, with necessary inputs/placeholders.
- [ ] Student can explain why roles, examples, and formatting do not guarantee correctness.
- [ ] Student can distinguish generated explanations from actual execution evidence.
- [ ] Student followed institutional AI-use and privacy rules.

**Exit questions**

1. Which missing detail most improved your prompt?
2. What did you verify, and how?
3. What would you do if a targeted follow-up still produced an incorrect answer?

**Optional homework:** Improve one toolkit prompt using a permitted course topic. Bring one output, one verification, and one uncertainty.

**Next:** [Day 3 — CS Course Knowledge Assistant](../projects/Project1-CS-Course-Assistant.md).
