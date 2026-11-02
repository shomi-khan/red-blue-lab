# AGENTS.md — AI Agent-এর বাধ্যতামূলক নির্দেশনা

এই repository-তে content তৈরি, পরিবর্তন বা review করার আগে এই ফাইল এবং সংশ্লিষ্ট source-of-truth document পড়ো।

## 1. Source of truth ও precedence

1. User-এর সর্বশেষ স্পষ্ট নির্দেশনা।
2. docs/PROJECT-CHARTER.md
3. docs/DECISIONS.md
4. docs/AUTHORING-GUIDELINES.md
5. docs/LEARNING-ARCHITECTURE.md
6. docs/GRAPH-ARCHITECTURE.md
7. docs/VISUAL-DESIGN-GUIDELINES.md
8. docs/SECURITY-AND-SAFETY.md
9. docs/AI-WORKFLOW.md এবং সংশ্লিষ্ট template।

তথ্য অনুপস্থিত থাকলে গুরুত্বপূর্ণ world-building decision নিজে থেকে নিও না। Unknown ও proposed বিষয় আলাদা করে human review চাও।

## 2. কাজ শুরুর আগে

- Request, deliverable ও scope বুঝে নাও।
- সংশ্লিষ্ট source documents পড়ো।
- Existing canon, chronology, character knowledge ও dependencies পরীক্ষা করো।
- Confirmed, proposed, unresolved ও unknown তথ্য আলাদা করো।
- Technical, narrative, visual ও safety impact বিবেচনা করো।
- Scope conflict থাকলে কাজের আগে সবচেয়ে প্রয়োজনীয় clarification চাও।

## 3. Non-negotiable principles

- **Story-first:** Novel-কে tutorial-এর wrapper বানাবে না।
- **Concept-first:** আগে system model, data flow, trust boundary, protocol, threat, failure ও evidence বোঝাও।
- **Tool-second:** Tool কেবল বাস্তব investigative বা engineering need থাকলে তৈরি হবে।
- **Visualize:** Diagram, flowchart, sequence, state model, table বা annotated example prose-এর চেয়ে কার্যকর হলে ব্যবহার করো।
- **Optional learning:** গল্প পড়তে lab বাধ্যতামূলক নয়; lab করতে গল্প বাধ্যতামূলক নয়।
- **Evidence:** Observation, hypothesis, inference, confirmed finding ও unknown গুলিয়ে ফেলবে না।

## 4. Narrative quality

- চরিত্রকে technical concept বোঝানোর mouthpiece বানাবে না।
- Character-এর motive, limitation, ভুল, দ্বিধা, সম্পর্ক ও consequence থাকবে।
- Tension তৈরি হবে uncertainty, conflicting evidence, risk, deadline ও competing incentives থেকে।
- একই scene formula বা cliffhanger বারবার ব্যবহার করবে না।
- Filler বা artificial word count নয়।
- Continuity না পড়ে নতুন canon invent করবে না।
- Hypothesis-কে evidence হিসেবে উপস্থাপন করবে না।

## 5. Technical correctness

- Protocol, OS, architecture, cryptography, AI ও security behavior যাচাই ছাড়া দাবি করবে না।
- Drama তৈরির জন্য technical law বদলাবে না।
- Diagram ও prose একই behavior দেখাবে।
- Logs, packets, outputs, vulnerabilities ও fixtures consistent হবে।
- Limitation, uncertainty ও failure mode প্রকাশ করবে।
- Simplification করলে label করো।

## 6. Language

- Explanatory content ও narrative বাংলা।
- Technical terms, code, command, flags, API, protocol, identifier ও schema field English-এ।
- Natural Bengali prose; অপ্রয়োজনীয় English sentence নয়।
- প্রথমবার term এলে ছোট বাংলা ব্যাখ্যা দাও।
- Technical precision নষ্ট করে জোরপূর্বক অনুবাদ করবে না।

## 7. Visuals

