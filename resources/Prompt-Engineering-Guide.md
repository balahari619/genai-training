# Complete Prompt Engineering Guide for Students

**Level:** Beginner to Intermediate | For B.Sc. Computer Science students  
**Purpose:** Write clear prompts, evaluate outputs, and use AI responsibly for CS learning and projects

---

## 🎯 What is Prompt Engineering?

**Simple Definition:** Prompting means giving an AI system clear instructions and context, then checking and refining its response. A better prompt can improve usefulness, but it cannot guarantee correctness.

### The Problem
```
Bad Prompt: "Write an essay"
↓
Output: Generic, generic, 500 words of nothing useful

Good Prompt: "Write a 500-word essay on climate change for a high school student. 
Include causes, effects, and 3 actionable solutions. Use simple language."
↓
Output: Specific, structured, actually useful
```

---

## 🔑 The 5 Core Elements of a Great Prompt

### 1. **Role** - Who Should the AI Be?

**Example:**
```
❌ Vague: "Explain recursion"

✅ Clearer: "Explain recursion to a first-year B.Sc. Computer Science student.
Use a simple example and define the key terms."

✅ More specific: "Explain recursion to a first-year B.Sc. Computer Science
student who knows loops but is new to recursive functions. Use a short
factorial example, trace the calls, and mention one common mistake."
```

**Why It Matters:**
- Gives AI context for the tone and depth
- A role can help set tone and viewpoint, but it does not make the AI a qualified expert
- Example roles: programming tutor, code reviewer, technical interviewer, study coach

**Templates:**
```
"Act as a [profession/role]..."
"You are a [specific type of expert]..."
"Imagine you're [specific person]..."
```

---

### 2. **Context** - What's the Situation?

**Example:**
```
❌ Bad: "Write a resume"

✅ Good: "Write a one-page resume for a B.Sc. Computer Science graduate
applying for an entry-level software role. Use only the experience I provide."

✅ Better: "Draft a resume for Priya, a final-year B.Sc. Computer Science
student applying for a software internship. Use only the coursework, projects,
and skills she provides. Do not invent experience or metrics; ask questions
when details are missing."
```

**Why It Matters:**
- AI tailors output to specific situations
- More context = more relevant response
- Helps AI avoid generic outputs

**Key Context to Include:**
- Who is it for?
- What's the goal?
- Any constraints? (length, format, audience)
- What's the background?

---

### 3. **Instructions** - What Exactly Do You Want?

**Example:**
```
❌ Bad: "Create a presentation"

✅ Good: "Create a 5-slide presentation outline on renewable energy."

✅ Better: "Create a 5-slide presentation outline on renewable energy. 
For each slide, include:
- Slide title
- 3-4 main bullet points
- 1 supporting fact or statistic
- Tone: Professional but accessible to non-experts"
```

**Why It Matters:**
- Removes ambiguity
- Gives AI clear direction
- Clear instructions make the requested result easier to check; the output may still miss requirements

**Instruction Keywords:**
- List / Create / Explain / Summarize / Compare
- Break into [number] parts
- Include / Exclude / Add / Remove
- Format as [type]: bullets, table, steps, etc.

---

### 4. **Examples** - Show What You Want (Few-Shot Prompting)

**Example:**
```
❌ Bad: "Format this code like my example"

✅ Good: "Format this Python code like the example. Keep the same indentation
and naming style."

✅ Better: "Use the examples to infer the formatting style, not the program
logic:

Example input: `def add(a,b):return a+b`
Example output: `def add(a, b):\n    return a + b`

Now format this without changing its behavior:
`[paste a short code sample]`"
```

**Why It Matters:**
- Shows the AI the style or format you want
- Especially helpful for specialized outputs
- Dramatically improves consistency

**When to Use Examples:**
- Specific formatting required
- Tone is important
- Output needs to match a particular style

---

### 5. **Output Format** - How Should the Answer Look?

**Example:**
```
❌ Vague: "Explain arrays"

✅ Clearer: "Explain arrays in programming."

✅ More specific: "Explain arrays to a first-year CS student.
Format your response as:
- A one-sentence definition
- A small code example in pseudocode
- A trace showing the index and value for each element
- One common off-by-one error
- Two quick practice questions"
```

**Why It Matters:**
- A requested structure makes the response easier to scan and evaluate
- Saves time reformatting
- Makes content more usable

**Common Format Requests:**
```
- Bullet points
- Numbered list
- Table with [columns]
- 3 paragraphs
- Short form (under 100 words)
- Long form (detailed explanation)
- FAQ format
- Step-by-step guide
- Pros and cons format
```

