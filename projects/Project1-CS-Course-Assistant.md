# Project 1: CS Course Knowledge Assistant

**Day 3 Main Project | Document-grounded AI | No coding required for the core activity**

---

## 🎯 Project Overview

**What You're Building:** A source-grounded study workspace that answers questions about selected B.Sc. Computer Science course documents.

**Why This Matters:** Demonstrates how AI can be used to create practical solutions that help real people.

**Technology Used:** Google NotebookLM or an institution-approved document-grounded AI tool. Availability, limits, and features can change.

**Important:** NotebookLM is a document-based AI workspace. It is not a custom-built, standalone chatbot that you can deploy or integrate into another application. This project teaches document grounding, source checking, and evaluation.

---

## 📚 What The AI Assistant Will Do

Students ask questions about approved course sources, and the AI responds with references when available:

```
Student: "What is the difference between a stack and a queue in our notes?"
AI: Summarizes the relevant source material and points to the cited section

Student: "Which steps do the lecture notes give for database normalization?"
AI: Summarizes the steps from the uploaded course document

Student: "Does this material explain when a hash collision occurs?"
AI: Answers from the sources, or says it cannot find the explanation

Student: "Give me a question that tests the concept, but don't show the answer yet."
AI: Creates a practice question that the student should check against the notes
```

---

## 🛠️ Step-by-Step Building Process

### STEP 1: Select Approved Course Sources (30 minutes)

**Useful Sources:**
- Instructor-approved lecture notes or slides
- A public course syllabus or module outline
- Openly licensed or instructor-provided textbook excerpts
- Public documentation for a programming language or software tool
- Your own notes, after removing personal or restricted information

**Choose 2-4 sources** that cover one focused topic, such as data structures,
database systems, operating systems, or computer networks. Use current,
permitted materials and note each source's title and date.

Do not upload private student records, credentials, personal data, copyrighted
course material without permission, or confidential institutional documents.

---

### STEP 2: Create a Document Workspace (10 minutes)

**Go to:** https://notebooklm.google.com

**Access:** Use only an institution-approved account and service. Account requirements and availability vary. If students cannot access the workspace, use the facilitator's prepared demonstration or an approved alternative; do not require personal account creation.

**Create New Notebook:**
1. Create a notebook or workspace using the currently available interface.
2. Name it for the topic, e.g. "Data Structures Study Assistant".
3. Check that the selected tool is permitted by your institution.

---

### STEP 3: Upload Documents (20 minutes)

**Method 1: Direct PDF Upload**
1. Click "Add source" in your notebook
2. Select "Upload files"
3. Choose approved course documents (PDFs)
4. Wait for processing to complete; time and supported formats vary.

**Method 2: Copy-Paste Text**
1. If the file cannot be uploaded, use a supported source option
2. Click "Add source"
3. Select "Paste text"
4. Add only material you are allowed to use

**Expected:** The tool confirms that sources are available for questions.

---

### STEP 4: Test Your Assistant (30 minutes)

**Start Asking Questions:**

In the chat area, ask questions like:

```
Question 1: "According to the uploaded notes, what is a stack?"
Expected: AI summarizes a relevant source section

Question 2: "What is the difference between a stack and a queue in these notes?"
Expected: AI compares the source descriptions and points to supporting passages

Question 3: "Compare the two sorting algorithms discussed in these notes."
Expected: AI compares only details supported by the sources

Question 4: "Create a short practice question about this topic, and cite the source concept."
Expected: AI generates a question; student checks it against the notes

Question 5: "What is the time complexity of the algorithm in this example?"
Expected: AI cites a source if stated; otherwise, verify the analysis independently
```

**Verification Process:**
For each answer AI gives:
1. Mentally verify: "Is this from the documents I uploaded?"
2. Cross-check: If important, re-read the source document
3. Note: Any questions AI couldn't answer (outside scope)

---

### STEP 5: Test Edge Cases (15 minutes)

**Questions AI Should Answer:**
- Questions directly from uploaded documents ✅
- Questions that require combining information ✅
- Follow-up questions on previous answers ✅

**Questions AI Might Struggle With:**
- Information not in documents ❓
- Real-time information (current exam dates) ❓
- Information that changed after document was created ❓

**Test These Scenarios:**
```
Q: "What is the time complexity of this algorithm?"
(Check whether the sources provide the answer; verify independently if not.)

Q: "Compare the two data structures discussed in separate sources."
(Check that every part of the answer is supported.)

Q: "What is the current exam timetable?"
(The workspace should not guess if the sources do not contain it.)
```

---

### STEP 6: Improve Your Assistant (20 minutes)

**If AI Is Missing Information:**

1. **Add More Documents**
   - Add another permitted course source
   - Check that the new source is relevant and current

