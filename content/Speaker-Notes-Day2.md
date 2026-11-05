# Day 2 Speaker Notes — Detailed Tanglish Delivery Script

**Session:** Prompt Engineering & AI for Computer Science

**Audience:** B.Sc. CS students

**Duration:** 4 scheduled hours, including a 15-minute break

Use with [Day 2 content](./Day2-Content.md) and the [activity workbook](../activities/Day2-Activities.md).

This is a separate spoken script, not a replacement for the teaching content or the short notes in the Day 1 HTML deck. Sections match the Day 2 presentation storyboard; a Day 2 HTML slide deck is not included.

Quoted paragraphs are suggested words to speak. Italic text is a facilitator cue—do not read it aloud. Keep the Tanglish conversational; you can change phrases to match your usual speaking style. Do not lecture throughout the practice blocks: explain briefly, let students work, then ask how they verified the output.

## Timing map

| Time | Sections | Focus |
|---|---|---|
| 09:00–09:30 | 1–4 | Foundations and prompt demonstration |
| 09:30–10:45 | 5–10 | Five guided labs |
| 10:45–11:00 | — | Break |
| 11:00–11:30 | 11 | Evidence and targeted refinement |
| 11:30–12:15 | 12–14 | Study, careers, and prompt toolkit |
| 12:15–12:55 | 15 | Challenge and share-back |
| 12:55–13:00 | 16 | Recap and exit ticket |

---

## 1. Welcome back — Generate, then evaluate
**09:00–09:05**

### Say

“Vanakkam everyone! Yesterday AI enna panna mudiyum, enna limitations irukku-nu paathom. Innikki namma AI-kitta eppadi task clear-aa sollradhu, answer useful-aa irukka-nu eppadi check panradhu-nu practice pannaporom.”

“Start pannradhukku munnaadi oru quick question: yesterday AI answer-la neenga check panna vendiyirundha oru vishayam nyabagam irukka?”

*Take two responses. Ask about the check, not just the tool name.*

“Good. Answer confident-aa irundhaalum verify pannanum-nu namma paathom. Innikki adhai next level-ku eduthuttu porom. Prompt improve pannuvom; aana improved prompt correct answer guarantee pannum-nu solla maatom.”

### If the room is quiet

“Oru small example: AI oru code snippet kuduthaa, code-ai actually run pannucha? Illa explanation mattum generate pannucha? Indha difference nyabagam irundhaa podhum.”

### Transition

“Appo today mudiyumbodhu unga kitta enna irukkanum-nu first paapom.”

---

## 2. What you will create today
**09:05–09:08**

“Innikki neenga five reusable prompts save panna poringa: concept explain panna, code understand panna, bug investigate panna, test cases design panna, study illa career preparation-ku help panna.”

“Adhoda, oru before-and-after example maintain pannuvom. Initial prompt enna, response-la enna missing, follow-up-la enna change pannom, adhai eppadi verify pannom—indha record mukkiyam.”

“Python therinja code run pannalaam. Theriyala na paper-la trace panni check pannalaam. AI account access illa na prepared response-ai review pannalaam. Learning goal ellarukkum same.”

*Ask students to open the workbook or take out paper. Do not spend the block troubleshooting every account.*

### Transition

“Prompt-na enna? Periya technical term maadhiri irundhaalum, basic-aa adhu oru task description.”

---

## 3. A prompt is not a magic spell
**09:08–09:18**

“Namma oruthar-kitta help kekkumbodhu, ‘idha pannu’ nu mattum sonna avangalukku clarity irukkaadhu. Yaarukkaaga, enna purpose, enna format-nu sonna easier-aa help panna mudiyum. AI prompt-layum indha clarity useful.”

“Five questions yosikkalaam: enna task? Yaarukkaaga? Enna background theriyum? Enna constraints? Answer-ai eppadi check panna porom?”

“For example, ‘Explain binary search’ nu kekkaradhukkum, ‘First-year CS student-kku sorted array-la binary search trace panni explain pannu’ nu kekkaradhukkum difference irukku.”

“Role add pannalaam—‘act as a tutor’ nu. Aana role sonna AI real professor aagidum-nu illa. Relevant context dhaan mukkiyam. ‘Twenty years experience irukkira expert’ nu type pannina answer automatically trustworthy aagadhu.”

