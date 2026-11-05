# Day 1: Introduction to Artificial Intelligence & Generative AI

**Duration:** 4 hours  
**Approach:** 20% Concepts + 60% Hands-on + 20% Activities  
**Goal:** Build AI literacy and connect Generative AI to CS study, software development, and everyday use

---

## 🎯 Learning Objectives

By the end of Day 1, students will:
1. Understand the difference between AI, Machine Learning, and Generative AI
2. Know how Generative AI actually works (simplified)
3. Explore available AI tools and understand that features and access vary
4. Understand both capabilities and limitations of GenAI
5. Use AI effectively for CS study while checking its outputs

---

## 📋 Day 1 Schedule

| Time | Topic | Duration | Activity |
|------|-------|----------|----------|
| **09:00 - 09:30** | AI, ML, and Generative AI | 30 min | Concepts + discussion |
| **09:30 - 10:15** | How Generative AI Works | 45 min | Concepts + guided demonstration |
| **10:15 - 10:30** | *Break* | 15 min | - |
| **10:30 - 11:30** | Exploring AI Tools | 60 min | Guided hands-on |
| **11:30 - 12:15** | Beyond Text: Code, Images, Audio & Presentations | 45 min | Guided hands-on |
| **12:15 - 13:00** | Interactive AI Challenge | 45 min | Activity and reflection |

---

## 📖 PART 1: What is Artificial Intelligence? (30 minutes)

### Concept: Defining AI, ML, and GenAI

#### What is Artificial Intelligence (AI)?

**Simple Definition:** AI is a broad field that develops computer systems for tasks such as prediction, language, perception, and decision support. Not every AI system learns from examples; some use rules designed by people.

**Everyday Examples:**
- Netflix recommending movies you might like
- Google Maps predicting traffic
- Your phone's face recognition
- Email spam filters
- YouTube suggestions

**Key Point:** AI systems do not understand in the human sense. Different systems use different methods, and their outputs need context and evaluation.

---

### What is Machine Learning (ML)?

**Definition:** A field of AI in which systems learn patterns from data to make predictions or decisions, rather than relying only on hand-written rules.

**How it works:**
1. Feed computer lots of examples
2. Computer finds patterns in those examples
3. Computer uses patterns to make predictions on new data

**Analogy:** A spam filter can learn patterns from examples of spam and non-spam messages. The analogy is limited: a model does not learn or understand exactly like a person.

---

### What is Generative AI (GenAI)?

**Definition:** AI that generates new content (such as text, images, code, or audio) from learned patterns and the context in a prompt.

**How it differs from many predictive AI systems:**
- A predictive system may classify an email or estimate a value
- A generative system produces content such as text, images, or code

**Examples:**
- General-purpose assistants can draft or explain text and code
- Image-generation tools can create visuals from prompts
- Coding assistants can suggest or explain code when that feature is available

---

### Key Takeaway: AI is Everywhere

```
Predictive or classification AI
├── Email spam filter (classifies emails)
├── Movie recommendation (predicts what you like)
└── Face recognition (identifies people)

Generative AI (Creating New Content)
├── Text-generation assistants (draft text)
├── Image-generation tools (create visuals)
├── Coding assistants (suggest, explain, and edit code)
└── Video-generation tools (create or transform video)
```

---

## 📖 PART 2: How Generative AI Works (45 minutes)

Use the first 15 minutes to explain tokens and generation. Spend the remaining
30 minutes on a guided demonstration and student verification activity.

### Simplified Explanation of LLMs

**LLM = Large Language Model**

An LLM is trained by optimizing model parameters on data. At use time, it generates a sequence of tokens conditioned on the prompt and conversation context. It is not simply searching a complete copy of the internet, and fluency does not guarantee truth.

---

### Understanding Tokens

**Token:** A unit of text processed by a model. A token may be a word, part of a word, or punctuation; tokenization varies by model.

```
Text: "Generative AI can help explain code."

Tokens: The model splits text into tokens; the exact boundaries vary by model.
```

**Why it matters:**
- Tokens are not the same as words
- Context and output limits depend on the model and product
- API pricing and free-tier limits vary; this is not relevant to every chat product

