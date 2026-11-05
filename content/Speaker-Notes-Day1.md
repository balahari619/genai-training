# Day 1 Speaker Notes — Tanglish Delivery Script

**Workshop:** Beyond ChatGPT — From AI Users to AI Creators  
**Audience:** B.Sc. Computer Science students  
**Duration:** 4 scheduled hours, including a 15-minute break  
**Language:** Conversational Tanglish (Tamil in Latin script, with English technical terms)  
**Slides:** [Day1-GenAI-Foundations.html](../slides/Day1-GenAI-Foundations.html)  
**Teaching content:** [Day1-Content.md](./Day1-Content.md)

> These are speaking notes, not a second copy of the lesson content. Use the quoted paragraphs as a natural script, not something you have to read word for word. The italicized directions are for you, not for the class. Pause, listen, and adapt the examples to the students in the room.

## Before students arrive

- Open the slide deck and make sure the photo and logo appear.
- Test the projector, internet connection, and the institution-approved AI tool.
- Keep a no-login fallback ready: a prepared prompt and response that you can show or read aloud.
- Use only a harmless toy code sample or public CS material in the live demo. Never paste passwords, API keys, personal records, confidential code, or restricted course material.
- Have the Day 1 activity sheet and a timer ready.
- If tool access is not available, continue with the prepared response and ask students to evaluate it. The learning goal is not account creation.

## Day 1 run of show

| Time | Slides | Segment |
|---|---:|---|
| 09:00–09:05 | 1 | Welcome and personal introduction |
| 09:05–09:10 | 2–3 | Set expectations and preview the day |
| 09:10–09:30 | 4–5 | AI, ML, Generative AI, and CS examples |
| 09:30–09:45 | 6–9 | How GenAI works, tokens, training, limitations |
| 09:45–10:15 | 10 | Facilitator-led AI demonstration and verification |
| 10:15–10:30 | — | Break |
| 10:30–11:30 | 11 | Guided exploration of an approved assistant |
| 11:30–12:15 | 12 | Beyond text: image, code, presentation, audio/video examples |
| 12:15–12:30 | 13 | Responsible-use habits and challenge briefing |
| 12:30–12:45 | 14 | Team AI challenge |
| 12:45–12:55 | 15 | Student share-back |
| 12:55–13:00 | 16 | Recap and exit ticket |

The schedule is a guide. If a conversation is valuable, keep it—but protect enough time for students to try, verify, and reflect.

---

## Slide 1 — Beyond ChatGPT: From AI Users to AI Creators
**Suggested time: 5 minutes**

### Say

“Vanakkam everyone! Naan Bala Hari. CS Visually-oda founder; Thoughtworks-la GenAI consultant-aa work panren. Software engineering, data, AI indha areas-la five years-ku mela work pannirukken. PayPal, Comcast-layum experience irukku.”

“Indha workshop-la naan unga kitta AI pathi lecture mattum panna poradhilla. Neengalum try pannuveenga, questions keppeenga, output-ai verify pannuveenga. Indha five days mudiyumbodhu, AI tools-ai responsible-aa use panna theriyanum; oru useful AI-based solution-ai neengale design panna mudiyanum.”

“AI expert-aa, illa coding expert-aa inga vara vendiya avasiyam illa. Curiosity-oda vandhaa podhum. Namma ellarum serndhu explore pannalaam.”

### Ask the room

“Ungalukku AI edhavadhu build panna, illa purinjikka help pannumna, neenga enna try panna virumbuveenga?”

*Give two or three students a chance to answer. Acknowledge answers warmly. If the room is quiet, say:* “Parava illa, yosikka time eduthukkonga. Workshop pogapoga ideas varum.”

### Transition

“Super. Andha curiosity-oda, innikki AI basics-la irundhu start pannuvom.”

---

## Slide 2 — Generative AI Foundations
**Suggested time: 2 minutes**

### Say

“Innikki namma Generative AI-na enna, adhu roughly eppadi work aagudhu, namma CS studies-la eppadi use pannalaam-nu paaka porom. AI use pannina answer correct-aa irukka-nu eppadi check panradhu-nu kooda practice pannuvom.”

“AI tool use pannirukkanum-nu inga prerequisite illa. Neenga already use pannirundhaalum, innikki konjam different angle-la paapom: ‘Idhu enna nalla pannudhu? Enna panna mudiyadhu? Naan eppadi verify pannalaam?’”

### Ask

“Yaaravadhu already AI tool use pannirukkeengala? Oru hand raise pannunga—just curiosity.”

