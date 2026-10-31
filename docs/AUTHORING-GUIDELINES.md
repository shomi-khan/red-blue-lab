# Authoring Guidelines

## 1. Reader contract

পাঠক গল্প পড়তে এসেছে। তাকে classroom-এ বসিয়ে দেওয়া যাবে না।

- গল্পের প্রথম কাজ পাঠককে situation, character, question বা mystery-র মধ্যে টেনে নেওয়া।
- Learning narrator-এর ঘোষিত agenda হবে না।
- "এই অধ্যায়ে আমরা শিখব" বা "এখন tool বানাই" ধরনের classroom language novel-এ নয়।
- Character-এর action, decision, mistake, investigation ও consequence দিয়ে technical detail প্রকাশ পাবে।
- গভীর ব্যাখ্যা আলাদা learning artifact-এ থাকবে।

## 2. Narrative craft

### Scene-এ জীবন
প্রয়োজনমতো motive, immediate need, setting, dialogue, silence, disagreement, incomplete information, changing hypothesis ও human consequence থাকবে। প্রতিটি scene-এ সবকিছু থাকা বাধ্যতামূলক নয়।

### Character exposition machine নয়
চরিত্র শুধু concept explain করার জন্য থাকবে না। তাদের নিজস্ব motive, expertise, blind spot, relationship ও limitation থাকবে। কেউ সবসময় সঠিক হবে না।

### Mystery ও suspense
- Clue fair হতে হবে; reveal-এর পর আগের ইঙ্গিত বোঝা যাবে।
- Red herring থাকতে পারে, author cheating নয়।
- Mystery-র উত্তর technical plausibility ও character motivation পূরণ করবে।
- সব প্রশ্ন এক episode-এ resolve করতে হবে না।
- Cliffhanger optional, বাধ্যতামূলক formula নয়।

### Pacing
Dense prose-কে scene break, short paragraph, dialogue, evidence excerpt, timeline, diagram বা image দিয়ে ভাঙো। একই তথ্য বারবার বলো না। Fixed word count নেই; filler নয়।

## 3. Technical storytelling

Technical detail narrative-এ আসবে যখন সেটি decision বদলায়, clue ব্যাখ্যা করে, hypothesis পরীক্ষা করে, risk তৈরি করে বা system limitation প্রকাশ করে। অপ্রয়োজনীয় lecture আলাদা Concept Note-এ সরাও।

### Evidence discipline

| শ্রেণি | অর্থ |
|---|---|
| Observation | সরাসরি দেখা বা মাপা তথ্য |
| Evidence | Claim যাচাইয়ে ব্যবহৃত artifact |
| Hypothesis | পরীক্ষা বাকি থাকা সম্ভাব্য ব্যাখ্যা |
| Inference | Evidence থেকে যুক্তিসঙ্গত সিদ্ধান্ত |
| Confirmed finding | নির্ধারিত পদ্ধতিতে যাচাই করা ফল |
| Unknown | উপলব্ধ evidence দিয়ে জানা যায়নি |

Log-এ event নেই মানেই event ঘটেনি নয়। Timeout মানেই port closed নয়। AI অদ্ভুত output দিয়েছে মানেই model compromised নয়।

### Technical integrity
- Drama তৈরির জন্য protocol behavior বদলাবে না।
- TCP connection established হওয়া application healthy প্রমাণ করে না।
- Encryption থাকলেই endpoint নিরাপদ নয়।
- Authentication ও authorization আলাদা।
- AI model, training data, retrieval source, orchestration ও infrastructure আলাদা attack surface।
- Vulnerability, exploitability, impact ও attribution আলাদা।
- Simplification করলে label করো।

## 4. Story ও learning content আলাদা

- **Novel:** scene, dialogue, action, clue, conflict, revelation।
- **Concept Note:** system explanation, diagram, protocol walkthrough, comparison।
- **Lab:** experiment, implementation specification, local fixture, verification।
- **Reference:** glossary, architecture note, evidence index, continuity fact।

Novel-এ checklist বা acceptance criteria ঢোকাবে না। গল্পের প্রয়োজনে tool তৈরি হতে পারে; সেটির optional Lab আলাদা থাকবে।

## 5. Bengali-first writing

- Narrative ও explanation স্বাভাবিক বাংলায়।
- Technical term English-এ: TCP handshake, trust boundary, privilege escalation, packet capture।
- প্রথমবার term এলে ছোট বাংলা ব্যাখ্যা দাও।
- Code, command, protocol field, API, log key ও JSON/YAML field অপরিবর্তিত রাখো।
- সংলাপ চরিত্র অনুযায়ী স্বাভাবিক হবে।
- অনুবাদসুলভ বাক্য, ভারী শব্দ ও inconsistent term এড়িয়ে চলো।

## 6. Flexible episode shape

সম্ভাব্য flow: Opening movement → Question → Investigation → Technical revelation → Consequence → Forward pull.

এটি mandatory formula নয়। কোনো episode action, aftermath, conversation বা discovery দিয়ে শুরু হতে পারে।

## 7. Learning connection

প্রয়োজন অনুযায়ী আলাদা artifact:
- Concept Note
- Visual Walkthrough
- Safe Experiment
- Lab Specification
- Synthetic Evidence Pack
- Threat Model
- Code Review Exercise
- Detection / Incident Response Exercise
- Further Reading

সব episode-এ সব artifact লাগবে না।

## 8. Character continuity

World Bible তৈরি হলে সেটি approved fact-এর source হবে। Episode লেখার আগে character কী জানে, কী জানে না, কোন evidence দেখেছে, কোন hypothesis ভুল হয়েছে, তার skill/limitation ও relationship state পরীক্ষা করো।

## 9. Image direction

Image scene-কে উন্নত করলে placeholder ও English generation prompt দাও। Approved world reference ছাড়া character-এর face, costume বা signature design স্থির করবে না। Format docs/VISUAL-DESIGN-GUIDELINES.md-এ।

## 10. Review checklist

- [ ] গল্পটি কি নিজে থেকেই পড়তে আগ্রহ তৈরি করে?
- [ ] চরিত্ররা কি নিজেদের উদ্দেশ্যে কাজ করছে?
- [ ] Scene-এ conflict, change বা discovery আছে?
- [ ] Mystery clue fair এবং payoff plausible?
- [ ] Technical detail স্বাভাবিকভাবে এসেছে?
- [ ] Observation ও hypothesis আলাদা?
- [ ] Classroom language এড়ানো হয়েছে?
- [ ] Bengali prose স্বাভাবিক?
- [ ] Learning artifact optional ও আলাদা?
- [ ] Visual বোঝাপড়া বা atmosphere উন্নত করছে?
- [ ] Safety boundary অক্ষুণ্ণ?
