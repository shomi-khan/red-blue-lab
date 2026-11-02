# AI Agent Workflow

AI agent research assistant, story editor, technical reviewer ও content drafter হতে পারে। কিন্তু নিজে থেকে canon বা বড় project decision অনুমোদন করতে পারবে না।

## 1. Role separation

| Role | দায়িত্ব |
|---|---|
| User / Project owner | Canon, scope ও final approval |
| Story planner | Mystery arc, scene purpose, pacing |
| Narrative author | Approved plan থেকে Bengali prose |
| Technical researcher | Protocol ও security claim যাচাই |
| Learning designer | Concept ও competency design |
| Visual designer | Diagram ও image prompt |
| Reviewer | Narrative, technical, visual, safety ও language review |

এক agent একাধিক role নিতে পারে, কিন্তু নিজের draft নিজে review করাকে independent verification বলবে না।

## 2. Workflow

### Planning
Request interpretation, relevant source, known facts, unknowns, proposed structure, risk ও approval requirement জানাও। বড় plot/world decision আগে review-এ দাও।

### Story drafting
1. Approved world/canon পড়ো।
2. Relevant episode ও continuity পড়ো।
3. Scene purpose, POV, chronology, character knowledge ও clue plan করো।
4. Technical claim যাচাই করো।
5. Bengali prose লেখো।
6. Image দরকার হলে placeholder ও prompt দাও।
7. Narrative, technical, continuity ও safety review করো।

### Learning artifact
1. Narrative event ও concept-এর সম্পর্ক নির্ধারণ।
2. Prerequisite ও reader knowledge যাচাই।
3. Mental model তৈরি।
4. Visual নির্বাচন।
5. Example/experiment/lab প্রয়োজন কি না সিদ্ধান্ত।
6. Verification ও limitation যোগ।
7. Tool সত্যিই দরকার কি না পুনর্বিবেচনা।
8. নতুন বা পরিবর্তিত reader-facing Learning Node হলে `AGENTS.md`-এর বাধ্যতামূলক Knowledge Coverage Analysis workflow অনুসরণ করো। Existing Knowledge ও Learning Graph এবং সংশ্লিষ্ট Markdown content inspect করে আগে explain করা scope পুনরাবৃত্তি এড়াও।
9. প্রয়োজন অনুযায়ী `knowledge/graph.yaml`-এ Knowledge Node/relationship এবং `learning/graph.yaml`-এ Learning Node/Knowledge link update করো। প্রতিটি `explains` link-এর `content_anchor` বাস্তব section-এ resolve করে section-টি সংশ্লিষ্ট Concept সত্যিই explain করে কি না যাচাই করো।
10. `docs/GRAPH-ARCHITECTURE.md`-এর relationship endpoint, DAG ও cross-file validation rules মেনে graph consistency যাচাই করো। Structural ও semantic validation কোনটি বাস্তবে করা হয়েছে তা আলাদা করে report করো.
11. Narrative-only change হলে অকারণে Learning Node বা graph edge তৈরি কোরো না; কেন graph update প্রয়োজন হয়নি তা report করো।

### Review
Narrative, character, mystery, technical correctness, learning depth, visual accuracy, Bengali quality, safety ও continuity আলাদা করে review করো। Concrete issue, impact, location ও suggested fix দাও।

## 3. Research rules

- Protocol ও standard-এর primary specification অগ্রাধিকার।
- Vulnerability-তে vendor advisory, CVE record, project documentation ও reputable research ব্যবহার।
- পরিবর্তনশীল technology-তে research date ও source record করো।
- Fiction-এর জন্য technical claim বানিয়ে ফেলো না।
- Source না পেলে unverified/proposed label করো।
- Research citation reference artifact-এ দাও; novel-কে academic paper বানিও না।

## 4. Canon management

World Bible approved fact-এর source হবে। Agent approved fact বদলাবে না, proposed idea-কে canon বানাবে না, chronology contradiction লুকাবে না, character knowledge limit অতিক্রম করাবে না এবং অনুমতি ছাড়া unresolved mystery reveal করবে না।

Conflict পেলে draft থামিয়ে conflict report করো।

## 5. Quality gates

1. **Narrative:** পাঠক কি গল্প পড়তে চাইবে, নাকি lesson পড়ছে বলে মনে হবে?
2. **Technical:** Claim accurate, contextualized ও limitation-aware?
3. **Learning:** Usable mental model তৈরি হয়েছে, নাকি শুধু jargon?
4. **Visual:** Diagram বোঝায়? Image narrative-এ মূল্য যোগ করে?
5. **Safety:** Exercise authorized, bounded ও non-destructive?
6. **Continuity:** Approved world facts ও chronology মেনে চলে?

Critical gate fail করলে ready বলবে না।

## 6. Change management

- Foundation rule বদলানোর আগে rationale ও impact জানাও।
- User approval ছাড়া core philosophy বদলাবে না।
- বড় পরিবর্তন cohesive PR-এ রাখো।
- PR description বাংলায়: summary, rationale, changed files, validation, known gaps ও human review points।
- যাচাই না করা test বা link verified বলবে না।

## 7. Agent honesty

কাজ শেষে জানাও কী তৈরি হয়েছে, কোন source অনুসরণ, কী যাচাই, কী যাচাই হয়নি এবং কোন ambiguity বা human decision বাকি।
