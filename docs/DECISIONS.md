# Project Decisions

এখানে approved decision ও open decision রাখা হবে। User approval ছাড়া proposed idea-কে approved decision হিসেবে লিখবে না।

## Approved decisions

### D-001 — Story-first
**Decision:** Primary experience হবে Cyber Security Mystery Thriller novel; পাঠক গল্প পড়তে আসবে, শেখার বাধ্যবাধকতা নিয়ে নয়।  
**Rationale:** Narrative engagement-ই reader-এর প্রবেশদ্বার।

### D-002 — Concept-first, tool-second
**Decision:** Tool count বা tool-building progression organizing principle নয়। Concept, system visualization, evidence ও engineering judgment অগ্রাধিকার পাবে।  
**Rationale:** Professional security knowledge শুধু tool implementation দিয়ে মাপা যায় না।

### D-003 — Visualization-led
**Decision:** Flowchart, sequence, architecture, data-flow, state, timeline, table ও annotated example প্রয়োজনমতো ব্যবহার হবে। Narrative image-এর জন্য placeholder ও generation prompt থাকবে।  
**Rationale:** Complex system-এর mental model দৃশ্যমান করা।

### D-004 — Bengali-first
**Decision:** README, instructions, guidelines, templates ও explanatory prose বাংলা; technical terms, code ও machine-readable values English।  
**Rationale:** Review সহজ ও technical precision অক্ষুণ্ণ রাখা।

### D-005 — No world canon in foundation
**Decision:** Foundation কোনো character, setting, plot, villain motive বা AI system স্থির করবে না।  
**Rationale:** World-building আলাদা phase-এ হবে।

### D-006 — Optional learning path
**Decision:** Novel পড়তে Lab বাধ্যতামূলক নয়; Lab করতে Novel বাধ্যতামূলক নয়।  
**Rationale:** Reader autonomy।

### D-007 — Safety by design
**Decision:** Practical exercise local, synthetic, intentionally vulnerable বা explicitly authorized environment-এ সীমিত।  
**Rationale:** Responsible security practice।

### D-008 — Git history preservation
**Decision:** নতুন foundation tree পুরোনো content প্রতিস্থাপন করবে, কিন্তু Git history rewrite/delete করবে না।  
**Rationale:** Reviewable reset ও historical traceability।

### D-009 — Initial DC and Marvel character usage
**Decision:** প্রাথমিক creative development-এ DC ও Marvel-এর পরিচিত character ও নাম ব্যবহার করা হবে। এই পর্যায়ে এটি user-approved creative direction; পূর্ণ character canon নয়। ভবিষ্যতে original-character adaptation করা যেতে পারে।  
**Rationale:** পরিচিত character-এর মাধ্যমে reader engagement তৈরি করা।  
**Consequences:** Public বা commercial release-এর আগে copyright, trademark, fan-fiction scope ও licensing review করতে হবে।

### D-010 — Multi-POV storytelling
**Decision:** গল্প Peter-কেন্দ্রিক হবে না; গুরুত্বপূর্ণ character-দের নিজস্ব POV, objective, knowledge, motivation, limitation ও progression থাকবে।  
**Rationale:** একই cyber conflict-এর attacker, defender, investigator ও AI perspective দেখানো।

### D-011 — Hybrid POV structure
**Decision:** সাধারণত chapter একজন character-এর POV অনুসরণ করবে; প্রয়োজনে একই chapter-এর মধ্যে scene পরিবর্তন করে অন্য character-এর POV দেখানো যাবে।  
**Rationale:** Narrative control বজায় রেখে suspense, dramatic irony ও conflicting interpretation তৈরি করা।

### D-012 — Peter as the reader's primary anchor
**Decision:** Peter / Spider পাঠকের প্রধান learning anchor হবে, কিন্তু একমাত্র protagonist বা learning source নয়। Peter একজন নবীন hacker হিসেবে প্রয়োজন অনুযায়ী শিখবে, ভুল করবে, পরীক্ষা করবে এবং ধীরে ধীরে capability বাড়াবে।  
**Rationale:** পাঠকের সঙ্গে একটি accessible learning journey তৈরি করা, কিন্তু universe-কে এক চরিত্রে সীমাবদ্ধ না রাখা।

### D-013 — Learning from multiple character perspectives
**Decision:** Hero, villain, investigator, engineer ও AI character-এর কাজের progression থেকেও পাঠক শিখবে। Offensive, defensive, investigative, engineering ও AI/system perspective পুরো project-এ meaningfulভাবে থাকবে।  
**Rationale:** Cyber Security-কে একাধিক দৃষ্টিকোণ থেকে বোঝা।