---

## 📝 A Useful Prompt Template

```
Act as a [ROLE].

Context: [SITUATION & WHO IT'S FOR]

Task: [WHAT YOU WANT]

Requirements/Instructions:
- Requirement 1
- Requirement 2
- Requirement 3

Format: [HOW IT SHOULD LOOK]

Tone: [PROFESSIONAL/CASUAL/CREATIVE/etc]

[Optional: Include an example]
```

---

## 🎓 Real Student Examples

### Example 1: Writing an Email

**Bad Prompt:**
```
"Write an email"
```

**Good Prompt:**
```
Act as a professional communication expert.

Context: I'm a final-year B.Sc. Computer Science student applying for a software internship.

Task: Write a concise, professional email to the placement coordinator asking
about software internship opportunities.

Requirements:
- Professional tone
- 150-200 words
- Include: my interest in software development and project experience I provide; do not invent qualifications
- Proper email format with subject line

Format:
Subject: [Your subject here]
[Email body]
```

---

### Example 2: Summarizing a Textbook Chapter

**Bad Prompt:**
```
"Summarize this PDF"
```

**Good Prompt:**
```
Act as a study guide creator for college students.

Context: This is an instructor-provided chapter from a data structures course.
The student needs to study this material for an exam.

Task: Create a comprehensive study guide from this document.

Requirements:
- Extract 5-7 main concepts
- For each concept: definition + real-world example
- Create 5 practice exam questions
- Include key terms to memorize
- Highlight what's most important

Format:
## Main Concepts
1. [Concept name]
   - Definition: 
   - Example:

## Practice Questions
1. [Question 1]
```

---

### Example 3: Creating Presentation Content

**Bad Prompt:**
```
"Create a presentation on AI"
```

**Good Prompt:**
```
Act as a presentation designer for college students.

Context: I'm giving a 15-minute presentation to my non-technical classmates 
about Artificial Intelligence.

Task: Create a detailed 6-slide presentation outline on "How AI Works."

Requirements:
- Beginner-friendly language (avoid technical jargon)
- Each slide should have a clear title and 3-4 main points
- Include at least one relatable analogy or comparison
- Add statistics or facts where relevant
- End with "What's Next for AI" to generate discussion

Format:

Slide 1: Title Slide
[Title and subtitle]

Slide 2: [Topic]
Main Points:
- Point 1
- Point 2
- Point 3

Example/Visual idea: [What visual would help here?]
```

---

### Example 4: Preparing for an Interview

**Bad Prompt:**
```
"Generate interview questions"
```

**Good Prompt:**
```
Act as an interviewer conducting an entry-level software internship interview.

Context: I'm a B.Sc. Computer Science student applying for a software
internship. My actual skills, projects, and coursework are: [provide details].

Task: Conduct a mock interview with me. Ask one question at a time about
programming fundamentals, data structures, and my projects. Wait for my answer
before giving feedback.

Requirements:
- Ask 5-7 questions typical for this role
- Questions should assess: technical knowledge, problem-solving, 
communication, and enthusiasm
- Wait for my answer after each question
- Provide feedback on my response
- At the end, give overall feedback and tips for improvement

Tone: Professional but encouraging
```

---

## 🔄 The Iterative Process: Refining Your Prompts

### Iteration Cycle

**Step 1: Ask Initial Prompt**
```
"Explain blockchain"
```

**Step 2: Evaluate Response**
- Is it too technical? Too simple?
- Does it answer what I needed?
- What's missing?

**Step 3: Refine Prompt**
```
"Explain blockchain in a way that a 15-year-old can understand. 
Include what it's used for and why it's important. 
Use an analogy to make it clearer."
```

**Step 4: Get Better Response**
```
Check whether the revision is more understandable and relevant; verify any factual claims.
```

**Step 5: Continue Refining**
If still not perfect, ask follow-up questions:
```
"Give me a real-world example where blockchain is used in India."
"Explain the security benefits in simpler terms."
"What are the main limitations?"
```

---

## 🚫 Common Prompt Mistakes to Avoid

### Mistake 1: Being Too Vague
```
❌ "Write about science"
✅ "Write a 500-word article on how vaccines work, 
   for a general audience with no medical background"
```

### Mistake 2: Forgetting Context
```
❌ "Create a resume"
✅ "Help me describe this CS project for an internship resume using only the
   contribution, tools, and results I provide"
```