*Do not quiz or make anyone explain if they do not want to.*

### Transition

“Indha questions-ku answer theda, innikki namma follow panna pora route-ai paapom.”

---

## Slide 3 — Understand it. Try it. Question it.
**Suggested time: 3 minutes**

### Say

“Namma innikki moonu maadhiri work pannuvom: first concept understand pannuvom; apram tool use panni try pannuvom; kadaisila answer-ai question panni verify pannuvom.”

“First, AI, Machine Learning, Generative AI difference. Appuram, models-um tokens-um pathi oru simple mental model. Break-kku appuram tools explore pannuvom. Text mattum illa, code, image, audio maadhiri examples-um paapom. Kadaisila team-aa oru chinna challenge.”

“Terms ellam memorize pannradhu namma target illa. Oru concept puriyala na innooru explanation kekka theriyanum; answer vandhaa, adhu correct-aa-nu check panna theriyanum. Adhu dhaan innikki namma goal.”

### Transition

“Appo first question: AI, Machine Learning, Generative AI—indha moonum eppadi related?”

---

## Slide 4 — AI is the broad field; GenAI is one part
**Suggested time: 12 minutes**

### Say

“AI-nu sonna adhu oru broad field. Computer systems-ku prediction, language, image recognition, decision support maadhiri tasks panna help pannra methods ellam indha broad area-kulla varalaam.”

“Machine Learning-nu sonna, data-la irundhu patterns learn panni prediction illa decision edukka use pannra methods. Oru spam filter-ai example-aa eduthukkalaam. Spam, non-spam messages-oda examples kuduthaa, system-ku sila patterns identify panna mudiyum. Aana adhu oru simple analogy dhaan; computer manushan maadhiri learn pannudhu-nu artham illa.”

“Generative AI enna different? Idhu content generate pannum—text, image, audio, code maadhiri. Oru email classify pannradhu prediction task-a irukkalaam; pudhu email draft pannradhu generation task.”

“Idha strict-aa separate boxes maadhiri nenachikka vendaam. Generative AI-um Machine Learning methods use pannalaam. Aana ella AI system-um pudhu content generate pannadhu.”

### Ask the room

“Email spam filter—idhu generate pannudha, illa classify pannudha?”

*Let students answer: classify/predict.*

“Chat assistant oru paragraph draft panninaa?”

*Let students answer: generate.*

“Good. Ippo unga phone face unlock, map-la traffic prediction, movie recommendations—ivai ellam AI use pannra examples-a irukkalaam. Aana ivai ellam Generative AI-nu solla mudiyadhu.”

### If students ask whether AI “thinks”

“‘Think’ nu solradhu casual-aa use pannalaam; aana technical-aa system eppadi work aagudhu-nu paakumbodhu careful-aa irukkanum. Innikki namma AI-ai human maadhiri conscious-aa irukku-nu assume panna maatom. System enna input edukkudhu, enna output kudukkudhu, adhai eppadi evaluate pannalaam-nu focus pannuvom.”

### Transition

“Indha difference-ai namma CS student life-oda connect panni paapom.”

---

## Slide 5 — Where GenAI fits into your CS journey
**Suggested time: 8 minutes**

### Say

“Computer Science padikkumbodhu, sila concepts first time-la click aagaadhu. Recursion, data structures, networking—AI-kitta ‘idha beginner level-la explain pannu’ illa ‘innoru example kudu’ nu kekkalaam.”

“Code ezhudha munnaadi pseudocode kekkalaam. Oru error message irundhaa, possible causes enna-nu ideas kekkalaam. Test cases brainstorm panna sollalaam. Aana AI kudukkira answer-ai direct-aa submit pannaama, code run panni, tests panni, neengale explain panna mudiyudha-nu paakanum.”

“AI unga learning-ku assistant-aa irukkalaam; unga understanding-ku replacement illa. Course-la AI use pathi enna rules irukko adhai follow pannunga. Disclosure venumna transparent-aa disclose pannunga.”

### Ask

“Indha list-la unga course work-ku romba useful-aa irukkum-nu thonradhu edhu—concept explanation-aa, debugging ideas-aa, test cases-aa?”

*Take a few answers. Ask one follow-up: “Adhu kudukkira answer correct-aa-nu neenga eppadi check pannuveenga?”*

### Transition

“Ippo AI assistant response eppadi create pannudhu-nu romba simple-aa paapom. Idhu deep technical architecture lecture illa—oru mental model mattum.”