---

### The Training Process

```
Step 1: Data Collection
↓
Training data is prepared; data sources and methods vary by model

Step 2: Learning Patterns
↓
The model adjusts parameters to learn statistical patterns in its training objective

Step 3: Parameter Adjustment
↓
The model can generate text tokens based on the prompt and context

Step 4: Ready to Use
↓
At use time, the model generates a response; a fluent response is not necessarily correct
```

---

### Critical Concept: Hallucinations

**What is a Hallucination?**

When an AI system produces unsupported or incorrect content, sometimes with a confident tone.

**Example (Real):**
```
User: "Give me a Python library method for this task."
AI: It may invent a method, use the wrong API, or omit an important condition.
```

**Why it happens:**
- Fluent output is not proof of correctness
- It can produce plausible but invalid code, citations, or explanations

**Key Takeaway:** Always verify AI's answers, especially for facts, dates, and citations!

---

### Capabilities Depend on the Tool

Do not assume an assistant has web access, file access, current knowledge, or access to your computer; these depend on the product and enabled features. AI can help explain concepts, draft code and tests, and summarize material, but its output still needs source verification, execution, and human review.

---

## 📖 PART 3: Exploring Popular AI Tools (60 minutes)

### Overview of Main AI Tools

| Tool | What It Does | Best For | Cost |
|------|-------------|----------|------|
| **ChatGPT / Gemini / Claude** | General-purpose AI assistants | Explanations, study, drafting, code discussion | Features and access vary |
| **Coding assistants** | IDE-integrated suggestions and explanations | Code completion, refactoring, tests | Features and access vary |
| **Search-grounded assistants** | Responses with web sources | Current research, followed by source checking | Features and access vary |

---

### Hands-On Demo 1: General-Purpose AI Assistant

**Step 1:** Open an institution-approved AI chat assistant. Product access and account requirements vary.

**Step 2:** Try this prompt:

```
Prompt: "Explain how a hash table works to a first-year B.Sc. Computer
Science student. Include one tiny example and distinguish average from
worst-case lookup time."
```

**Expected Output:** A clear explanation that keeps the key CS terms accurate.

**Step 3:** Try a follow-up question:

```
Prompt: "Show a tiny example and tell me one case where the average-case
claim might not hold."
```

**Observation:** Notice whether the assistant uses relevant details from earlier turns in this conversation. Context handling varies by tool.

---

### Hands-On Demo 2: Compare with a Second Approved Assistant

Use another institution-approved assistant if available; otherwise compare two
responses from the same tool with different context.

Try this prompt:

```
Prompt: "I'm a first-year B.Sc. Computer Science student. Explain how a hash
table works, show a small example, compare average and worst-case lookup time,
and identify one common misconception."
```

**Observation:** Notice how it adapts to the student's level and provides examples. Verify technical claims with course material or a small test.

If file analysis is available and approved, try an instructor-provided PDF:

```
Prompt: "Summarize the main points from this document in bullet points."
```

---

### Hands-On Demo 3: Comparing Outputs

**Use the same prompt on 2-3 different AI tools:**

```
Common Prompt: "Explain this short Python function, identify edge cases, and
suggest three tests. Do not rewrite it unless you explain the changes."
```

**Comparison Task:**
- Which tool explained the code most clearly?
- Did any tool invent behavior or miss an edge case?
- Which suggestions could be verified by running tests?

**Key Learning:** Different AI tools have different strengths!

---

## 📖 PART 4: Beyond Text - Images, Code, Audio & Presentations (45 minutes)

### Multimodal and Coding Tools

Products and access change; demonstrate tools available through college-approved accounts.

**Live Demo: Create a Concept Diagram**

```
Prompt: "Create a clean diagram-style illustration of a request moving
through a web application: browser, server, database, and response. Use
distinct labels and no extra text."
```

Discuss that generated diagrams may contain incorrect labels or relationships;
students should check and correct the technical content.

**Coding Assistant Demonstration:** Ask an approved assistant to explain a
short code snippet and suggest tests. Review the suggestions and run code only
in an approved environment.

---

### AI for Presentations

