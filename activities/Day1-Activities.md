# Day 1: Hands-On Activities & Exercises

**Duration:** 45-minute activity block, with short exercises also embedded in the guided hands-on sessions  
**Objective:** Practice using AI tools for B.Sc. Computer Science learning and project work

---

## 🎯 Activity Overview

| Activity | Time | Tools | Outcome |
|----------|------|-------|---------|
| Activity 1A: Email Writing | 15 min | ChatGPT | Professional email |
| Activity 1B: Study Material Summary | 15 min | Gemini + PDF | Summary notes |
| Activity 2: Concept Explanation | 10 min | ChatGPT | Simplified learning |
| Activity 3: Translation & Localization | 10 min | Claude | Tamil translation |
| Activity 4: Content Creation | 10 min | ChatGPT/Gemini | Social media post |
| Activity 5: Idea Generation | 10 min | ChatGPT | Creative ideas |
| Challenge: Hallucination Detection | 15 min | ChatGPT + Verification | Critical thinking |

**Total Activities: 85 minutes (fits within 60-min hands-on block + 45-min challenge block)**

---

## 📝 ACTIVITY 1A: Professional Email Writing (15 minutes)

### Scenario
You need to email your college's placement coordinator asking about internship opportunities.

### Activity Steps

**Step 1: Write a Bad Prompt (3 min)**
```
Bad Prompt: "Write an email"
```

Ask ChatGPT this and observe the generic, poor output.

**Step 2: Write a Good Prompt (3 min)**
```
Good Prompt:
"Act as a professional communication coach. I'm a final-year B.Sc. Computer
Science student seeking a software development internship. Draft a concise,
polite email to the placement coordinator. Mention my interest in software
development and the projects and skills I provide below. Do not invent
experience or qualifications. Use a subject line and keep the email under
180 words. Ask me for missing details rather than making them up."
```

**Step 3: Compare Outputs (5 min)**
- Copy both responses
- Highlight differences
- Discuss: What made the second prompt better?

**Step 4: Student Practice (4 min)**
Each student writes their own improved prompt for an email they actually need to send.

---

### Expected Output Example

```
Subject: Inquiry About Software Internship Opportunities

Dear [Coordinator Name],

I am a final-year B.Sc. Computer Science student interested in software
development internships. My relevant coursework and project experience include
[add accurate details]. I would appreciate information about current
opportunities and the application process.

Thank you for your time. I look forward to hearing from you.

Best regards,
[Student Name]
[Contact Information]
```

### Reflection Questions
1. How is this different from the basic email?
2. What specific information made it professional?
3. How could you further improve this prompt?

---

## 📚 ACTIVITY 1B: Summarizing Study Materials (15 minutes)

### Scenario
You have a chapter on algorithms, databases, or computer networks to study. You need useful notes without losing important definitions or conditions.

### Activity Steps

**Step 1: Choose a Document**
- Use a sample CS course PDF (algorithms, databases, networks, or operating systems)
- OR have students bring a real assignment PDF

**Step 2: Upload to Google Gemini**
```
How to upload:
1. Go to gemini.google.com
2. Click "Attach file" (+ icon)
3. Select your PDF
4. Wait for upload
```

**Step 3: Ask for Summary**
```
Prompt: "Using only the uploaded chapter, summarize its main ideas in 5-7
bullets. Preserve technical terms and definitions. Cite the section or page
for each key claim when available, and flag anything the source does not say."
```

**Step 4: Compare Summaries**
- AI's summary vs your initial understanding
- Which details did AI capture?
- Which important points might AI miss?

**Step 5: Follow-up Questions**
```
Prompt 1: "Explain the first concept in this document with an example."
Prompt 2: "What are the key takeaways for an exam?"
Prompt 3: "Create 3 practice questions based on this material."
```

---

### Expected Output Example

**Document:** Chapter on "Database Normalization"

**AI Summary:**
- Normalization organizes relational tables to reduce avoidable duplication
- Functional dependencies describe relationships between attributes
- First, second, and third normal forms impose progressively stronger constraints
- A decomposition should preserve needed information and, where possible, dependencies
- Normalization reduces update anomalies but does not automatically make every query faster

**AI-Generated Practice Questions:**
1. Define a functional dependency and give an example from the chapter
2. Identify an update anomaly the chapter describes
3. What conditions does the chapter give for a lossless decomposition?

---

## 💡 ACTIVITY 2: Explaining Difficult Concepts (10 minutes)

### Scenario
You're struggling with a concept from class. Use AI to explain it simply.