### D-014 — Character-linked study materials
**Decision:** কোনো character প্রয়োজন অনুযায়ী কোনো বিষয় পড়তে শুরু করলে পাঠকের জন্য সেই learning journey-এর সঙ্গে যুক্ত detailed study materials উপস্থাপন করা যাবে। Novel classroom lecture হবে না; গভীর explanation আলাদা learning artifact-এ থাকবে।  
**Rationale:** গল্পের কৌতূহল থেকে theory শেখার স্বাভাবিক সেতু তৈরি করা।

### D-015 — Knowledge-first, solution-discovery-driven learning
**Decision:** পাঠককে problem বোঝা ও independently solve করার জন্য পর্যাপ্ত theory, system model, evidence ও resources দেওয়া হবে; complete solution আগেভাগে spoon-feed করা হবে না। প্রয়োজন হলে initial walkthrough ও resource guidance থাকবে।  
**Rationale:** Independent problem-solving ও engineering judgment তৈরি করা।

### D-016 — Resource and library guidance when useful
**Decision:** কোনো walkthrough বা experiment-এর জন্য library, framework বা existing utility প্রাসঙ্গিক হলে সেটি suggest করা হবে, সঙ্গে তার উদ্দেশ্য ও documentation-এর দিকনির্দেশনা থাকবে। Tool/library suggestion বাধ্যতামূলক curriculum নয়।  
**Rationale:** পাঠককে অপ্রয়োজনীয় implementation burden না দিয়ে বাস্তব problem exploration-এ সহায়তা করা।

### D-017 — Universe-wide tool development
**Decision:** Tool development শুধু Peter-এর জন্য সীমাবদ্ধ নয়। বিভিন্ন character-এর বাস্তব investigative বা engineering need অনুযায়ী tool তৈরি, ব্যবহার, adapt বা improve হতে পারে। পাঠককে প্রতিটি tool নিজে তৈরি করতে বাধ্য করা হবে না।  
**Rationale:** Tool হলো problem-solving-এর instrument; project-এর learning objective tool count বা code volume নয়।

### D-018 — Cumulative learning and knowledge reuse
**Decision:** আগে শেখা knowledge পরবর্তী incident ও learning activity-তে পুনরায় ব্যবহার, নতুন concept-এর সঙ্গে integrate এবং ক্রমশ জটিল পরিস্থিতিতে প্রয়োগ করতে হবে।  
**Rationale:** বিচ্ছিন্ন lesson নয়, connected mental model ও durable competency তৈরি করা।

### D-019 — Persistent reader learning context
**Decision:** পাঠকের পূর্বে শেখা concept, notes, reference, experiment ও reusable knowledge পরবর্তী learning activity-তে কাজে লাগবে। প্রতিটি chapter-এ learning শূন্য থেকে শুরু হবে না।  
**Rationale:** Reader progression-কে ধারাবাহিক রাখা এবং আগের learning-এর বাস্তব মূল্য তৈরি করা।


### D-020 — Broad Cyber Security + Systems Engineering Education
**Decision:** Project-এর learning scope শুধু Cyber Security-তে সীমাবদ্ধ থাকবে না। Computing Foundations, Systems & Networking, Software & Application Engineering, Cyber Security Core, Advanced Security & Investigation এবং Emerging & Specialized Systems-সহ বিস্তৃত, interconnected knowledge ecosystem গড়ে তোলা হবে। Systems Thinking, Psychology & Human Factors এবং Engineering Judgment cross-cutting capability হিসেবে থাকবে।  
**Rationale:** পাঠককে শুধু security tool ব্যবহারকারী নয়, system-level reasoning করতে সক্ষম Systems-minded Security Engineer হিসেবে গড়ে তোলার foundation দেওয়া।  
**Consequences:** Domain layer rigid syllabus order নয়। Broad foundation-এর পর T-shaped specialization, prerequisite mapping, cumulative learning এবং cross-domain knowledge integration অগ্রাধিকার পাবে। বিস্তারিত `docs/LEARNING-DOMAINS.md`-এ।

### D-021 — Fictional Threat, Real-world Engineering
**Decision:** গল্পে প্রয়োজন অনুযায়ী fictional বা futuristic technology ও threat আনা যাবে; তবে সেগুলো বোঝা, investigate, disable, contain বা defend করার engineering reasoning বাস্তব জগতের যাচাইযোগ্য principle-এর ওপর দাঁড়াবে। Fictional mechanism ও বাস্তব technology স্পষ্টভাবে আলাদা রাখতে হবে।  
**Rationale:** গল্পের সম্ভাবনা বাড়িয়েও পাঠকের বাস্তব engineering knowledge ও technical trust অক্ষুণ্ণ রাখা।  
**Consequences:** Fictional system-এর architecture, dependency, trust boundary, failure mode ও limitation internally consistent হবে। বাস্তব engineering principle নাটকীয়তার জন্য বিকৃত করা যাবে না। ক্ষতিকর operational construction বা compromise guide নয়, safe analysis ও defensive engineering-এ focus থাকবে।