### Ask

“Neenga friend-kitta assignment help kekkumbodhu, avangalukku first enna information solluveenga?”

*Use students' answers to point to task, background, and expected output.*

“Correct. More details always better-nu illa. Task-ku sambandham illaadha details add pannina noise aagum. Useful details mattum kuduppom.”

### Transition

“Ippo same task-ai moonu prompts-la try panni difference paapom.”

---

## 4. Vague → clearer → checkable
**09:18–09:30**

*Show the three binary-search prompts from the content file. Run selected versions if access permits; otherwise explain the expected differences without promising exact model behavior.*

“First prompt: ‘Explain binary search.’ Idhu wrong prompt-nu solla mudiyadhu; aana learner level, example, output format ellam open-aa irukku. Model guess panni answer pannalaam.”

“Second prompt-la first-year student-nu context add panrom. Third-la sorted input requirement, small example, index convention, midpoint rule add panrom. Ippo response-la enna irukkanum-nu namakku clear.”

“Target 11; list `[2, 5, 8, 11, 14]`. First midpoint index 2—value 8. Target bigger, so right side. Next midpoint index 3—value 11. Found.”

*Write the two trace rows. Explain zero-based indexing if necessary.*

“Answer table-la idhe varudha-nu check pannalaam. Prompt clear-aa irundhaalum, response-la wrong index irukkalaam. Namma check panna vendiyadhu irukku.”

### Ask

“Indha improved prompt-la answer-ai verify panna easiest-aa help pannina detail edhu?”

*Accept the example input, midpoint rule, sorted assumption, or required trace.*

### Transition

“Ippo neengale prompts write pannuveenga. First useful context-um role-um try pannalaam.”

---

## 5. Lab 1 — Useful context and a tutor role
**09:30–09:45**

### Brief

“Starting prompt ‘Teach me recursion.’ Idhai improve pannunga. Learner-ku loops theriyum, recursion new-nu assume pannunga. Base case, recursive case, factorial of 3 example, rendu understanding questions kekkalaam.”

“Role optional. Patient tutor-nu sonna tone set aagalaam; aana input details miss aagirundhaa role mattum adhai fix pannaadhu.”

*Use 3 minutes to model, 7 minutes for pair work, 3 minutes for response review, and 2 minutes for recording the check.*

### While circulating

“Unga prompt-la neenga already enna theriyum-nu sonneengala?”

“Answer vandha, factorial of 3 enna aaganum-nu independently check pannunga.”

“Base case explain pannirukka? Recursion always faster-nu edhavadhu overclaim irukka?”

### Debrief

“Factorial of 3 result 6. Andha example-la recursion stop aagura base case clear-aa irukkanum. Example helpful-aa irundhaalum, adhai trace panni purinjikradhu namma velai.”

### Transition

“Ippo answer format-ai control panna try pannuvom. Table nalla irundhaa study panna easy; aana table correct-aa-nu separate-aa check pannanum.”

---

## 6. Lab 2 — Constraints and structured output
**09:45–10:00**

“Arrays versus linked lists compare panna solluvom. First important detail: fixed-size array-aa? Python list-aa? Singly linked list-aa? Assumptions change aanaa answer-um change aagum.”

“Prompt-la indexed access, search, insertion, deletion, memory layout include panna sollunga. Assumption column add pannunga.”

*Show the prepared structured prompt. Give pairs time to inspect one response or the fallback checks.*

“Linked list insertion always O(1)-nu sonna enna missing? Insert panna vendiya location already theriyudha? Illa first adhai search pannanuma?”

*Allow answers before explaining.*

“Known node/reference irundhaa link update constant time-la nadakkalaam. Aana position kandupidikka traversal venumna time adhigam. Adhanaala context and assumptions matter.”

### Debrief

“Format beautiful-aa irukkaradhu accuracy illa. One row choose panni course notes-oda compare pannunga. Assumption correct-aa irukka-nu check pannunga.”

### Transition

“Structure-ai describe pannradhu oru way. Output example kaatturadhu innooru way.”

---

