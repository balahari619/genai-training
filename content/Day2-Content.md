# Day 2: Prompt Engineering & AI Productivity

**Duration:** 4 hours  
**Focus:** Effective prompts for CS study, code work, technical communication, and careers  
**Goal:** Students learn to direct AI, verify outputs, and use it responsibly in computer science work

---

## 📋 Day 2 Schedule

| Time | Topic | Duration |
|------|-------|----------|
| **09:00 - 09:30** | Prompting Foundations | 30 min |
| **09:30 - 10:45** | Guided Prompting Workshop | 75 min |
| **10:45 - 11:00** | *Break* | 15 min |
| **11:00 - 11:30** | Checkable Explanations & Iteration | 30 min |
| **11:30 - 12:15** | AI for CS Study and Careers | 45 min |
| **12:15 - 13:00** | Prompt Challenge | 45 min |

---

## 🎯 Learning Outcomes

By end of Day 2:
- ✅ Write clear, effective prompts
- ✅ Use context, examples, constraints, structured outputs, and iterative refinement
- ✅ Use AI for academic tasks (research, writing, learning)
- ✅ Use AI to explain, debug, document, and test code without outsourcing understanding
- ✅ Use AI for CS career tasks (resume, portfolio, technical interview prep)
- ✅ Understand and apply prompt iteration

---

## 📚 PART 1: Introduction to Prompt Engineering (30 min)

### What Makes a Prompt Good?

**The 5 Elements (Review from Guide):**
1. **Role** - Who should AI be?
2. **Context** - What's the situation?
3. **Instructions** - What exactly do you want?
4. **Examples** - Show what you want
5. **Output Format** - How should it look?

### Demonstration: Progressive Prompt Improvement

**Iteration 1 (Vague):**
```
Prompt: "Write a resume"
Output: Generic template, not useful
```

**Iteration 2 (Better):**
```
Prompt: "Write a resume for a B.Sc. Computer Science student"
Output: More specific, but still generic
```

**Iteration 3 (Strong):**
```
Prompt: "Act as a career coach. Draft a one-page resume for [student name],
a final-year B.Sc. Computer Science student applying for a software
development internship. Use only the education, skills, coursework, and
projects I provide below. Do not invent internships, awards, metrics, or
technical expertise.

Student details:
- Programming languages: [actual experience]
- Relevant coursework: [actual courses]
- Projects: [name, contribution, tools, verified result]
- Activities or experience: [actual details]

Format: Plain, readable headings and concise bullets. Ask questions if
important details are missing."

Output: Specific, targeted, actually useful
```

### Why This Matters

- **Vague prompts** = Generic, unuseful outputs
- **Specific prompts** = Customized, valuable outputs
- **Time saved** = Better output on first try instead of iterations

---

## 🛠️ PART 2: Prompting Techniques Workshop (75 min)

### Technique 1: Role-Based Prompting (15 min)

**The Concept:** Assign AI a persona to get better responses

**Workshop Activity:**

Same question, different roles:

```
Question: "What should I do to prepare for a job interview?"

WITHOUT ROLE:
"Study company, practice common questions, wear professional clothes, be on time"
(Generic, not personalized)

WITH ROLE - As a Recruiter:
"As a recruiter, I'll tell you what impresses us: Research our company's recent 
projects and mission... Ask us thoughtful questions about growth opportunities... 
Prepare specific examples of your achievements... Most candidates fail by not 
demonstrating how they add value..."
(More insightful and experienced)

WITH ROLE - As a Mentor:
"As your mentor, I recommend: First, calm your nerves with deep breathing. 
Research 3 specific things about the company. Prepare stories that show your 
problem-solving... Remember, they're assessing if you're someone they'd want 
to work with daily..."
(More supportive and holistic)
```

**Student Exercise (10 min):**

Same question to different roles:
```
Question: "How can I improve my writing?"

Prompts:
1. "Act as an English teacher..."
2. "Act as a published author..."
3. "Act as a business communication expert..."
4. "Act as a journalist..."

Compare outputs - which role gave the most useful advice for YOUR needs?
```

---

### Technique 2: Few-Shot Prompting (15 min)

**The Concept:** Show examples of what you want, not just describe it

**Demonstration:**

```
BEFORE (Description only):
"Create a catchy LinkedIn headline for a student"

Output: "B.Sc. Computer Science | Aspiring Software Developer | Building Projects"
(Okay, but generic)

AFTER (With examples):
"Create a catchy LinkedIn headline for a student. 
Here's the style I like:

Example 1: "B.Sc. Computer Science | Exploring Web Development | Building Projects"
Example 2: "Final-Year CS Student | Data Structures & Python | Open to Internships"
Example 3: "Soon-to-Graduate Psychologist | Behavioral Research Curiosity | Let's Connect"

Now create one for a final-year B.Sc. Computer Science student interested in
backend development, using only real skills and project experience."

Output: "Final-Year CS Student | Exploring Backend Development | Learning by Building"
(Much better, matches your style preferences)
```

