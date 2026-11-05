# Days 3, 4, 5: Complete Content Overview

**Summary of remaining workshop days with learning objectives and key content**

---

## 📅 DAY 3: Document-Grounded AI (Project 1)

### 🎯 Learning Objectives
- Explain how document-grounded question answering uses selected sources
- Create and evaluate a CS course study workspace using approved materials
- Distinguish a hosted document workspace from a custom-built, deployable app

### ⏱️ Schedule
- **9:00-9:45** (45 min): Document-grounded AI concepts and demonstration
- **9:45-11:15** (90 min): Guided project development
- **11:15-11:30** (15 min): Break
- **11:30-12:15** (45 min): Continue project development and test sources
- **12:15-1:00** (45 min): Demonstration, peer review, and reflection

### 📚 Key Topics

#### Introduction to Document-Grounded AI (30 min)

**What is a chatbot?**
- A conversational interface to a software system
- It may generate responses, retrieve information, use tools, or combine these approaches

**Useful distinctions:**
1. A fixed FAQ system selects from pre-written answers.
2. A generative model creates a response from learned patterns and current context.
3. A document-grounded assistant uses selected sources to help answer questions; retrieval-augmented generation (RAG) is one common architecture, though each product may implement it differently.

**How Knowledge-Based Chatbots Work:**
```
User selects approved documents
↓
Tool processes or indexes the sources
↓
User asks question
↓
Tool uses relevant source content as context
↓
Model generates an answer; citations may be available and must be checked
↓
User checks the answer against the original source
```

**Real-World Examples:**
- Course study assistant (answers from approved course notes)
- API documentation Q&A (answers from selected public documentation)
- Research Q&A (helps locate material in permitted papers)

#### Practical: Document-Grounded Study Workspace Demo (45 min)

**Live Demonstration:**
1. Open an institution-approved tool (account requirements vary)
2. Add instructor-approved CS course material
3. Ask questions and inspect cited source passages
4. Test an unanswerable question
5. Clarify: this workspace is not a custom chatbot application

**Student Practice Activity:**
- Students create a topic-focused notebook/workspace
- Add 2-4 approved course sources
- Test supported and unsupported questions
- Record whether each answer is grounded in the source

#### Project 1: CS Course Knowledge Assistant

**Full details in:** `projects/Project1-CS-Course-Assistant.md`

**Key Components:**
1. Select permitted sources on one CS topic
2. Add sources to a document-grounded workspace
3. Test direct, synthesis, and out-of-scope questions
4. Check citations and answers against the originals
5. Document limits and prepare a short demonstration

**Success Criteria:**
- Answers are checked against the selected course sources
- Student can explain what source grounding does and does not guarantee
- Out-of-scope behavior is tested and documented
- Student accurately describes this as a hosted workspace, not a standalone app

---

## 📅 DAY 4: AI Workflows, Agents & Automation (Optional Build Challenge)

### 🎯 Learning Objectives
- Distinguish a chatbot, a fixed workflow, and an AI agent
- Identify triggers, actions, conditions, permissions, and human review
- Design a simple workflow; building an automation is an optional extension

### ⏱️ Schedule
- **9:00-9:45** (45 min): Chatbots, workflows, and agents
- **9:45-10:45** (60 min): Guided workflow design
- **10:45-11:00** (15 min): Break
- **11:00-12:15** (75 min): Optional platform prototype or workflow simulation
- **12:15-1:00** (45 min): Test with synthetic data and reflect

### 📚 Key Topics

#### Chatbots, Workflows, and AI Agents (45 min)

**Chatbots:**
- Reactive (respond to user input)
- Single turn or conversation
- Answer questions
- Example: ChatGPT

**AI Agent (introductory definition):**
- Uses an AI model to pursue a bounded goal through one or more steps
- May select from explicitly available tools or actions
- Needs permissions, limits, monitoring, and human review
- Is not simply any chatbot or automation

**Fixed workflow:** Runs a predefined trigger/action sequence. Adding an AI classification step does not automatically make it an autonomous agent.

**Demonstration Comparison:**
```
CHATBOT:
User pastes an approved sample message and asks for a summary.

FIXED WORKFLOW:
A test form submission triggers a predefined sequence: store a response,
ask AI to categorize it, then place the proposed category in a review sheet.

AGENT (conceptual example):
Within explicit permissions, an AI system selects a next step from approved
tools to complete a bounded task. A person reviews consequential actions.
```

#### AI Workflows & Automation (60 min)

**What's an Automation Workflow?**

A series of automated steps triggered by an event:

```
TRIGGER → ACTION 1 → ACTION 2 → ACTION 3 → RESULT
```