## 7. Lab 3 — Few-shot examples
**10:00–10:15**

“Few-shot prompting-na, namakku thevaiyana pattern-ai sila examples use panni kaatturadhu. Innikki simple bug-report labels use pannuvom: validation, calculation, display.”

“Blank name accepted-na validation. Total wrong-aa add aagudhu-na calculation. Button text cut off-na display.”

*Read the three examples and let pairs classify the three new inputs.*

“Negative age accepted—validation. Wrong tax percentage—calculation. Heading overlaps menu—display. Aana ‘Submit press panna crash aagudhu’ nu sonna? Idhu endha category-nu confidently solla enough details irukka?”

“Missing details kekkalaam. Every input-kum forced-aa label kudukkanum-nu illa.”

### Important distinction

“Indha examples kuduthadhu model-ai retrain pannadhu illa. Namma current request-la output pattern guide panrom. Fine-tuning different process. Examples thappa irundhaa output-um wrong pattern follow pannalaam.”

### Transition

“Ippo text labels-la irundhu code explanation-ku pogalaam. Python theriyala na kooda trace follow panna mudiyum.”

---

## 8. Lab 4 — Trace before trusting
**10:15–10:30**

*Display the `count_even` function and its pseudocode from the content file. Use a list diagram rather than expecting Python proficiency.*

“Namma intended task list-la irukkira even numbers ellathaiyum count pannradhu. Input `[2, 3, 4]`. Manual-aa count panna rendu even numbers irukku—2 and 4.”

“Code-la loop index enga stop aagudhu-nu paapom. Python range ending value-ai include pannaadhu. Indha code-la list length minus one ending value-aa kuduthirukkom. So indexes 0 and 1 mattum visit aagum.”

“Index 0-la 2 even; count 1. Index 1-la 3 odd; count still 1. Last value 4 check aagala. Function 1 return pannum; intended result 2.”

*Give pairs the trace worksheet. Ask them to compare their own trace with the assistant's explanation.*

“AI trace kuduthaa, adhu actual execution result illa. Namma paper-la trace pannalaam; approved environment irundhaa run pannalaam. Rendum worksheet-la clear-aa label pannunga.”

### Transition

“Bug identify pannittom. Ippo fix propose pannuvom—but fix-ku munnaadi expected behavior clear-aa irukkanum.”

---

## 9. Lab 5, first part — Debugging needs intended and actual behavior
**10:30–10:37**

“Debugging prompt-la three details useful: code, expected behavior, actual behavior. ‘Code work aagala’ nu mattum sonna model-ku guess panna vendiyirukkum.”

“Inga expected result 2; actual 1. Smallest fix loop-la minus one remove pannradhu. Direct-aa values iterate panra solution-um valid-aa irukkalaam; aana smallest textual change venumna range ending adjust pannalaam.”

“Fix suggestion vandhaa adhai appadiye trust panna vendaam. Endha changed line behavior-ai correct pannudhu-nu explain panna sollunga. Apram tests use panni check pannuvom.”

*Let pairs write the debugging prompt and the minimal change.*

### Transition

“Oru input-la result correct-aa vandhaa podhuma? Test design konjam careful-aa pannanum.”

---

## 10. Lab 5, second part — Tests that actually reveal the bug
**10:37–10:45**

“Empty list expected 0. `[2]` expected 1. `[3]` expected 0. Mixed list `[2, 3, 4]` expected 2. `[-2, 1, 0]` expected 2—zero-um even.”

*Ask students to fill expected results before any execution.*

“Original code-ku `[2, 3]` test kuduthaa result 1 varum. Correct code-kum 1 dhaan. Why? Skip aagura last item odd. Indha test bug-ai expose pannaadhu.”

“So test pass aagudhu-nu mattum paakaama, test enna behavior check pannudhu-nu kekkanum. `[2]` illa last item even-aa irukkira list original bug-ai reveal pannum.”

### Break announcement

“Ippo 15-minute break. Break-kku appuram model thappa answer pannumbodhu, follow-up-la enna specific-aa sollradhu-nu practice pannuvom.”

---

## 11. Evidence and targeted refinement
**11:00–11:30: 15 minutes concepts + 15 minutes practice**