## Open decisions

পরবর্তী planning phase-এ স্থির হবে:

- Universe-এর নাম, branding, setting ও timeline।
- Real-world technology এবং fictional/future technology-এর সুনির্দিষ্ট অনুপাত।
- Character roster-এর পূর্ণতা, personality, backstory, relationship ও capability।
- Central mystery, antagonist motive এবং long-term story arc।
- Volume, season ও episode structure।
- Learning roadmap-এর chapter-level sequence, prerequisite detail ও specialization depth।
- Knowledge Dependency Graph-এর concrete schema, implementation ও maintenance process।
- Learning activity-এর difficulty, hints, validation, assessment ও reference-solution format।
- Tool inventory এবং কোন tool implementation পাঠক explore করবে।
- Narrative image style ও approved references।
- AI authoring, technical verification ও independent review workflow।
- Public release, fan-fiction scope, original adaptation ও licensing strategy।

## Decision update format

- ID: D-XXX
- Status: Proposed / Approved / Superseded
- Decision:
- Rationale:
- Consequences:
- Approved by:
- Date:

Superseded decision মুছবে না; নতুন decision দিয়ে reference করবে।


### D-022 — Integrated narrative learning
**Decision:** Learning experience-এর মূল flow হবে **Story → Curiosity → Knowledge → Exploration → Discovery → Engineering Judgment**। Character-এর study, research, investigation, experiment বা tool-building-এর প্রয়োজন গল্পে তৈরি হবে; তার সঙ্গে সম্পর্কিত detailed learning material গল্পের narrative sequence-এর মধ্যেই উপস্থাপিত হবে। Learning source শুধু Peter নয়; বর্তমান POV character-এর knowledge, objective, কাজ ও context অনুযায়ী learning material তৈরি হবে। Novel ও learning material independently readable থাকবে।
**Rationale:** পাঠক যেন গল্পের বাইরে হঠাৎ classroom-এ চলে গেছে এমন অনুভব না করে; learning গল্পের অভিজ্ঞতার অংশ হয়।
**Consequences:** Learning material আলাদা file বা section-এ থাকতে পারে, কিন্তু reader-facing sequence-এ তা সংশ্লিষ্ট story moment-এর সঙ্গে যুক্ত থাকবে। Character-এর POV ও knowledge boundary বজায় রাখতে হবে।

### D-023 — Hybrid Knowledge Graph
**Decision:** Knowledge architecture হবে Hybrid Knowledge Graph। Graph-এ Domain, Concept ও Learning Objective (LO)-এর মতো typed knowledge node এবং একাধিক explicit relationship থাকবে। Concept ও LO আলাদা node type; একই concept-এর একটিই canonical identity থাকবে, যদিও তা একাধিক domain ও LO-এর সঙ্গে সম্পর্কিত হতে পারে।
**Rationale:** Technical knowledge-এর cross-domain reuse এবং learner capability-র objective-কে একই structure-এ প্রকাশ করা, কিন্তু তাদের semantics গুলিয়ে না ফেলা।
**Consequences:** Concept-to-Concept technical relationships এবং LO-to-LO prerequisite dependencies আলাদা relationship family হবে। Graph-এর exact schema ও implementation এখনো open।

### D-024 — Learning Objective to Concept relationship semantics
**Decision:** LO ও Concept-এর সম্পর্ক তিনভাবে শ্রেণিবদ্ধ হবে: **Required**, **Supporting** এবং **Related**। Required concept LO অর্জনের জন্য প্রয়োজনীয়; Supporting concept বোঝাপড়ায় সহায়তা করে; Related concept প্রাসঙ্গিক হলেও আবশ্যিক নয়। একই Concept ভিন্ন LO-তে ভিন্ন classification পেতে পারে। Related relationship prerequisite বোঝায় না।
**Rationale:** একটি concept-এর গুরুত্ব learning objective অনুযায়ী বদলাতে পারে; একে global fixed label দেওয়া যথাযথ।

### D-025 — Strict Learning Objective prerequisites
**Decision:** LO-to-LO prerequisite strict হবে। কোনো LO-এর prerequisite LO থাকলে learner-কে পরবর্তী LO-তে অগ্রসর হওয়ার আগে সেগুলো সম্পন্ন করতে হবে। Story chronology প্রয়োজন অনুযায়ী এমনভাবে সাজানো হবে, যাতে এই dependency বজায় থাকে।
**Rationale:** Advanced learning-এর আগে প্রয়োজনীয় foundation নিশ্চিত করা।
**Consequences:** Mandatory prerequisite subgraph acyclic হতে হবে। Technical Concept-to-Concept relationship prerequisite হিসেবে গণ্য হবে না; prerequisite কেবল LO-to-LO dependency-তে প্রকাশিত হবে।