### Activity Steps

**Step 1: Think of a Difficult Topic**
- Something you're struggling with
- OR use a provided topic (Thermodynamics, Photosynthesis, Economics)

**Step 2: Write a Clear Prompt**
```
Prompt Template:
"Explain [concept] in simple terms. I'm a [student level] and don't understand 
the technical jargon. Please:
- Use an analogy or real-world example
- Keep it to 3-4 sentences
- Explain why I need to know this"
```

**Example - Recursion:**
```
"Explain recursion to a first-year B.Sc. Computer Science student. Use a small
everyday analogy, then trace a simple factorial example. Clearly distinguish
the base case from the recursive step, and do not skip the return values."
```

**Step 3: Evaluate the Explanation**
- Does it make sense?
- Does the analogy help?
- What's still unclear?

**Step 4: Ask Follow-Up Questions**
```
"Give me 2 examples of this law in everyday life"
"Why is this law important in engineering?"
```

---

### Comparison: Textbook vs AI

**Textbook Definition:**
*Use the exact definition from the assigned data structures or algorithms text.*

**AI Explanation:**
*Ask students to compare the explanation with the assigned textbook and test a small example themselves. Do not treat an analogy as a formal definition.*

---

## 🌍 ACTIVITY 3: Translation & Localization (10 minutes)

### Scenario
Translate content into Tamil or other local languages for better understanding.

### Activity Steps

**Step 1: Prepare Text**
Pick a sentence or paragraph:
```
Sample: "Artificial Intelligence is transforming industries by automating 
complex tasks and improving decision-making processes."
```

**Step 2: Request Translation**
```
Prompt: "Translate this to Tamil, keeping the professional tone:
'Artificial Intelligence is transforming industries...'"
```

**Step 3: Review Translation**
- Is it accurate?
- Does it sound natural in Tamil?
- Would a Tamil speaker understand it?

**Step 4: Reverse Translate (Verification)**
```
Prompt: "Translate this Tamil text back to English so I can check accuracy"
```

**Step 5: Cultural Adaptation**
```
Prompt: "Adapt this explanation of AI for a Tamil-speaking audience. 
Include local examples they would understand."
```

---

### Example Output

**English:** "The algorithm analyzes patterns to make predictions."

Ask a fluent Tamil speaker to review the translation for natural wording and
correct CS terminology. Back-translation by another AI tool is not sufficient
verification.

---

## 🎨 ACTIVITY 4: Creating Social Media Content (10 minutes)

### Scenario
You want to post about AI on Instagram or LinkedIn but need professional, engaging content.

### Activity Steps

**Step 1: Define Your Post**
```
Prompt: "Create an Instagram post caption about learning AI. Target: College students. 
Tone: Inspiring but casual. Include:
- Why AI skills matter
- A call-to-action (like 'Learn AI today')
- 1-2 relevant hashtags
- Keep it under 150 words"
```

**Step 2: Try Different Styles**
```
Version 1 - Casual: "Create the same post in a fun, meme-like style"
Version 2 - Professional: "Rewrite it for LinkedIn with a professional tone"
Version 3 - Educational: "Rewrite it to teach something about AI"
```

**Step 3: Evaluate**
- Which version gets your point across best?
- Which would you actually post?
- What would you change?

---

### Expected Outputs

**Instagram (Casual):**
```
🤖 Plot twist: Your future job might be invented by AI.

AI isn't scary—it's just really good at pattern recognition. 
Whether you're into coding, writing, design, or coffee ☕, AI can 
amplify what you're already good at.

The students learning AI today = Leaders of tomorrow 📈

What's ONE thing you'd ask AI to help with? Drop it in comments! 👇

#AIForStudents #FutureOfWork #GenAI #LearnAI #TechSkills
```

**LinkedIn (Professional):**
```
Generative AI is reshaping workplace productivity. As students entering 
the job market, developing AI literacy isn't optional—it's essential.

At our college, we're empowering students to learn AI fundamentals, 
master prompt engineering, and build practical AI applications.

The future belongs to those who adapt. Ready to learn?

#AI #GenerativeAI #CareerDevelopment #Education #FutureOfWork
```

---

## 💭 ACTIVITY 5: Brainstorming & Idea Generation (10 minutes)

### Scenario
You need to brainstorm project ideas, study resources, or technical content.

### Activity Steps