2. **Ask Better Questions**
   ```
   Bad: "Tell me everything about data structures"
   Good: "Based only on the uploaded notes, compare the two search algorithms and cite the relevant source."
   ```

3. **Use Follow-up Questions**
   ```
   Q1: "What is a primary key?"
   Q2: "How does the source distinguish a primary key from a foreign key?"
   Q3: "Which section supports that answer?"
   ```

---

## 📋 Project Deliverables

### Deliverable 1: Documentation

Create a document explaining your assistant:

```
CS COURSE KNOWLEDGE ASSISTANT - Project Report

1. Purpose
   Which course topic does your study workspace support?
   Who is the intended student user?

2. Sources Used
   List each approved course source and its date
   Explain why each is relevant

3. Sample Conversations
   Show a supported question, a synthesis question, and an out-of-scope test

4. Strengths
   What answers were supported by clear source passages?
   
5. Limitations
   Which answers were unsupported, incomplete, or difficult to verify?

6. Potential Improvements
   What source, evaluation test, or interface would you add next?

7. Scope
   Explain why this NotebookLM workspace is not a custom standalone chatbot.
```

---

### Deliverable 2: Live Demonstration

During Day 3, demonstrate your assistant:

**Demo Script (5 minutes):**

1. State the CS topic and intended user.
2. Show the sources and ask one question supported by them.
3. Show a citation and verify it against the original.
4. Test an unsupported question and describe the limitation.
5. Explain one improvement and clarify the workspace's scope.

**Backup Plan:** If internet fails, present a prepared test log and screenshots. Do not include private data.

---

## 🎯 Evaluation Criteria

### Success Metrics

| Criterion | Full Marks | Partial | Needs Work |
|-----------|-----------|---------|-----------|
| **Sources Selected** | 3-4 current, permitted CS sources | 2-3 suitable sources | Missing or unsuitable |
| **Workspace Setup** | Sources processed and scope clear | Works with minor issues | Not ready to test |
| **Evaluation Tests** | 5+ varied tests including out-of-scope | 3-4 relevant tests | Fewer than 3 tests |
| **Grounding Checks** | Citations checked against originals; gaps identified | Some answers checked | Claims accepted without checks |
| **Documentation** | Complete & clear | Mostly done | Incomplete |
| **Demonstration** | Clear, smooth demo | Works with issues | Can't demo |
| **Insight/Reflection** | Deep understanding | Basic understanding | Surface level |

---

## 💡 Real-World Applications

The same document-grounding concept can support:

1. **Course study:** Explore approved lecture notes or public documentation
2. **API documentation:** Find information in a selected public reference
3. **Project onboarding:** Search permitted repository documentation
4. **Research:** Locate claims in permitted academic sources

These are applications of document-grounding techniques; a hosted workspace is
not automatically a deployed chatbot.

---

## 🚀 Pro Tips for Success

### Tip 1: Document Quality
- Use readable, approved sources with titles and dates
- Note missing, outdated, or conflicting information
- Do not add confidential or unlicensed documents

### Tip 2: Test Thoroughly
- Ask questions you KNOW the answer to first
- Then ask new questions
- Check if AI cites sources correctly

### Tip 3: Organization
- Group sources by CS topic
- Use clear file names

### Tip 4: Demo Preparation
- Practice your 5-minute demo
- Have backup answers ready
- Test internet connection before demo day

### Tip 5: Document Upload
- Follow the selected provider's current file-size and format limits
- Check that text is selectable and readable before upload

---

## 📞 Troubleshooting

### Issue: Document Upload Fails
**Solution:** 
- Ensure it's a PDF or text format
- Try splitting into smaller files
- Check file isn't corrupted

### Issue: AI Gives Wrong Information
**Solution:**
- Upload more recent/accurate documents
- Re-check the source document
- The tool may still misread or misrepresent source content; verify the cited passage

### Issue: AI Says "I Don't Have This Information"
This may be appropriate when sources do not contain the answer, but it does
not prove the tool is reliable. Check the sources and test other out-of-scope
questions.

### Issue: Internet Disconnects During Demo
**Preparation:**
- Pre-load your assistant
- Screenshot key conversations
- Have phone hotspot as backup
- Practice demo offline with screenshots

---

## 🎓 Learning Outcomes

By completing Project 1, you will have:

✅ Created a document-grounded CS study workspace  
✅ Understood document grounding and its limitations  
✅ Experienced AI's strengths (summarizing, finding info)  
✅ Discovered AI's limitations (it needs good source material)  
✅ Created a tested resource for CS course study  
✅ Learned a skill that applies to many real jobs  

---

## 🔗 Resources

- NotebookLM: https://notebooklm.google.com (check account and institution availability)
- Help: https://support.google.com/notebooklm
- Alternative: Any institution-approved document-grounded workspace

---

**Next:** Project 2 on Day 5 - CS Career and Technical Interview Assistant