**Example: Synthetic Course Feedback Triage Workflow**

```
TRIGGER: Facilitator submits synthetic feedback through a test form
↓
ACTION 1: Collect responses in spreadsheet
↓
ACTION 2: AI suggests a topic label and sentiment
↓
ACTION 3: AI categorizes topic (academics/facilities/food/etc)
↓
ACTION 4: Create summary report
↓
RESULT: Proposed labels appear in a sheet for human review
```

**Key Automation Concepts:**
- **Trigger:** Event that starts workflow (form submission, email received, time scheduled)
- **Action:** What happens (send email, update spreadsheet, call AI)
- **Condition:** If X is true, do Y (if negative feedback, alert manager)
- **Iteration:** Repeat for each item (process each feedback one by one)

Tool features, account eligibility, integrations, and free usage limits change. Select one platform only if it is approved and available; otherwise, use the workflow diagram and a simulated spreadsheet.

#### Optional Guided Challenge: Prototype a Feedback Workflow (75 min)

**Step 1: Design Your Workflow (15 min)**

```
Feedback Flow:
1. Test form → collect synthetic feedback
2. Store in Google Sheets
3. AI analyzes sentiment
4. Create summary report
5. Human reviewer approves any follow-up action
```

**Step 2: Set Up Google Form (15 min)**

Create form with fields:
- Feedback topic
- Feedback text
- Rating (1-5)

**Step 3: Connect Form to a Spreadsheet (10 min, if available)**

- Enable form responses to go to spreadsheet
- Verify data flows correctly

**Step 4: Optional Platform Prototype (25 min, only if approved and available)**

```
Make Step 1: Watch for new rows in Google Sheets
↓
Make Step 2: Send synthetic feedback to an approved AI service for suggested classification
↓
Make Step 3: Add result back to spreadsheet
↓
Make Step 4: Summarize findings
↓
Make Step 5: Place a draft summary in a human-review step
```

**Step 5: Test Workflow (10 min)**

- Submit synthetic test feedback
- Check the proposed categories and summary against the inputs
- Do not send messages or take consequential actions automatically

#### Real-World Applications (30 min)

**Example Workflows to Discuss:**

1. **Bug Report Triage**
   - Trigger: A synthetic issue report is submitted
   - Action: AI suggests a topic label and priority for human review
   - Result: A reviewer checks the suggested label before routing

2. **Public Documentation Digest**
   - Trigger: A facilitator adds a public documentation link
   - Action: Extract key topics and draft a summary
   - Result: A learner reviews source links before sharing

3. **Test Report Summary**
   - Trigger: A synthetic test run produces results
   - Action: Summarize failures and group similar messages
   - Result: A developer verifies the summary against actual test output

4. **Code Review Checklist**
   - Trigger: A sample code change is submitted
   - Action: AI drafts a checklist of possible issues
   - Result: A human reviewer inspects the code and tests it

---

## 📅 DAY 5: Final Project & Career Opportunities

### 🎯 Learning Objectives
- Apply all skills to build a useful personal AI tool
- Understand career opportunities in AI
- Complete and demo final project
- Discuss responsible AI use

### ⏱️ Schedule
- **9:00-9:45** (45 min): Project briefing, responsible use, and career context
- **9:45-11:15** (90 min): Guided project development
- **11:15-11:30** (15 min): Break
- **11:30-12:15** (45 min): Peer testing and refinement
- **12:15-1:00** (45 min): Demonstrations and CS careers discussion

### 📚 Key Topics

#### Project 2: CS Career and Technical Interview Assistant

**What You're Building:** A reusable, prompt-based assistant that helps a CS student explore roles, describe real project experience, and practice technical interviews. This is a tested prompt workflow, not a separately deployed software application.

**Core Features:**

1. **Project and Resume Feedback**
   - Improves clarity of real skills and project descriptions
   - Does not invent experience, impact metrics, or qualifications

2. **CS Role Exploration**
   - Compares roles such as software developer, QA engineer, data analyst, and support engineer
   - Separates common requirements from job-posting-specific requirements

3. **Technical Interview Practice**
   - Asks one question at a time on selected topics
   - Gives feedback on the student's explanation and solution approach
   - Encourages testing and discussing complexity where relevant

4. **Skill Development Plan**
   - Relates learning goals to the student's current courses and projects
   - Labels recommendations as suggestions to verify, not guaranteed hiring advice

**Building Process (90 min):**

**Step 1:** Define Your Career Goal
```
"I'm exploring roles: software developer / QA engineer / data analyst.
Skills and courses I have completed: [actual details]
Projects I have built: [actual details and my contribution]
Skills I want to develop: [specific goals]
Time available: [realistic weekly hours and target date]"
```