**Student Exercise (10 min):**
- Students share a type of content they write often
- Instructor creates one example
- Student creates 2 examples of their preferred style
- Student asks AI using few-shot prompting
- Compare: Generic AI output vs AI output trained on examples

---

### Technique 3: Requesting Useful, Checkable Explanations (15 min)

**The Concept:** Ask for a concise rationale, explicit assumptions, intermediate results where useful, and checks you can verify. A generated explanation is not proof that the answer is correct.

**Demonstration:**

```
Prompt: "Trace this short function on the input [example]. Show the values
of the variables after each loop iteration, state the expected output, and
list one edge case I should test. If the code is ambiguous, ask me first."
```

**Why It Works:**
- A clear, checkable explanation can help you inspect an answer
- Verify code by running tests and checking behavior yourself

**Student Exercise (10 min):**
Choose a short code example. Compare "What does this return?" with a prompt
asking for a trace table, assumptions, and an edge-case test. Check both
answers by running the code.

---

### Technique 4: Structured Output Prompting (15 min)

**The Concept:** Ask for output in a specific structure

**Demonstration:**

```
WITHOUT STRUCTURE:
Q: "Compare arrays and linked lists for a CS exam"
A: Long paragraph of text, hard to study from

WITH STRUCTURE:
Q: "Compare socialism and capitalism using this table format:

| Aspect | Array | Linked List |
|--------|-----------|-----------|
| Definition | | |
| Who owns property | | |
| How prices are set | | |
| Real-world examples | | |
| Pros | | |
| Cons | |"

Output: Perfectly formatted table, easy to study from
```

**Student Exercise (5 min):**
- Each student prepares a study topic
- Sends prompt WITHOUT structure
- Sends same prompt WITH structure
- Compares how much easier structure makes studying

---

## 📚 PART 3: Advanced Prompting Strategies (30 min)

### Strategy 1: Iterative Refinement

**The Process:**

```
Attempt 1: Write initial prompt
↓
Evaluate: Is the output good?
↓
If NO → Ask follow-up question
↓
Attempt 2: Refine based on feedback
↓
Evaluate: Better?
↓
Continue until satisfied
```

**Live Example:**

```
Attempt 1:
Q: "Help me study for my data structures exam"
A: Generic study tips

Follow-up 1:
Q: "The exam is specifically on stacks, queues, and linked lists. Give me
practice questions that require tracing operations."
A: Better - more specific

Follow-up 2:
Q: "Make the questions progressively harder (3 easy, 3 medium, 3 hard).
Put answers and concise explanations in a separate section."
A: Excellent - exactly what I need
```

### Strategy 2: Constraint-Based Prompting

**The Concept:** Add limitations to force creative solutions

```
Q: "Explain recursion"
Output: Long, generic summary

Q: "Explain recursion in about 100 words, with a base case, recursive case,
and tiny example. Keep the definition technically accurate."
Output: Concise explanation that preserves the core CS concepts
```

### Strategy 3: Perspective Shifting

**The Concept:** Ask AI to view from different angles

```
Q: "Should I focus next on web development, data engineering, or software
testing, given my current courses and project experience?"

Different perspectives:
1. As a career counselor: Focus on job prospects
2. As a computer scientist: Focus on technical value
3. As a software team lead: Focus on practical project experience
4. As a lazy student: Focus on time investment vs payoff
5. As your friend: Focus on your happiness

This gives 5 different viewpoints to make a good decision
```

---

## 💼 PART 4: AI for CS Study & Career Preparation (45 min)

### Use Case 1: Research & Learning

**Task:** Understand a complex topic quickly

**Prompt Template:**
```
"I need to understand [topic] for [purpose: exam/project/career].

My current level: [What you know]
Time available: [30 minutes/2 hours/1 day]
Learning style: [Visual/textual/examples/practice problems]

Create a learning plan that includes:
- Key concepts to master
- Simplified explanations
- Real-world examples
- Practice questions
- Resources for deeper learning"
```

**Real Example:**
```
"I need to understand blockchain technology for an IT seminar presentation.

My current level: I know what Bitcoin is, but not the underlying technology
Time available: 4 hours
Learning style: I learn best with analogies and real examples

Create a 4-hour self-study plan including:
- 5 main concepts (explained simply)
- Analogy for how blockchain works
- 3 real-world applications (besides cryptocurrency)
- Key terminology
- How to explain it to non-technical people
- 5 interview questions someone might ask"
```

### Use Case 2: Assignment Help

**Task:** Improve your academic work

**Prompt Template:**
```
"I'm working on [assignment type] about [topic].

My current draft: [Paste your work]

Please review and:
- Point out strengths
- Identify weaknesses
- Suggest improvements
- Provide one example of how to improve a specific section
- Rate the overall quality and how to improve further"
```

