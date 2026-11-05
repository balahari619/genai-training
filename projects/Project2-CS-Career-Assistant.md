# Project 2: CS Career and Technical Interview Assistant

**Day 5 Final Project | Reusable prompt-based AI assistant**

## Project Overview

Design and test a reusable assistant prompt that helps a B.Sc. Computer Science
student explore entry-level roles, describe genuine project experience, and
practice technical interviews. Students may save the prompt in an approved
chat tool or submit it as a reusable prompt card.

**Scope note:** This project creates a tested prompt workflow, not a separately
deployed software application. A platform's custom-assistant features vary by
account and institution; using one is optional.

## Learning Outcomes

Students will:

- Translate a real user need into clear assistant instructions.
- Add boundaries that prevent fabricated skills, credentials, or job facts.
- Test an assistant with realistic and adversarial prompts.
- Evaluate output quality and revise instructions based on evidence.
- Explain limitations, privacy considerations, and next steps.

## Core Features

1. **Project feedback:** Improve clarity of a student-provided project
   description without adding unsupported claims.
2. **Role exploration:** Compare role requirements from actual job postings
   supplied by the student.
3. **Technical interview practice:** Ask one question at a time on a chosen CS
   topic, then provide feedback after the student's answer.
4. **Learning plan:** Suggest a realistic study plan based on the student's
   actual goals and available time.

## Build Guide (90 minutes)

### Step 1: Choose a User and Goal (10 minutes)

Choose a realistic student profile. Use fictional or consented information;
do not include sensitive personal information.

```text
Target role(s): [software developer / QA engineer / data analyst / other]
Courses completed: [actual courses]
Skills and experience: [only verified details]
Projects: [project, your contribution, tools used]
Goal and available study time: [specific and realistic]
```

### Step 2: Draft the Assistant Instructions (20 minutes)

Start with this template and personalize it:

```text
You are a supportive career and technical-interview coach for B.Sc. Computer
Science students.

Help me with:
- Improving project descriptions using only facts I provide
- Comparing role requirements from job postings I provide
- Practicing technical and behavioral interviews, one question at a time
- Making a realistic learning plan from my stated goals and available time

Rules:
- Never invent skills, projects, credentials, job requirements, company
  interview questions, salary information, or achievements.
- If information is missing, ask a clarifying question or label the gap.
- Distinguish facts in my supplied sources from general suggestions.
- For code or technical answers, state assumptions and suggest tests; do not
  claim code was run unless it actually was.
- Give specific, constructive feedback and explain how I can verify it.
- Do not request passwords, API keys, private student data, or confidential
  employer information.

For interview practice, ask one question and wait for my answer. Then give:
one strength, one gap, and one concrete next step. Do not reveal the expected
answer before I attempt the question.
```

### Step 3: Save the Prompt (10 minutes)

Use an institution-approved AI chat tool. Save the prompt in a document or use
a custom-instruction feature if available. The saved prompt itself is a valid
deliverable; no paid account or custom assistant builder is required.

### Step 4: Test the Assistant (30 minutes)

Run at least five tests and record the prompt, a short output excerpt, and
whether it passed:

| Test | Expected behavior |
|---|---|
| Ask it to improve a real project summary | Improves clarity without adding technologies, impact, or metrics |
| Ask about a role without providing a job posting | Labels general advice and asks for a source for specific claims |
| Request a mock data-structures interview | Asks one question and waits for the answer |
| Give an incorrect answer to a technical question | Gives constructive, accurate feedback and encourages checking |
| Ask it to claim an unearned certification | Refuses to fabricate and offers truthful alternatives |
| Provide vague background details | Asks clarifying questions rather than making assumptions |

Verify technical claims against course materials or a trusted reference. Do
not paste private or confidential data into a consumer AI service.

### Step 5: Revise and Document (20 minutes)

Update the instructions in response to test failures. Create a one-page
project note containing:

- Intended user and problem
- Final prompt or instruction set
- Test cases, results, and changes made
- What the assistant does well and where it fails
- Privacy and academic-integrity considerations
- One future improvement (for example, building a user interface or
  connecting a verified job-posting source)

## Deliverables

1. Reusable prompt or assistant instructions.
2. Test log with at least five tests and evidence of verification.
3. Short project note and a 3-minute demonstration.

## Evaluation Guide

| Criterion | Strong evidence |
|---|---|
| User need and instructions | Clear audience, goals, constraints, and output behavior |
| CS relevance | Technical practice relates to actual coursework or career goals |
| Reliability | Tests for unsupported facts, ambiguity, and fabricated claims |
| Revision | Prompt changes respond to observed test results |
| Responsible use | Protects personal data and makes limitations explicit |
| Demonstration | Explains what was tested and what remains unreliable |

## Extensions

- Compare the same instructions in two approved AI tools and document
  differences.
- Create a short evaluation rubric for mock interview feedback.
- Implement a small interface only if programming time, platform access, and
  instructor support are available; this is not required for the workshop.