**Step 2:** Create AI Instructions

Using ChatGPT or Gemini, craft detailed instructions:

```
"You are a supportive career and technical-interview coach for B.Sc. Computer Science students.

Your goal: Help [student name] transition into [target role].

About the student:
- Background: B.Sc. Computer Science student, [actual skills and experiences]
- Goal: Get [target role] at [company type]
- Timeline: [Your timeline]
- Challenges: [What's hard for you]

Your responsibilities:
1. Help describe only verified coursework, skills, and projects
2. Compare entry-level CS roles using evidence I provide
3. Conduct a mock technical or behavioral interview, one question at a time
4. Give feedback on correctness, clarity, and what to practice next
5. Suggest a realistic skill plan and mark claims that need checking

Never invent job requirements, company interview questions, credentials, or
salary facts. Ask clarifying questions when information is missing.

Interview style: Professional but supportive
Tone: Encouraging, honest about challenges
Language: Clear, avoid jargon unless appropriate"
```

**Step 3:** Save a Reusable Prompt

Use an approved chat tool to test the instructions, then save them in a
document or an available custom-instruction feature. Feature availability
depends on the account and platform; a saved prompt is an acceptable project
deliverable.

**Step 4:** Test Your Assistant

Ask your assistant:
1. "Rewrite this project description for clarity without adding claims."
2. "Compare these two entry-level CS role descriptions and list verified differences."
3. "Interview me on data structures, one question at a time."
4. "Review my answer and identify one correct point, one gap, and one next step."
5. "Create a four-week study plan from these courses and my available hours."

**Step 5:** Document & Present

Create presentation:
- Who is this assistant for? (You or others?)
- What problem does it solve?
- How would you improve it?
- Lessons learned

**Demonstration (5 min):**
- Show assistant in action
- Ask 2-3 questions live
- Explain how you'd use this

#### CS Careers and Responsible AI Panel (45 min)

**Section 1: AI Career Landscape (15 min)**

**CS Career Paths to Explore**

1. **Software Developer:** programming, data structures, collaboration, and testing.
2. **QA / Test Engineer:** test design, automation, debugging, and product quality.
3. **Data Analyst / Junior Data Engineer:** SQL, data quality, statistics, and communication.
4. **Cybersecurity Analyst:** networking, operating systems, secure practices, and careful investigation.
5. **AI/ML Engineer (longer learning path):** programming, mathematics, data, model evaluation, and deployment.
6. **Cloud / Support Engineer:** systems fundamentals, troubleshooting, scripting, and clear documentation.

Role titles and entry requirements vary. Students should verify current requirements using actual local job postings rather than rely on generic AI career predictions.

**Sector Opportunities:**
- Finance: AI for credit decisions, fraud detection, trading
- Healthcare: AI for diagnosis support, treatment planning
- Education: AI tutors, personalized learning, assessment
- Marketing: AI for personalization, content generation
- HR: AI for recruitment, performance analysis
- Government: AI for policy analysis, citizen services

AI literacy complements, but does not replace, CS fundamentals and practical project experience.

**Section 2: How to Prepare Now (10 min)**

**For B.Sc. Computer Science Students:**

1. **Develop AI Literacy**
   - Understand what AI can/can't do
   - Know popular tools and their strengths
   - Follow AI news and trends

2. **Build CS Foundations**
   - Practice programming, data structures, databases, networks, and testing
   - Use AI to support learning, not to skip the fundamentals

3. **Build a Verifiable Portfolio**
   - Document what you built, what AI helped with, and what you tested
   - Share only work you are permitted to publish; never post credentials or private data

4. **Stay Curious**
   - Experiment with new AI tools
   - Read about AI developments
   - Join AI communities online

5. **Communication Skills**
   - Learn to explain technical concepts simply
   - Develop writing skills
   - Practice presenting ideas clearly

**Example Learning Paths:**

| Interest | Possible Path | Useful Foundations |
|------------|-----------|-----------|
| Building applications | Software developer | Programming, data structures, databases, testing |
| Finding patterns in data | Data / ML roles | Python, SQL, statistics, evaluation |
| Protecting systems | Cybersecurity | Networks, operating systems, secure coding |
| Making software reliable | QA / test engineering | Test design, debugging, automation |

**Section 3: Responsible AI & Ethics (15 min)**

**Key Principles for Ethical AI Use:**

1. **Honesty**
   - Disclose when content is AI-generated
   - Don't pass off AI work as entirely your own
   - Be transparent about AI limitations