Students can ask an approved presentation tool for an outline on a CS topic.
Review and verify technical claims before using the slides.

---

### AI for Audio & Video

**Optional Demo: Audio or Video Generation**

If an approved tool supports audio summaries, demonstrate it using a permitted
course handout. Feature availability varies; do not make this a required
student account or activity.

---

### Limitations of Generated Media

⚠️ **Things to Know:**

1. Generated media can contain errors or misleading details.
2. Consent and attribution matter when creating or sharing synthetic media.
3. Check current provider terms and college policy before publishing outputs.

---

## 🎯 PART 5: Interactive AI Challenge (45 minutes)

### Challenge 1: Solving a Study Problem (15 min)

**Scenario:** You are studying a CS concept such as recursion, hashing, or
database normalization and need another explanation.

**Task:**
1. Use an approved AI assistant
2. Write a prompt asking it to explain the selected CS concept
3. Screenshot the response
4. Note: Is it helpful? What's missing?

**Sample Better Prompt:**
```
"Explain [CS concept] to a first-year B.Sc. Computer Science student. Include:
- A precise definition and a beginner-friendly analogy
- One small worked example
- One misconception or edge case
- Two questions I can use to check my understanding
Do not invent course-specific facts; tell me what I should verify."
```

---

### Challenge 2: Creating Professional Content (15 min)

**Scenario:** You need to write a LinkedIn profile summary to attract recruiters.

**Task:**
1. In ChatGPT, paste this:
```
"I'm a final-year B.Sc. Computer Science student interested in software
development. Use only these real skills and project details: [add yours].
Draft a 3-4 line LinkedIn summary. Do not invent skills, awards, or experience."
```

2. Compare the AI's output to a weak one
3. Discuss: What makes the AI output professional?

---

### Challenge 3: The Hallucination Check (15 min)

**Scenario:** You need to verify if AI is making things up.

**Task:**
1. Ask ChatGPT: "What is the title of the third chapter in 'The God of Small Things' by Arundhati Roy?"
2. Ask: "Who won the Filmfare Award for Best Actor in 2023?"
3. For each answer, verify on Google
4. Discuss: Did AI hallucinate?

---

## 📝 Key Takeaways for Day 1

### ✅ What Students Should Understand

1. **AI vs ML vs GenAI:** Clear differences and uses
2. **How GenAI Works:** It's pattern prediction, not magic
3. **Popular Tools:** ChatGPT, Gemini, Claude, and their differences
4. **GenAI Capabilities:** What it's great at
5. **GenAI Limitations:** Hallucinations, outdated data, biases
6. **Practical Uses:** Real tasks for students

### 🚫 Common Misconceptions to Address

- ❌ "AI can do anything" → ✅ "AI is powerful but has limitations"
- ❌ "AI always tells the truth" → ✅ "AI can confidently produce incorrect or unsupported output"
- ❌ "AI understands language" → ✅ "AI recognizes patterns in text"
- ❌ "AI is only for tech experts" → ✅ "Anyone can use AI tools"

---

## 📊 Day 1 Assessment

### Quick Self-Check Questions

1. What's the difference between AI and Generative AI?
2. What does "hallucination" mean in the context of AI?
3. Name three popular AI tools you tried today.
4. What's a limitation of AI you discovered?
5. How could you use AI for one of your current assignments?

### Homework (Optional)

- Explore one more AI tool not covered in class
- Use an approved AI tool to help with a real academic task, then verify its output
- Take notes on what worked well and what didn't

---

## 🎤 Facilitator Tips for Day 1

1. **Start with familiarity:** Ask what AI tools students have tried; avoid assuming experience
2. **Real examples:** Use local, relatable examples from their college life
3. **Hands-on matters:** Let students try tools themselves, not just watch
4. **Encourage questions:** Create a safe space for curiosity
5. **Manage expectations:** Be clear about what AI can't do
6. **End on excitement:** Leave them wanting to learn more

---

## 🔗 Tool Access

Use the current provider links and access guidance in
`resources/AI-Tools-Comparison.md`. Check college approval and feature
availability before the demonstration.

---

**Next:** Day 2 - Prompt Engineering & AI Productivity