### Use Case 3: Learning with Code (AI as a Pair-Programmer)

Use AI to explain code, suggest tests, and diagnose errors; do not treat generated code as correct until you understand and run it.

```
I'm learning [language/topic]. Here is the smallest code example that shows
the issue:
[paste code you are allowed to share]

Expected behavior: [what should happen]
Actual behavior or error: [what happens]

First explain the likely cause without changing the code. Then suggest the
smallest fix, explain each changed line, and propose 3 tests including one
edge case. Do not claim you ran the code.
```

**Class check:** Run the suggested code in an approved local environment or
Colab. Compare actual results with the AI's explanation. Never paste passwords,
API keys, private student data, or institution-owned code into an unapproved tool.

### Use Case 4: Resume Building

**Task:** Create a strong resume

**Prompt Template:**
```
"Create a resume for me to apply for [job title].

About me:
- Current education: [Program, year, college]
- Skills: [List your skills]
- Experience: [Internships, projects, work]
- Achievements: [Grades, awards, leadership]
- Target company: [Company type/name]

Requirements:
- ATS-friendly format (can be parsed by resume scanners)
- Highlight relevant skills for this role
- Use action verbs
- Quantify achievements where possible
- One page
- Professional tone"
```

### Use Case 5: Interview Preparation

**Task:** Prepare for job interviews

**Prompt Template:**
```
"Conduct a mock interview with me for the position of [Job Title] at [Company Type].

About me: [Brief background, skills, interests]

Interview style: [Behavioral/Technical/Mixed]

For each question:
- Ask the question
- Wait for my response
- Provide constructive feedback
- Suggest a better answer if needed

At the end, give overall feedback and top 3 areas for improvement."
```

### Use Case 6: Content Creation

**Task:** Create engaging study/career content

**Prompt Template:**
```
"Create [content type] about [topic] for [platform].

Audience: [Who should understand this]
Goal: [Why are you creating this]
Tone: [Professional/casual/inspiring]
Format: [Specific requirements]

Requirements:
- [Specific element 1]
- [Specific element 2]
- Include [type of media if needed]"
```

---

## 🏆 PART 5: Prompt Engineering Competition (45 min)

### Competition Structure

**Challenge 1: Emoji Challenge (15 min)**

Goal: Make a technical explanation clear to a non-technical audience

```
Prompt: "Explain what an API does to a non-technical college student in
under 100 words. Use one everyday analogy, then state where the analogy
stops being accurate."

Winning answer would be creative and actually understandable
```

**Challenge 2: The Bad Prompt Challenge (15 min)**

Goal: Take the worst prompt and make it the best

Facilitator gives a vague prompt like:
"Tell me about stuff"

Students transform it into:
"Act as [role]. Create [specific output] for [specific audience] about [specific topic].
Requirements: [specific needs]"

**Challenge 3: Real-World Scenario (15 min)**

Scenario: "You have an exam on data structures. Create a prompt that asks for
a study guide with definitions, traced examples, practice questions, and a
separate answer key. Ask the AI to flag anything not supported by your notes."

Judging Criteria:
- Clarity and specificity
- Would this actually help you study?
- Covers all important elements

---

## 📝 Key Takeaways for Day 2

### ✅ Prompt Engineering Principles

1. **Specificity:** More details = better output
2. **Role:** AI responds better with a persona
3. **Structure:** Specify format for usable output
4. **Examples:** Show what you want, not just describe
5. **Iteration:** Refine based on first response

### 🎯 Real Applications for Students

- Research and learning
- Code explanation, debugging, test design, and technical documentation
- Assignment improvement
- Resume and cover letter writing
- Interview preparation
- Content creation for presentations

### 💡 Common Mistakes to Avoid

❌ Being vague about what you want  
❌ Not providing enough context  
❌ Asking multiple questions at once  
❌ Trusting AI answers without verification  
❌ Not iterating to improve responses  

---

## 📊 Self-Assessment: Prompt Quality Rubric

Rate your prompts:

| Aspect | Poor | Good | Excellent |
|--------|------|------|-----------|
| **Clarity** | Vague, confusing | Clear intention | Crystal clear, specific |
| **Role/Context** | Missing | Mentioned | Detailed and relevant |
| **Format** | Not specified | Partially specified | Fully detailed |
| **Examples** | None | One | Multiple |
| **Actionability** | Generic | Relevant | Immediately useful |

Aim for "Excellent" on all fronts!

---

## 🎤 Facilitator Tips for Day 2

1. **Live Demonstrations:** Show bad → good prompts in real-time
2. **Pair Work:** Have students work together on prompt refinement
3. **Share Wins:** Celebrate great prompts from students
4. **Competition Energy:** Make the competition fun and supportive
5. **Real Stakes:** Use real assignments they need help with
6. **Iterative:** Show multiple iterations of the same prompt

---

**Next:** Day 3 - Build and evaluate a document-grounded CS course assistant