2. **Accuracy**
   - Verify AI outputs, especially facts
   - Don't trust AI blindly
   - Understand when to use AI and when not to

3. **Fairness**
   - Be aware of AI biases
   - Don't use AI to discriminate
   - Question AI's answers if they seem unfair

4. **Responsibility**
   - Use AI to enhance your skills, not replace learning
   - Take accountability for AI-generated content
   - Respect copyright and privacy

5. **Sustainability**
   - Understand AI's environmental impact
   - Use AI tools thoughtfully
   - Consider if automation is needed

**Real-World Ethical Dilemmas:**

```
SCENARIO 1: Your assignment
Q: Can you have AI write your entire essay?
A: No - that's academic dishonesty. Using AI to brainstorm/improve? Yes.

SCENARIO 2: Hiring with AI
Q: Is it okay to use AI to screen job candidates?
A: Risky - AI often has biases. AI can help, but humans must review.

SCENARIO 3: Creating content
Q: Can you generate images with AI and publish them?
A: Check the tool's terms. Some allow commercial use, others don't.

SCENARIO 4: Privacy concerns
Q: Should you paste private student data or unpublished code into an AI tool?
A: Only use services approved for that data. When uncertain, do not upload it.
```

**Taking Responsibility:**

- Always attribute AI assistance
- Verify facts especially for academic/professional work
- Understand AI's limitations
- Use AI to enhance, not replace critical thinking
- Stay informed about AI developments and concerns

**Section 4: Q&A & Open Discussion (5 min)**

Students ask:
- "What should I learn next?"
- "How do I get a job using AI skills?"
- "Is AI going to replace my career?"
- "Should I specialize in AI?"
- "How do I learn programming?"

---

## 📊 Final Workshop Assessment

### Assessment Components

| Component | Marks | Details |
|-----------|-------|---------|
| Day 1 & 2 Activities | 20 | Participation, prompt quality, CS use cases, verification |
| Project 1: CS Course Knowledge Assistant | 30 | Source quality, grounding checks, limitations, demo |
| Project 2: CS Career and Technical Interview Assistant | 40 | Useful instructions, realistic tests, accuracy, reflection |
| Final Participation & Demo | 10 | Engagement, clear presentation, Q&A |
| **Total** | **100** | - |

The Day 4 workflow build is an optional, ungraded extension. Students may
complete the workflow design activity without creating accounts or connecting
live services.

### Success Criteria

**Minimum Passing (70+):**
- Completed both projects
- Demonstrated understanding of concepts
- Participated in activities

**Strong Performance (85+):**
- Both projects well-executed
- Creative use of tools
- Clear explanations
- Good presentations

**Excellent (95+):**
- High-quality projects
- Innovative applications
- Clear understanding of limitations
- Inspiring presentations
- Helps peers learn

---

## 🎓 Final Deliverables

By end of Day 5, each student will have:

1. ✅ **Project 1:** CS course study workspace grounded in approved sources
2. ✅ **Project 2:** Reusable CS career and technical interview prompt assistant
3. ✅ **Documentation:** Written explanations of both projects
4. ✅ **Demonstrations:** 5-minute presentation of each project
5. ✅ **Portfolio:** Project notes, test evidence, and reflection to show employers or use for future learning
6. ✅ **Knowledge:** Understanding of AI fundamentals and career paths

---

## 💼 Certificate & Continuation

**Workshop Certificate:**
Upon completion, all students receive a certificate recognizing:
- Completion of 5-day GenAI workshop
- Practical projects completed
- AI literacy demonstrated

**Next Steps:**
1. Add projects to LinkedIn/portfolio
2. Continue learning with advanced courses
3. Explore specific AI specialization paths
4. Build more projects independently
5. Join AI communities and attend meetups

---

## 🔗 Resources for Continued Learning

### Free Learning Platforms
- Google AI Essentials
- OpenAI Learning Platform
- Coursera Free Courses
- YouTube AI Education Channels

### Communities
- Reddit: r/ChatGPT, r/OpenAI
- Discord: Various AI communities
- LinkedIn: Follow AI thought leaders
- Twitter: Stay updated on AI news

### Tools to Explore
- Python and notebooks for optional AI coding projects
- Model APIs and retrieval systems as follow-on topics, after learning security, privacy, and cost basics
- Specialized tools used in the student's chosen CS area

---

**Workshop Complete!**

**Congratulations on completing the 5-Day Generative AI Workshop.**

**You now have practical AI skills that you can immediately apply in your studies, career, and life.**

**Keep learning, stay curious, and build amazing things with AI! 🚀**