---

## Slide 6 — A simple mental model: input → model patterns → output
**Suggested time: 7 minutes**

### Say

“Neenga oru prompt type panreenga. Model andha prompt-um, conversation-la irukkira relevant context-um process panni, adutha output enna irukkalaam-nu generate pannudhu. Language model text-ai piece by piece generate pannum.”

“Oru analogy try pannalaam. Neenga sentence start pannina, adha paathu aduthu endha words varalaam-nu guess pannradhu maadhiri oru simplified idea. Aana AI-oda process idha vida romba complex; adhu manushan maadhiri meaning purinjikkudhu-nu indha analogy sollala.”

“Prompt clear-aa irundhaa relevant response varra chance improve aagum. Context useful-aa irundhaa answer better fit aagalaam. Aana prompt nalla irundhaalum truth guarantee aagadhu.”

“Image model-um language model-um same-aa work pannum-nu solla koodadhu. Image, audio, text ellathukkum different representations, different methods irukkalaam.”

### Check understanding

“Model-ukku question kuduthaa, adhu answer-ai Google-la search panni edukkudhu-nu automatic-aa assume pannalama?”

*Expected response: illa / tool irundhaa mattum.*

“Correct. Sila tools browsing use pannalaam; sila tools use pannaadhu. Product-la feature enabled-aa-nu check pannanum.”

### Transition

“Response text generate aagumbodhu, words-ai model eppadi handle pannum? Adhukku token-nu oru term irukku.”

---

## Slide 7 — Tokens and context
**Suggested time: 5 minutes**

### Say

“Model text-ai process pannumbodhu, sentence-ai tokens-nu sollra chinna pieces-aa split pannum. Sila short words full token-aa irukkalaam; sila long words parts-aa piriyalaam; punctuation-um token-aa irukkalaam.”

“Idhu exact-aa eppadi split aagudhu-nu model-um language-um poruththu maarum. Adhanaala ‘oru word equals oru token’ nu fixed rule illa.”

“Context window-na, oru request-la model consider panna mudiyara information-oda limit. Prompt, conversation, attach panna documents, tool results—idhellam context occupy pannalaam. Romba lengthy input kuduthaa, ella details-um model consider pannidum-nu nambakoodadhu.”

### Quick analogy

“Phone-la memory limited irukkira maadhiri imagine pannunga. Oru conversation-la romba neraya information serndhaa, sila details-ai summarize panna vendiyirukkalaam. Model context-um limited dhaan; limit evvalavu-nu model/product poruththu maarum.”

### Transition

“Tokens pathi basic idea vandhuduchu. Ippo training time-la model enna learn pannudhu, namma use pannumbodhu enna nadakkudhu-nu separate pannip paapom.”

---

## Slide 8 — Training and using a model
**Suggested time: 5 minutes**

### Say

“Training time-la model parameters adjust aagi, training objective-ku thevaiyana patterns learn panna try pannum. Endha data use pannanga, eppadi train pannanga-nu model poruththu details maarum. Namma indha class-la adha full-aa cover panna maatom.”

“Namma AI tool use pannumbodhu training process-ai live-aa thirumba nadathradhu illa. Namma prompt-um conversation context-um base panni system output generate pannudhu.”

“Oru mukkiyamaana clarification: assistant automatically internet search pannum, namma laptop files ellam padikkum, Python code run pannum-nu assume panna koodadhu. Andha features irundhaa, product-la explicit-aa browsing, file, illa code tool connect aagirukkum. Access and settings check pannanum.”

### Ask

“Oru chat assistant code snippet kuduthuchu-na, adhu code-ai actually run panniduchu-nu namakku eppadi theriyum?”

*Listen for: tool / execution result / explicit output. Reinforce that generated code alone is not evidence that it ran.*

### Transition

“Model pattern base panni output generate pannudhu. Appo output nalla confident-aa irundhaa, adhu correct-nu arthama? Adha next slide-la paapom.”

---

## Slide 9 — A confident answer can still be wrong
**Suggested time: 6 minutes**

### Say

“Hallucination-nu sonna, AI unsupported-aa illa incorrect-aa irukkira details-ai confident tone-la produce pannalaam. Answer smooth-aa irukkum; structure-um nalla irukkum. Aana adhu factually correct-nu adhu mattum vechu solla mudiyadhu.”

“Code example-la, AI oru library method name suggest pannalaam. Andha method actual-aa irukka? Unga version-la work aaguma? Parameter correct-aa? Official documentation-la verify pannanum. Code-na, safe environment-la run panni tests pannanum.”