### Welcome back and explain

“Welcome back! AI answer nalla sound aagudhu-na adhu evidence illa. Trace table irundhaa inspect panna mudiyum; source passage irundhaa claim support pannudha-nu check panna mudiyum; code execute pannina tested inputs-ku actual behavior theriyum.”

“Long explanation irundhaa correct-nu guarantee illa. ‘Step by step sollu’ nu kekkaradhu verification-ku replacement illa. Namma inspect panna mudiyara assumptions, trace, tests, sources kekkanum.”

“Wrong response vandhaa ‘try again’ nu mattum sollama, exact mismatch sollunga. Prompt-la enna requirement miss pannirukku? Endha claim unsupported? Adhai identify panni follow-up write pannunga.”

### Practice

*Show the deliberately faulty binary-search answer. Do not present it as an actual provider response.*

“Idhu namma exercise-kaaga prepare pannina faulty answer: binary search any list-la work aagum; always O(1); trace 8, 14, 11. Indha answer-la enna defects irukku?”

*Have pairs identify the three defects and write one targeted follow-up.*

“Sorted input requirement, midpoint convention, worst-case complexity—indha moonaiyum follow-up-la specify pannalaam. Then trace rows verify pannuvom.”

“Oru revision panniyum wrong-aa irundhaa endless-aa prompt panna vendaam. Course notes illa trusted source refer panni, unresolved issue note pannunga.”

### Transition

“Ippo source itself namma prompt-la kuduthaa enna benefit-nu paapom.”

---

## 12. Study using supplied sources
**11:30–11:45**

“Stack and queue pathi short classroom note namma provide panrom. Indha source use panni study sheet create panna solluvom. AI-kku ‘use only this note’ nu constraint kuduppom.”

“Stack LIFO—last in, first out. Push A, push B, pop pannina B remove aagum. Queue FIFO—first in, first out. Enqueue A, enqueue B, dequeue pannina A remove aagum.”

*Let pairs request a comparison, two questions, and a separate answer key. Have them compare against the original note.*

“Ippo exam date kekkalaam. Note-la exam date irukka? Illa. So answer invent pannaama ‘source-la information illa’ nu sollanum.”

“Source kuduthaa hallucination completely disappear aagidum-nu illa. Namma response source-ku faithful-aa irukka check pannanum. Naalaikku document-grounded assistant build pannumbodhum indha habit thevai.”

### Transition

“Source faithfulness study-ku mattum illa. Resume-la namma real profile-ku faithful-aa irukkanum.”

---

## 13. Honest career assistance and interview practice
**11:45–12:00**

“Inga synthetic student profile use panrom. Actual student details upload panna thevai illa. Basic Python, SQL theriyum; library tracker course project-la menu handling and input validation pannirukkaar; five manual tests; internship experience illa.”

“Idhai use panni rendu resume bullets create panna sollunga. Output-la ‘500 users’, ‘40 percent improvement’, ‘production deployment’ vandhaa enna problem? Profile-la evidence illa.”

“Professional-aa rewrite pannradhu okay; qualifications invent pannradhu okay illa. Metric illana model question kekkalaam; number create panna koodadhu.”

*Have students inspect two bullets, then try the one-question-at-a-time interview prompt.*

“Mock interview-la one question kekka sollunga. Unga answer-kku wait panna sollunga. Ella questions-um ore time-la list panninaa interactive practice goal miss aagudhu.”

“AI feedback useful-aa irukkalaam; aana actual hiring decision illa. Resume format illa role suggestions job guarantee pannaadhu.”

### Transition

“Innikki practice pannina patterns-ai save panni reusable toolkit-aa maathuvom.”

---

## 14. Build your five-prompt toolkit
**12:00–12:15**

“Concept tutor, code explainer, debugging helper, test designer, study/career helper—indha five prompts save pannunga. Topic, learner level, code, expected behavior, source note maadhiri input places-ku placeholders vechukkonga.”

“Prompt reusable-aa irukkanumna, earlier chat-la sonna details-ai depend pannaama necessary input-ai include pannanum. Fresh chat open pannina model previous conversation therinjirukkum-nu assume panna koodadhu.”