- Concept বোঝাতে Mermaid, flowchart, sequence, architecture, state, timeline বা table ব্যবহার করো।
- Narrative image সত্যিই scene উন্নত করলে placeholder ও detailed English prompt দাও।
- AI-generated image-কে accurate architecture বা technical evidence হিসেবে ব্যবহার করবে না।
- World Bible অনুমোদিত হওয়ার আগে character design স্থির করবে না।
- Decorative visual যোগ করবে না।

## 8. Safety

docs/SECURITY-AND-SAFETY.md বাধ্যতামূলক। Real unauthorized target, credential theft, persistence, stealth, malware deployment বা ক্ষতিকর operational walkthrough তৈরি করবে না। Safe local simulation, synthetic evidence, detection ও mitigation-কে অগ্রাধিকার দাও।

## 9. AI workflow

1. Understand: request ও canon পড়ো।
2. Plan: deliverable, dependency, uncertainty ও review criteria নির্ধারণ।
3. Propose: বড় plot বা architecture পরিবর্তনের আগে review চাও।
4. Draft: approved facts ও template অনুসরণ।
5. Verify: narrative, technical, visual, continuity, language ও safety review।
6. Report: কী বদলেছে, কী যাচাই হয়েছে, কী বাকি এবং কোন human decision প্রয়োজন তা জানাও।

## 10. নিষিদ্ধ অনুমান

- User approval ছাড়া DC character, setting, relationship বা plot-কে final canon ধরবে না।
- প্রতিটি episode-এ tool, diagram, image, quiz বা lab বাধ্যতামূলক করবে না।
- Tool count-কে learning quality-এর মাপকাঠি করবে না।
- Professional competency-কে নির্দিষ্ট tool বা volume count-এ সীমাবদ্ধ করবে না।
- Research বা test না করে verified বলবে না।

## 11. Completion checklist

- [ ] User request পূরণ।
- [ ] Story-first ও concept-first philosophy অক্ষুণ্ণ।
- [ ] Bengali prose, English technical terms।
- [ ] Technical claims accurate ও evidence-aware।
- [ ] Visuals প্রয়োজনমতো, decorative নয়।
- [ ] Safety boundary অক্ষুণ্ণ।
- [ ] Canon ও continuity ভাঙেনি।
- [ ] Unknown ও human decision স্পষ্ট।
- [ ] Verification status সত্যভাবে জানানো হয়েছে।


## 12. Knowledge ও Learning Graph rules

- Knowledge Graph, Learning Graph এবং Reader Learning Track-কে আলাদা concern হিসেবে রাখো।
- Graph-এর canonical contract `docs/GRAPH-ARCHITECTURE.md`; schema ও YAML catalog পরিবর্তনের আগে সেটি পড়ো।
- Markdown হলো narrative ও learning content body-এর canonical source। `knowledge/graph.yaml` হলো Knowledge Graph metadata/relationships-এর authoritative source; `learning/graph.yaml` হলো Learning Graph catalog/links-এর authoritative source। Markdown থেকে YAML graph-কে নীরবে infer বা regenerate কোরো না।
- Learning Node কেবল Peter-এর জন্য নয়; reader-facing reusable learning artifact।
- Learning Node schema বা catalog-এ publication status/workflow যোগ কোরো না; পূর্বের Learning Node-গুলো published হিসেবে গণ্য।
- Reader-specific progress, notes বা identity shared graph catalog-এ commit কোরো না।

### 12.1 বাধ্যতামূলক content authoring workflow

যখনই নতুন reader-facing learning content তৈরি বা বিদ্যমান learning content পরিবর্তন করবে, নিচের সম্পূর্ণ workflow অনুসরণ করো। শুধু Markdown file তৈরি/সম্পাদনা করে কাজ শেষ হয়েছে বলে গণ্য করবে না।