“Ellaa mistake-um hallucination-nu label panna vendam. Prompt ambiguous-aa irundhirukkalaam, context missing-aa irukkalaam, information old-aa irukkalaam, illa model reasoning-la mistake aagirukkalaam. Namma use panna vendiya habit: important answer-na evidence thedu.”

### Ask

“AI oru answer-ku citation kuduthaa, citation irukkaradhu mattum podhuma?”

*Expected: no; open and inspect the cited source.*

“Correct. Citation genuine-aa irukka, andha source-la actual-aa claim irukka-nu check pannanum.”

### Transition

“Ippo indha principle-ai oru chinna demo-la apply pannalaam. Naan answer generate panna kaamikka poradhilla mattum; adhai eppadi check panradhu-nu kooda kaamikka poren.”

---

## Slide 10 — Facilitator demonstration: ask, inspect, verify
**Suggested time: 30 minutes**

### Set up — 3 minutes

“Namma oru simple code example use pannuvom. Idhu toy example; unga assignment illa, private repository illa. AI tool-ku personal data, password, API key edhuvum share panna maatom.”

*Open the approved assistant. If unavailable, project the prepared example and response. Use a short loop/indexing snippet prepared in advance.*

### Ask the assistant — 5 minutes

Type:

```text
Explain why this loop might skip the last item.
Use a tiny example input and show the index values.
Do not claim to have run the code.
```

“Indha prompt-la task clear-aa irukku. ‘Tiny example’ nu specify pannirukkom; ‘index values show pannu’ nu check panna mudiyara output kekkirom. ‘Code run pannadha’ nu solli, run pannadha result-ai run pannadhu maadhiri present panna vendam-nu constraint kudukkirom.”

### Read and inspect the response — 7 minutes

“Ippo answer-ai padikkumbodhu, fluent-aa irukku-nu mattum paakaama, index trace correct-aa irukka-nu paapom. Example input-la list length enna? Loop endha index-la start aagudhu? Condition last element-ai include pannudha?”

*Think aloud. If an answer appears incorrect, point it out calmly and show how to catch the error. If it is correct, still explain how you checked it.*

### Verify — 10 minutes

“Namma ippo manually index trace panni paapom. Oru test input choose pannalaam. Expected output enna? Actual code behavior enna? Code run panna approved environment irundhaa run pannalaam; illatti paper-la trace pannalaam.”

*Ask students to suggest one normal input and one edge case, such as an empty list or a one-item list. Avoid implying one test proves a program correct.*

### Reflect — 5 minutes

Ask:

- “AI answer-la useful-aa irundhadhu enna?”
- “Neenga verify pannina claim edhu?”
- “Innum enna check pannina nambikkai adhigamaagum?”

### If the tool is unavailable

“Live tool access ippo work aagala. Parava illa—learning goal tool open pannradhu illa. Namma prepared response-ai paathu, same maadhiri test case yosichu verify pannuvom.”

### Transition to break

“Super. Namma ‘AI sonnadhu correct-aa?’ nu kekkaradhukku oru process irukku-nu paathom: prompt, inspect, verify. Ippo 15-minute break. Break-kku appuram neengale tools use panni explore pannuveenga.”

---

## Break — 15 minutes

*Before resuming, make sure the approved tool and fallback activity are ready. Do not spend the break asking students to create personal accounts.*

---

## Slide 11 — Guided exploration: try one task
**Suggested time: 60 minutes**

### Re-entry — 3 minutes

“Welcome back! Ippo unga turn. Neenga oru AI tool use panni, oru small CS task try pannuveenga. Specific AI tool use pannirukkanum-nu illa; access illa na pair-aa work pannalaam, illa screen-la irukkira prepared example-ai review pannalaam.”

### Explain the activity — 5 minutes

“Moonu options: oru CS concept-ai beginner level-la explain panna sollunga; oru short pseudocode example draft panna sollunga; illa simple algorithm-ku test cases suggest panna sollunga. Unga task safe-aa, non-sensitive-aa irukkanum.”

“Response vandhaa, adhai notes, official documentation, illa small example/test use panni verify pannunga. Oru useful point, oru uncertainty, oru limitation note pannunga.”

### Student work — 35 minutes

*Students work individually or in pairs. Walk around and coach; do not dictate exact prompts. If a student is stuck, offer:*