### Mistake 3: Asking Multiple Questions at Once
```
❌ "Tell me about AI, ML, and deep learning and their differences 
   and real-world applications and career opportunities"
✅ (Ask separately or use clear structure:)
   "Compare AI, ML, and deep learning. For each, explain:
   - Definition
   - Real-world example
   - Career opportunity"
```

### Mistake 4: Not Specifying Length or Format
```
❌ "Summarize this document"
✅ "Summarize this 20-page document in 5 bullet points. 
   Focus on the main findings and conclusions."
```

### Mistake 5: Expecting Hallucinations to Be Facts
```
❌ Ask AI a very specific factual question and trust the answer
✅ Ask AI the question, then verify the answer on Google
```

---

## 💡 Advanced Prompting Techniques

### 1. Ask for Checkable Explanations

Ask for a concise rationale, assumptions, a trace table, or a test case you
can verify. A generated explanation can be incomplete or incorrect; it does
not prove that an answer is correct.

```
Prompt: "Trace this function on the input [example]. Show the variable values
after each iteration, state the output, and suggest one edge-case test.
Do not claim to have run the code."
```

---

### 2. Few-Shot Prompting

**Problem:** AI might guess the style you want

**Solution:** Provide 2-3 examples

```
Prompt: "Write brief code comments in this style:

Example input: `items.sort()`
Example comment: `# Sort items in place`

Example input: `total += price`
Example comment: `# Add the current price to the running total`

Now write one concise comment for each line in this short snippet:
`[paste a non-sensitive code sample]`

Do not change the code."
```

---

### 3. Role-Based Prompting with Expertise

```
Prompt: "For a class discussion, outline ethical risks to consider when an
organization uses AI to screen job applications. Include possible bias,
privacy, accessibility, and human-oversight questions. Do not present this as
legal advice; list points that should be verified with appropriate sources."
```

---

### 4. Structured Output Prompting

```
Prompt: "Create a study guide with this exact structure:

## Key Concepts (bullet list)
## Definitions (terms + 1-line definition)
## Connections (how concepts relate)
## Common Mistakes (what students get wrong)
## Practice Problems (3 example problems)
## Resources (where to learn more)

Topic: Photosynthesis"
```

---

## 📊 Prompt Quality Checklist

Before you send a prompt, check:

- [ ] Does it have a clear role/persona?
- [ ] Is context provided (who it's for, why)?
- [ ] Are instructions specific and clear?
- [ ] Is the desired format explained?
- [ ] Is the length/scope defined?
- [ ] Have I provided examples if needed?
- [ ] Is the tone specified?
- [ ] Would someone else understand what I'm asking?

---

## 🎯 Quick Prompt Templates by Task

### For Writing
```
Act as [professional type]. Write a [document type] for [audience] about [topic].
Requirements:
- Tone: [professional/casual/creative]
- Length: [word count]
- Include: [specific elements]
Format: [bullets/paragraphs/sections]
```

### For Learning
```
I'm learning about [topic]. Explain it as a [profession] would explain it 
to someone with [my level of knowledge].
Include:
- [Specific aspect 1]
- [Specific aspect 2]
Example: [type of example]
```

### For Problem-Solving
```
I need to solve [problem]. Here's my situation: [context].
Requirements:
- Consider: [constraints]
- Prioritize: [what matters most]
- Provide: [number] solutions
For each solution:
- Pros and cons
- Implementation steps
- Challenges
```

### For Research
```
Research and summarize [topic] for [specific purpose].
Focus on:
- [Key area 1]
- [Key area 2]
- [Key area 3]
Sources should be: [credible/academic/recent]
Format: [how to present]
Include verifiable sources where available; do not invent citations or links.
```

---

## ✨ Practice Exercise: Improve These Prompts

### Exercise 1
**Original:** "What should I do after college?"
**Your Challenge:** Make this prompt 10x better
**Hint:** Add role, context, specific requirements

---

### Exercise 2
**Original:** "Explain recursion"
**Your Challenge:** Make it specific for studying
**Hint:** Add audience, format, and what specifically you need

---

### Exercise 3
**Original:** "Write a project proposal"
**Your Challenge:** Make it detailed and actionable
**Hint:** Add who it's for, what the project is, and requirements

---

## 🔗 Resources

- Provider documentation for the AI tool you use (features and guidance change)
- College library and instructor-approved learning resources
- Community: r/ChatGPT for prompt sharing

---

**Next:** Day 2 Content for more advanced prompting techniques