*Ask each pair to swap one prompt and change its input. Allow feedback rather than demanding five live model calls.*

“Partner unga prompt-ai use pannumbodhu missing context edhavadhu kandupidicheengala? Adhai add pannunga. Input maarina old example answer appadiye varudha? Appo prompt refine pannanum.”

### Transition

“Toolkit ready. Ippo one final challenge-la task, output, verification—ellathaiyum connect pannuvom.”

---

## 15. Final challenge and share-back
**12:15–12:55**

### Brief

“Moonu options-la onnu choose pannunga: beginner-kku API explain pannunga; stack/queue note use panni study sheet create pannunga; illa toy function bug diagnose panni tests propose pannunga.”

“First five minutes-la success criteria write pannunga. Adutha ten minutes prompt and output; next ten minutes verification and one revision. Apram five minutes record complete pannunga. Last ten minutes groups share pannalaam.”

“AI access illa na prepared response-ai inspect panni, neenga send panna vendiya improved prompt write pannunga. Paid tool use panna thevai illa; namma focus learning process dhaan.”

### While circulating

“Unga acceptance criteria enna?”

“Indha answer-la neenga actually verify pannina part edhu?”

“Expected result-um actual result-um separate-aa note pannirukkeengala?”

“Prompt change pannina specific defect enna fix aaganum?”

“Oru limitation honest-aa note pannunga. Ellame perfect-nu solla thevai illa.”

### Share-back

“Oru minute-la unga task, prompt improvement, verification, limitation share pannunga. Tool name vida process mukkiyam.”

*Select a few pairs according to time. Give feedback about task fit and evidence, not prompt length.*

“Good prompt-na longest prompt illa. Useful context, clear task, check panna mudiyara output, actual verification—indha combination dhaan mukkiyam.”

### Transition

“Innikki learning-ai three questions-la close pannuvom.”

---

## 16. Recap, exit ticket, and Day 3 bridge
**12:55–13:00**

“Innikki prompts-la task, context, constraints, output format, examples use panna practice pannom. Code trace, bug diagnosis, test cases, study source, honest career content—indha areas-la AI help eppadi use pannalaam-nu paathom.”

“Aana role add pannadhu expertise guarantee illa; examples kuduthadhu retraining illa; table beautiful-aa irundhadhu correctness illa; explanation irundhadhu execution evidence illa.”

### Ask

“Unga original prompt-la missing-aa irundha useful detail enna?”

“Neenga enna verify panneenga, eppadi?”

“Follow-up panniyum wrong-aa irundhaa next enna pannuveenga?”

*Students can write a brief exit ticket instead of everyone speaking.*

### Close

“Innikki five prompts-oda toolkit unga kitta irukku. Naalaikku approved CS documents use panni source-grounded course assistant create pannuvom. Innikki ‘source-la irukka?’ nu ketta question, naalaikkum namma main habit-aa irukkum. Thanks everyone!”

---

## Facilitator recovery lines

### If no one answers

“Partner-oda thirty seconds discuss pannunga; apram oru idea share pannalaam.” Start with a low-pressure pair discussion rather than calling on someone unexpectedly.

### If a student is uncomfortable with code

“Syntax ellam memorize panna vendaam. List-la evvalavu even values irukku-nu first count pannuvom; apram code visit pannra indexes-ai paper-la mark pannuvom.”

### If the assistant gives a correct answer immediately

“Correct-aa irukku-nu namakku eppadi theriyum? Adhai check pannina evidence record pannunga.” Do not try to force a model mistake.

### If the assistant gives an incorrect answer

“Idhu useful verification opportunity. Exact mismatch identify panni one targeted follow-up pannuvom. Still wrong-na source/test use panni unresolved-aa note pannuvom.”

### If the tool is unavailable or limited

“Live output venam; prepared answer use panni same exercise pannalaam. Namma learning task-ai tool availability decide panna vendaam.”

### If students want to paste personal resumes or private code

“Indha session-ku synthetic profile and toy code podhum. Personal/private information share panna thevai illa; institution-approved access and policy follow pannunga.”

### If time runs short

Reduce live provider comparisons and the number of share-backs. Keep the verification step, saved toolkit, and exit ticket.