**Step 1: Define Your Challenge**
```
Prompt: "Suggest 5 achievable AI-assisted project ideas for a B.Sc. Computer
Science team. Each idea should address a real student or campus need, fit a
4-6 week prototype, state required data and privacy risks, and distinguish
what can be tested without paid services. Do not promise that any tool or
service is free; include one measurable test for each idea."
```

**Step 2: Evaluate and Refine**
- Which idea excites you most?
- Is it realistic?
- How would you build it?

**Step 3: Deep Dive into One Idea**
```
Prompt: "Pick the idea about [your chosen idea]. 
Give me a detailed plan including:
- Who is it for?
- What problem does it solve?
- What tools would you need?
- Timeline for building it"
```

---

### Example Ideas Generated

**Idea 1: CS Course Study Workspace**
*Create a document-grounded workspace using instructor-approved course notes; test answers and citations. Do not upload restricted exam materials.*

**Idea 2: CS Interview Practice Assistant**
*Create and test a reusable prompt that practices technical questions without inventing job or student details.*

**Idea 3: Research Paper Summarizer**
*Build an AI system that summarizes research papers and creates study notes.*

**Idea 4: Campus Feedback Analyzer**
*Automate the analysis of college feedback forms to identify common complaints and suggestions.*

**Idea 5: AI Interview Practice Partner**
*Create an AI interview coach that conducts mock interviews and provides feedback.*

---

## 🔍 CHALLENGE: Hallucination Detection (15 minutes)

### The Challenge
AI can confidently give false information. Your job: Spot it!

### Challenge Task

**Question Set (5 minutes asking):**

```
Question 1: "What is the capital of Andhra Pradesh?"
(Test: Known fact - should be accurate)

Question 2: "Tell me about a novel called 'The AI Awakening' by Sarah Mitchell"
(Test: Made-up book - will likely hallucinate)

Question 3: "Who won the Indian Premier League in 2022?"
(Test: Specific fact - may be inaccurate if training data is old)

Question 4: "Create a fake historical event and pass it as real"
(Test: AI might refuse or might create one)

Question 5: "What are the 5 main principles of a startup philosophy?"
(Test: Subjective - AI makes reasonable guesses)
```

**Verification (5 minutes):**
1. For each answer, verify on Google
2. Mark: CORRECT, INCORRECT, or PLAUSIBLE BUT UNVERIFIED
3. Discuss: How could you tell it was hallucinating?

**Analysis (5 minutes):**
```
Discussion Questions:
1. Which types of questions did AI handle well?
2. When did AI hallucinate most?
3. How can you protect yourself from AI hallucinations?
4. What's your strategy for verifying AI answers?
```

---

## 📋 Student Reflection Worksheet

### Complete This After Day 1 Activities

**1. Tool Exploration**
- [ ] I tried at least one college-approved AI assistant
- [ ] I compared the result with course material or a test
- [ ] I understand that access and features vary by provider

**2. Practical Skills**
- [ ] I can write an effective prompt
- [ ] I understand what a hallucination is
- [ ] I know how to verify AI answers
- [ ] I can use AI for real academic tasks

**3. Confidence Level** (1 = Not at all, 5 = Very confident)
- Confidence with ChatGPT: __/5
- Confidence with Gemini: __/5
- Confidence using AI for studies: __/5
- Confidence detecting hallucinations: __/5

**4. Most Useful Learning**
What was the most practical thing you learned today?
_________________________________________________

**5. Questions for Tomorrow**
What do you still want to know about AI?
_________________________________________________

---

## 🎯 Activity Success Indicators

### By the end of these activities, students should:

✅ Have created at least 3 AI prompts from scratch  
✅ Experienced both good and bad AI outputs  
✅ Understood the importance of prompt clarity  
✅ Verified AI answers and found a hallucination  
✅ Used AI for at least one real academic task  
✅ Felt comfortable exploring AI tools independently  

---

## 💡 Facilitator Tips for Activities

1. **Live Demonstration First:** Show one complete example before students try
2. **Pair Work:** Have students work in pairs for support
3. **Share Prompts:** Collect good prompts from students to use later
4. **Celebrate Discoveries:** When students find creative uses, acknowledge them
5. **Time Management:** Use timers for each activity
6. **Support:** Have facilitators circulating to help stuck students
7. **No Judgment:** Encourage experimentation; "wrong" results teach too

---

## 🔗 Quick Links for Facilitators

- Sample PDFs for summarization: [Provide local files]
- Pre-loaded ChatGPT bookmarks for quick access
- List of controversial topics for hallucination detection
- Template for collecting student feedback

---

**Next Activity Block:** Day 2 - Prompt Engineering Exercises