“Neenga first simple-aa kekkalaam: ‘Binary search eppadi work aagudhu-nu first-year student-kku explain pannu; oru small sorted list example use panni each step show pannu.’ Appuram answer-la endha step-ai verify panna mudiyum-nu paapom.”

*Prompts to use while circulating:*

- “Indha answer-la neenga verify panna vendiya claim edhu?”
- “Oru small input vechu test panna mudiyuma?”
- “Response unga level-kku suitable-aa irukka? Innum simple-aa solla kekkalaama?”
- “Tool access issue irundhaa, rendu perum oru response-ai share panni review pannalaam.”

### Pair comparison — 10 minutes

“Ippo unga partner-oda compare pannunga. Same task-aa? Prompt different-aa? Output-la enna difference? Endha answer-ai verify panna easy-aa irundhudhu?”

### Debrief — 7 minutes

Ask:

“Yaaravadhu one useful answer share pannuveengala?”

Then ask:

“Adhai eppadi check panneenga?”

Reinforce:

“AI tool useful-aa irundhudhu-nu sollradhu oru vishayam; adhu correct-nu evidence irukku-nu sollradhu vera vishayam. Rendum distinguish pannunga.”

### Transition

“Ippo namma text assistant-ai thaandi, vera media types-la AI enna panna mudiyum-nu paapom. Feature access vary aagum; available demo mattum use pannuvom.”

---

## Slide 12 — Beyond text: multimodal examples
**Suggested time: 45 minutes**

### Introduce — 3 minutes

“AI output text mattum illa. Sila tools image create pannum; sila audio-ai transcribe illa summarize pannum; sila coding assistant code suggestions kudukkum; sila tools presentation outline create pannum. Ellaa tools-layum ellaa features irukkum-nu artham illa.”

“Indha examples-ai demo panradhu capability explore panna dhaan. Generated output correct, unbiased, ready-to-publish-nu assume panna koodadhu.”

### Image or diagram demo — 12 minutes

Use an approved image tool and ask for a simple non-sensitive CS concept illustration:

```text
Create a simple diagram of a web request moving through a browser,
application server, and database, then returning a response.
Use clear labels and arrows.
```

Say:

“Prompt-la components-um direction-um specify pannirukkom. Output vandha apram server, database, request-response direction correct-aa irukka paapom. AI-generated diagram-la label spelling thappa varalaam; arrow direction-um wrong-aa irukkalaam.”

Ask:

“Indha diagram-ai class notes-la use panna munnaadi enna verify pannanum?”

### Code assistant demo — 12 minutes

“Ippo short code snippet-ai explain panna solli, possible edge cases and test ideas kekkalaam. Suggestion vandhaa, tool code run panniduchu-nu assume panna koodadhu. Approved environment-la run panni, tests pannanum.”

*Show only a small, harmless snippet. Keep student projects and credentials private.*

### Presentation content demo — 7 minutes

“Presentation tool use pannina, adhu outline illa slide draft create panna help pannalaam. Aana technical claim, diagram, citation ellam namma verify pannanum. Slides visually nalla irukkaradhu content correct-nu artham illa.”

### Audio/video optional demo — 6 minutes

“Available approved tool irundhaa, public illa permitted CS handout use panni audio summary maadhiri feature demo pannalaam. Feature illa na skip pannalaam; indha activity-ku students account create pannanum-nu illa.”

### Debrief — 5 minutes

“Image, code, presentation—ellathulayum same habit: output useful-aa irukka? Enna mistake irukkalaam? Namma eppadi verify pannalaam?”

### Transition

“Capability paathom. Ippo responsible-aa use panna moonu habits-ai settle pannuvom; adhai next team activity-la apply pannuveenga.”

---

## Slide 13 — Three habits for safer AI use
**Suggested time: 5 minutes**

### Say

“Moonu word nyabagam vechukkonga: protect, verify, be transparent.”

“Protect-na password, API key, personal records, restricted course material-ai unapproved tool-la share panna koodadhu.”

“Verify-na important facts, citations, code, calculations, generated images—use panna munnaadi check pannanum.”

“Be transparent-na unga college-oda course rules follow pannanum. AI help use pannirundhaa disclose panna sollirundhaa, adhai clear-aa sollanum.”

“Oru AI assistant suggest pannina work-ku final responsibility nammadhu dhaan.”

### Ask

“Ungalukku indha moonula most easy-aa marandhuruva habit edhu? Adhai eppadi nyabagam vechukkalaam?”

*Take one or two comments.*

### Transition

“Ippo unga group indha habits-ai use panni oru chinna challenge pannum.”

---

