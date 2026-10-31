# AGENTS.md — AI Agent-এর বাধ্যতামূলক নির্দেশনা

এই repository-তে content তৈরি, পরিবর্তন বা review করার আগে এই ফাইল এবং সংশ্লিষ্ট source-of-truth document পড়ো।

## 1. Source of truth ও precedence

1. User-এর সর্বশেষ স্পষ্ট নির্দেশনা।
2. docs/PROJECT-CHARTER.md
3. docs/DECISIONS.md
4. docs/AUTHORING-GUIDELINES.md
5. docs/LEARNING-ARCHITECTURE.md
6. docs/VISUAL-DESIGN-GUIDELINES.md
7. docs/SECURITY-AND-SAFETY.md
8. docs/AI-WORKFLOW.md এবং সংশ্লিষ্ট template।

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