1. **Read current state:** `knowledge/graph.yaml`, `learning/graph.yaml`, সংশ্লিষ্ট JSON Schema, `docs/GRAPH-ARCHITECTURE.md` এবং সম্পর্কিত existing Markdown content পড়ো।
2. **Identify knowledge scope:** Content কোন existing Domain, Concept ও Learning Objective ব্যবহার করছে তা নির্ধারণ করো। একই অর্থের Node আগে থেকেই থাকলে duplicate Node তৈরি কোরো না। নতুন Node কেবল নতুন, independently meaningful knowledge-এর জন্য।
3. **Run Knowledge Coverage Analysis:** প্রতিটি প্রাসঙ্গিক Concept-এর আগের `explains` links ও `content_anchor` পরীক্ষা করো। Anchor-এর target section বাস্তবে আছে কি না এবং section-টি Concept-এর scope যথাযথভাবে explain করে কি না, Markdown খুলে যাচাই করো। Metadata একা যথেষ্ট প্রমাণ নয়। অনিশ্চিত হলে explained ধরে নিও না; gap/review-needed হিসেবে চিহ্নিত করো।
4. **Plan reuse and gaps:** আগে explain করা scope পুনরাবৃত্তি না করে যথাযথ পুরোনো Learning Node-এ `references` link দাও। নতুন বা আলাদা scope হলে সেটি নতুন content-এ explain করো। Parent Concept ও child Concept-এর explanation আলাদাভাবে বিবেচনা করো।
5. **Author content:** Approved Bengali-first authoring ও technical/safety rules মেনে Markdown content তৈরি বা update করো। Content-এর section heading স্থিতিশীল ও অর্থবহ রাখো, যাতে anchor নির্ভরযোগ্য হয়।
6. **Update Knowledge Graph when needed:** নতুন Domain/Concept/LO সত্যিই প্রয়োজন হলে `knowledge/graph.yaml`-এ stable ID-সহ যোগ করো। প্রাসঙ্গিক typed relationship যোগ বা update করো। Existing Node-এর identity অকারণে বদলাবে না।
7. **Update Learning Graph:** প্রতিটি নতুন বা পরিবর্তিত reader-facing Learning artifact-এর জন্য `learning/graph.yaml`-এ Learning Node create/update করো। সঠিক `content_ref`, title, type ও প্রাসঙ্গিক metadata দাও। প্রতিটি relevant Knowledge Node-এর সঙ্গে সঠিক typed relationship দাও। প্রতিটি `explains` link-এ বাস্তব, valid `content_anchor` আবশ্যক।
8. **Verify graph consistency:** JSON Schema অনুযায়ী data shape; সব Node ও relationship ID unique; duplicate links নেই; সব content path বিদ্যমান; সব cross-file Node reference resolve করে; relationship-এর source/target type বৈধ; `parent_of` ও mandatory LO prerequisite DAG acyclic; technical relationship cycle অনুমোদিত; প্রতিটি `explains` anchor বিদ্যমান এবং সংশ্লিষ্ট Concept-কে বাস্তবে cover করে। Reader Track schema-তে catalog-এর বাইরে Learning Node reference নেই।
9. **Report the graph changes:** Final response-এ আলাদা করে উল্লেখ করো কোন Markdown file বদলেছে, কোন Knowledge Node তৈরি/পরিবর্তিত হয়েছে, কোন Learning Node তৈরি/পরিবর্তিত হয়েছে, কোন relationship যোগ/পরিবর্তিত হয়েছে, কোন পূর্বের content reference করা হয়েছে এবং কোন validation বাস্তবে সম্পন্ন/অসম্পন্ন।

যদি কাজটি কেবল narrative content হয় এবং কোনো reader-facing learning artifact বা Knowledge Graph scope পরিবর্তন না করে, অকারণে Learning Node বা graph edge তৈরি কোরো না। তবে এমন সিদ্ধান্তের কারণ report করো।

### 12.2 Validation discipline

- Structural validation এবং semantic validation আলাদা করে report করো।
- JSON Schema parse/validation, YAML parse এবং cross-file semantic checks বাস্তবে না চালালে সেগুলো completed বলে দাবি কোরো না।
- কোনো automated validator না থাকলে repository files ও relationships সরাসরি inspect করে Agent হিসেবে manual check করো; manual check-কে automated validation বলে উপস্থাপন কোরো না।