## Slide 14 — Team challenge: improve and check an answer
**Suggested time: 15 minutes**

### Brief — 2 minutes

“Group-la rendu illa moonu per serunga. Moonu challenge options irukku: algorithm-ai beginner-kku explain panna sollunga; toy function-ku test cases draft panna sollunga; illa public CS topic-ai summarize panna sollunga.”

“Public illa synthetic content mattum use pannunga. Yaaroda personal details-um, private assignment answer-um tool-la poda vendaam.”

### Give the task — 1 minute

“Neenga four things prepare pannanum: task enna, AI answer enna, oru claim-ai eppadi verify panneenga, oru limitation enna. Fluent answer mattum success illa—verify pannina process dhaan success.”

### Group work — 9 minutes

*Move between groups. Offer help only when needed:*

- “Prompt-la audience specify pannirukkeengala?”
- “Oru small example use panni answer test panna mudiyuma?”
- “Indha answer-la tool guess pannirukkalaam-nu thonra part edhu?”
- “Oru source illa test use panni verify pannunga.”

### Prepare share-back — 3 minutes

“Oru speaker select pannunga. 30 seconds-la unga prompt/task, verification, limitation—indha moonaiyum share panna ready pannunga.”

### Transition

“Ippo sila groups-oda experience kekkalaam. Answer correct-aa irundhadhu mattum illa, eppadi check panneenga-nu share pannunga.”

---

## Slide 15 — Share back: what worked, what needed checking?
**Suggested time: 10 minutes**

### Facilitate

“Rendu moonu groups, unga task-ai short-aa share pannunga. Neenga enna prompt kudutheenga? Answer-la useful-aa irundhadhu enna? Edhai verify panneenga? Enna limitation kandupidicheenga?”

*After each group, ask one follow-up:*

- “Neenga verification-ku enna evidence use panneenga?”
- “Innum oru test pannina enna therinjirukkum?”
- “Indha answer-ai real assignment-la use panna munnaadi enna change/check pannuveenga?”

### Reinforce

“Oru answer work aagala na adhu fail illa. Adhu enna assumption wrong, enna detail missing, enna verify pannanum-nu namakku kaattudhu. Tool output-ai blindly accept pannama question panninadhu dhaan innikki important skill.”

### Transition

“Great work. Last-aa innikki namma eduthuttu poganum-nu irukkira main points-ai recap pannuvom.”

---

## Slide 16 — Generate, then evaluate
**Suggested time: 5 minutes**

### Recap

“Innikki AI, Machine Learning, Generative AI eppadi related-nu paathom. Generative AI text, image, code maadhiri content create pannalaam; aana adhu kudukkira answer always correct-nu guarantee illa.”

“Tokens and context window pathi simple idea paathom. Tools-oda features vary aagum-nu therinjikittom. Oru AI output-ai useful-aa use panna, adhai verify panna vendiyadhu namma responsibility.”

### Exit ticket

“Kelamburadhukku munnaadi, oru chinna exit ticket:  
1. Innikki unga pudhu learning enna?  
2. AI answer-la neenga verify panna vendiya oru vishayam enna?  
3. AI use pannumbodhu follow panna pora oru rule enna?”

*Students can say it aloud, write it on paper, or share in their group.*

### Close

“Thanks everyone! Innikki neenga AI-ai use pannadhu mattum illa—AI answer-ai question panni verify-um panneenga. Naalaikku prompt-ai eppadi clear-aa design panni, CS study, code explanation, debugging, career preparation-la use pannalaam-nu hands-on-aa paapom. Curiosity-oda vaanga!”

---

## Quick reference: if the room gets stuck

### If no one answers

“Naan oru example start panren; adhukku neenga add pannunga.” Then give one low-pressure example and invite a show of hands or pair discussion before asking for spoken responses.

### If an answer sounds confidently wrong

“Nalla point. Idhai fact-aa accept pannama, namma eppadi check pannalaam?” Treat it as a verification exercise, not a student mistake.

### If the AI tool is unavailable

Use the prepared response or printed activity. Say: “Tool access issue namma learning-ai stop pannaadhu. Output-ai eppadi evaluate pannradhu-nu offline-aa practice pannalaam.”

### If a student shares sensitive information

Do not repeat or project it. Ask them to remove it from the prompt if possible, and remind the class to use synthetic or public examples and follow institutional guidance.

### If discussion runs over time

Shorten the number of share-backs, not the verification step. Keep the final exit ticket brief so you can still hear whether students understood the key idea.

