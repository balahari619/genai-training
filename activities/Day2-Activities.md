# Day 2 Activity Workbook

**Audience:** B.Sc. CS students

**Use with:** [Day 2 teaching content](../content/Day2-Content.md)

**Participation:** Individual or pair work; approved AI access is optional

## Instructions

Use public/synthetic examples only. Record what you actually checked; do not say code ran if you only read its explanation. If no AI access is available, use the prepared outputs in the teaching content and write the prompt you would send.

## Activity 1 — Improve an unclear prompt

**Starting prompt:** “Teach me recursion.”

Write a revision that specifies:

- What the learner already knows.
- One concrete example.
- What the response must include.
- One way to check understanding.

**Submit:** Original prompt, revised prompt, response/fallback critique, one verification.

**Facilitator check:** A factorial-of-3 example should end at 6, identify a stopping base case, and not claim recursion is always faster.

## Activity 2 — A structured comparison

Ask for a table comparing fixed-size arrays and singly linked lists. Include an assumptions column and distinguish finding an insertion location from inserting at a known location.

**Submit:** Prompt, table, one checked row.

**Facilitator check:** Array indexed access is typically O(1); linked-list indexed access is O(n). Finding a node/position can dominate the cost of an update. A table stating all linked-list insertions/deletions are O(1) needs correction.

## Activity 3 — Give examples

Use the bug-report examples in the teaching content.

Classify:

1. Negative age is accepted.
2. Final price uses the wrong tax percentage.
3. A heading overlaps the menu.
4. The page crashes when Submit is pressed.

**Submit:** Labels and reasons; say what information is missing when necessary.

**Facilitator check:** First three: validation, calculation, display. Fourth is ambiguous; an unsupported classification is weaker than requesting reproduction details.

## Activity 4 — Trace the toy function

```python
def count_even(numbers):
    count = 0
    for index in range(len(numbers) - 1):
        if numbers[index] % 2 == 0:
            count += 1
    return count
```

Input: `[2, 3, 4]`.

| Index visited | Value | Count after iteration |
|---|---|---|
| | | |
| | | |

Answer:

- Actual return:
- Intended count of even values:
- Cause of the mismatch:
- Was this executed or manually traced?

**Facilitator key:** Index 0/value 2/count 1; index 1/value 3/count 1. Actual 1, intended 2. Index 2 is skipped.

## Activity 5 — Design tests before trusting the fix

Write the smallest fix and complete this table:

| Input | Expected corrected result | Actual result, if executed | Why it matters |
|---|---:|---|---|
| `[]` | | | |
| `[2]` | | | |
| `[3]` | | | |
| `[2, 3, 4]` | | | |
| `[-2, 1, 0]` | | | |

**Facilitator key:** Replace `range(len(numbers) - 1)` with `range(len(numbers))`. Expected results: 0, 1, 0, 2, 2.

**Discussion:** Why can `[2, 3]` pass even with the bug? Its skipped final element is odd, so both versions count one even value.

## Activity 6 — Targeted refinement

Critique this deliberately faulty prepared answer:

> Binary search works on any list. For `[2, 5, 8, 11, 14]`, it checks 8, then 14, then 11. It is always O(1).

Write a follow-up that identifies the defects instead of saying “try again.”

**Submit:** Three defects, one revised prompt, corrected claims, verification.

**Facilitator key:** Standard binary search requires sorted data. With inclusive bounds and floor midpoint, the trace checks 8 then 11. Worst-case comparison count on a sorted random-access array is O(log n).

## Activity 7 — Source and career helpers

### Source task

Use the stack/queue note from the teaching content. Ask for a comparison, two questions, and a separate answer key. Then ask when your exam is.

**Facilitator key:** Stack removes B and leaves A; queue removes A and leaves B. Exam date is not provided.

### Career task

Use the synthetic profile in the teaching content to write two resume bullets. Start a mock interview that asks one question and waits for an answer.

**Facilitator key:** Bullets may mention menu handling, input validation, and five manual test cases. Invented internships, user counts, or percentage improvements are not acceptable.

## Activity 8 — Save your five-prompt toolkit

| Prompt | Saved prompt/filename | Input needed | How I will check it |
|---|---|---|---|
| Concept tutor | | | |
| Code explainer | | | |
| Debugging helper | | | |
| Test designer | | | |
| Study/career helper | | | |

Swap one prompt with another pair. Test whether it still works after changing its input and without the original conversation history.

## Final challenge — 45 minutes

Choose **one**, not all three:

1. Explain an API to a beginner in under 100 words using one analogy; state where it breaks down.
2. Create a study sheet using only the stack/queue note, including a trace and separate answer key.
3. Explain the counting bug, propose the smallest fix, and provide tests including one that exposes the original bug.

**Timing:** 5 min criteria, 10 min prompt/output, 10 min verification/revision, 5 min record, 10 min share-back, 5 min exit ticket.

### Submission template

```text
Team/student:
Chosen task:
Acceptance criteria:
Original prompt:
Output or prepared response reviewed:
Mismatch found:
Targeted follow-up:
Final output:
Verification method:
Expected versus actual result (if run):
Remaining limitation:
AI/tool usage disclosure:
```

### Facilitator notes

- API analogy: Accept analogies that describe a defined interface through which software requests functionality/data. Reject “every API needs the internet” or “an API is the database.” An analogy is not the full technical definition.
- Source challenge: Check faithfulness to the note and evidence, not fabricated detail.
- Debugging challenge: Require a discriminating test such as `[2]` or `[2, 3, 4]`.
- Give feedback on clarity, relevance, verification, and honest limitations. Support students without paid tools or programming experience.

### Exit ticket

1. What changed between your original and revised prompt?
2. What evidence did you check?
3. What would you do if the assistant remained wrong?
