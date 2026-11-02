# Knowledge ও Learning Graph Architecture

> Status: User-approved architecture
> Scope: Knowledge Graph, Learning Graph, typed relationships, coverage calculation এবং reader-specific learning progress
> এই document graph-এর data contract নির্ধারণ করে। এটি কোনো application runtime বা Learning Path Generator implementation নয়।

## 1. তিনটি আলাদা দায়িত্ব

| অংশ | কী সংরক্ষণ করে | কী করে না |
|---|---|---|
| **Knowledge Graph** | Domain, Concept, Learning Objective এবং তাদের জ্ঞানগত সম্পর্ক | Reader-এর progress বা learning route সংরক্ষণ করে না |
| **Learning Graph** | Tutorial, Note, Investigation, Experiment ইত্যাদি Learning Node এবং Knowledge Node-এর সঙ্গে typed link | কোনো নির্দিষ্ট reader-এর completion state রাখে না |
| **Reader Learning Track** | একজন reader কোন Learning Node বেছে নিয়েছে, কোন ক্রমে রাখছে এবং তার progress | Knowledge Node-এর explained status পরিবর্তন করে না |

একই Learning Node বহু reader ব্যবহার করতে পারবে। প্রত্যেক reader-এর progress আলাদা থাকবে।

Learning source শুধু Peter নয়। Story-এর যেকোনো POV character-এর study, research, investigation, design বা experiment থেকে reader-facing Learning Node তৈরি হতে পারে। Character-এর story journey এবং reader-এর ব্যক্তিগত progress আলাদা concern।

## 2. Knowledge Graph

### 2.1 Node types

- **Domain:** বড় knowledge area; একটি Concept একাধিক Domain-এর সঙ্গে যুক্ত হতে পারে।
- **Concept:** independently meaningful ও reusable knowledge unit। যেমন TCP, Session Authentication বা Certificate Authority।
- **Learning Objective (LO):** reader কী ব্যাখ্যা, trace, analyze, test, design বা evaluate করতে পারবে তার নির্দিষ্ট statement।

Concept-এর canonical identity একটিই থাকবে। একই Concept একাধিক Domain, LO এবং Learning Node-এর সঙ্গে যুক্ত হতে পারে।

### 2.2 Granularity

Concept-কে যতটা সম্ভব meaningful ও reusable ছোট unit-এ ভাগ করো, কিন্তু প্রতিটি শব্দ, field বা atomic detail-এর জন্য আলাদা Node তৈরি কোরো না। আলাদা Node তৈরি করো যখন বিষয়টি নিজস্ব ব্যাখ্যা, reuse, relationship, experiment বা assessment পাওয়ার যোগ্য।

General Concept-এর নিজস্ব explanation তার scope-এই সীমাবদ্ধ থাকবে। উদাহরণস্বরূপ, `Authentication` Node-এ definition, purpose, high-level types ও general flow থাকবে। `Password Authentication` এবং `Session Authentication` আলাদা Concept Node হবে; parent Node-এর explanation-এ তাদের বিস্তারিত পুনরাবৃত্তি করা হবে না।

### 2.3 Hierarchy ও technical relationship আলাদা

একটি Concept একাধিক parent-এর অধীনে থাকতে পারে। তাই hierarchy strict tree নয়, DAG। `parent_of` relationship-এ cycle নিষিদ্ধ।

Technical relationship আলাদা family। যেমন `uses`, `contains`, `depends_on`, `interacts_with`, `implements`, `part_of`। এগুলোতে cycle থাকতে পারে এবং এগুলো hierarchy বা learning prerequisite বোঝায় না।

### 2.4 Learning Objective relationship

- **Required:** LO অর্জনের জন্য Concept জানা আবশ্যক।
- **Supporting:** Concept বোঝাপড়ায় সহায়তা করে, কিন্তু একা mandatory নয়।
- **Related:** Concept প্রাসঙ্গিক, কিন্তু prerequisite নয়।
- **Prerequisite:** LO-to-LO dependency। একটি LO অন্য LO-এর prerequisite হলে dependency graph acyclic হতে হবে।

Concept-to-Concept technical relationship থেকে learning prerequisite অনুমান করা যাবে না।

## 3. Explained status ও coverage

প্রতিটি Domain/Concept Node-এর `self_explained` একটি boolean:

- `false`: Node-এর নিজের scope এখনো সম্পূর্ণভাবে explain করা হয়নি।
- `true`: Node-এর নিজের scope-এর explanation সম্পূর্ণ এবং review করা হয়েছে।

Leaf Node-এর coverage তাই binary: 0% অথবা 100%। Parent Node-এর coverage নিজের explanation এবং direct child-দের coverage মিলিয়ে গণনা হবে।

ধরি:

- `self_explained` = false হলে 0, true হলে 1
- `child_coverage` = প্রতিটি child-এর coverage, 0–100 scale-এ
- `n` = direct child-এর সংখ্যা

```text
coverage_percentage =
  (100 * self_explained + sum(child_coverage))
  / (1 + n)
```

এটি আগের normalized formula-এরই 0–100 scale-এ প্রকাশ। Parent-এর নিজের explanation এবং প্রতিটি direct child সমান weight পায়। Child না থাকলে ফল 0% বা 100% হবে।

**Coverage মানে content coverage, reader mastery নয়।** এটি explanation-এর quality, correctness, retention বা কোনো reader-এর competency প্রমাণ করে না।

### 3.1 Explained status কীভাবে নির্ধারিত হবে

শুধু Learning Node-এর সঙ্গে link থাকলেই Knowledge Node explained হবে না। `self_explained: true` করার আগে:

1. Node-এর নিজস্ব scope-এর উপযুক্ত published Learning Node থাকতে হবে।
2. Learning Graph-এ সেই Learning Node থেকে Knowledge Node-এ `explains` relationship থাকতে হবে।
3. Relationship-এ নির্দিষ্ট content anchor থাকতে হবে।
4. Explanation review করে status explicitly update করতে হবে।

`introduces`, `demonstrates`, `applies`, `investigates` বা `references` link একা explained status তৈরি করে না।

### 3.2 Recalculation

কোনো Node যোগ হলে, `self_explained` বদলালে অথবা hierarchy edge বদলালে তার সব ancestor-এর coverage পুনরায় হিসাব হবে। DAG-এ একটি Node-এর একাধিক parent থাকতে পারে, তাই প্রত্যেক affected ancestor একবার করে update করতে হবে।

Coverage value derived data; YAML source-এ manually লিখে রাখা যাবে না। প্রয়োজনে tooling এটি calculate করে display/cache করতে পারে।

## 4. Learning Graph

### 4.1 Learning Node

Learning Node হলো reader-এর শেখার উপাদান, Knowledge Node নয়। প্রাথমিক `type`:

- `tutorial`
- `notes`
- `investigation`
- `planning`
- `experiment`
- `walkthrough`
- `lab`
- `reference`

প্রতিটি Learning Node একটি canonical Markdown content file-কে reference করবে। Learning Node একটি বা একাধিক Knowledge Node-এর সঙ্গে যুক্ত হতে পারে; একই Knowledge Node-কে একাধিক Learning Node explain, demonstrate বা apply করতে পারে।

### 4.2 Learning-to-Knowledge relationship

প্রতিটি link-এ explicit `relationship` থাকবে:

| Relationship | অর্থ |
|---|---|
| `introduces` | প্রথমবার ধারণার সঙ্গে পরিচয় করায় |
| `explains` | ধারণাটি সরাসরি ব্যাখ্যা করে |
| `demonstrates` | Diagram, example বা walkthrough দিয়ে দেখায় |
| `applies` | বাস্তব scenario-তে প্রয়োগ করে |
| `investigates` | Investigation-এর মাধ্যমে ধারণাটি অনুসন্ধান করে |
| `plans` | Design বা planning context-এ ধারণাটি ব্যবহার করে |
| `references` | পুনরায় ব্যাখ্যা না করে আগের explanation/reference-এর দিকে নির্দেশ করে |

প্রয়োজনে link-এ `content_anchor` থাকবে, যেমন Markdown heading। এতে কোন section কোন Concept cover করে তা বোঝা যায়।

### 4.3 Duplicate explanation এড়ানো

কোনো Concept-এর scope একবার যথাযথভাবে explain হলে পরবর্তী Learning Node-এ একই explanation আবার লিখবে না। নতুন material প্রয়োজন হলে সেটি নতুন context, application, evidence, investigation বা deeper scope যোগ করবে এবং যথাযথ relationship ব্যবহার করবে।

আগের explanation পুনরায় ব্যবহার করতে `references` link দাও। নতুন Learning Node তৈরি হলেই নতুন Knowledge Node তৈরি করতে হবে না।

## 5. Reader Learning Track

Reader Learning Track হলো একজন reader-এর নিজস্ব selection ও progress। এটি Learning Graph-এর catalog নয়, বরং catalog-এর ওপর reader-specific state।

একটি track-এ reader-এর নির্বাচিত Learning Node-গুলো থাকবে। Reader নিজের ক্রম নির্ধারণ, bookmark, শুরু, complete বা skip করতে পারবে। Future Learning Path Generator LO prerequisite ও Learning Node mapping ব্যবহার করে suggested track দিতে পারে; graph structure নিজে route generator নয়।

প্রাথমিক progress state:

- `planned`
- `in_progress`
- `completed`
- `skipped`

একজন reader-এর একাধিক track থাকতে পারে। Track-এর item order reader-specific হবে।

**Privacy boundary:** Reader ID, progress, notes বা activity data repository-র shared YAML graph file-এ রাখা যাবে না। ভবিষ্যৎ application এগুলো reader-specific persistence layer-এ রাখবে। এই repository-তে শুধু data contract/schema থাকবে।

Reader-এর completion Knowledge Node-এর `self_explained` বা graph coverage বদলাবে না। একজন reader কোনো material complete করলেই project-এর content coverage পরিবর্তিত হয় না।

## 6. Storage ও source of truth

- `knowledge/graph.yaml`: Knowledge Graph-এর node ও relationship catalog।
- `learning/graph.yaml`: Learning Node catalog এবং Knowledge Node-এর সঙ্গে typed link।
- `schemas/*.schema.json`: YAML parse করার পর graph ও reader-track data validate করার JSON Schema contract।
- Markdown: Novel, Tutorial, Note, Investigation, Lab ও অন্য learning content-এর canonical body।
- Reader Learning Track: ভবিষ্যতে reader-specific persistence; repository-তে কোনো ব্যক্তিগত progress data নয়।

Graph YAML content-এর duplicate নয়; এটি stable ID, metadata, reference এবং relationship সংরক্ষণ করে। Markdown-এ content থাকবে। JSON Schema data shape validate করবে; cross-file semantic validation-এর জন্য অতিরিক্ত validator প্রয়োজন।

## 7. Validation rules

Graph update করার সময় অন্তত নিচের checks করতে হবে:

1. প্রতিটি graph-এর `schema_version` supported।
2. Node ID ও relationship ID graph-এর মধ্যে unique।
3. প্রতিটি edge-এর source ও target বিদ্যমান Node-কে reference করে।
4. Relationship type-এর source/target node type বৈধ।
5. `parent_of` এবং mandatory LO prerequisite graph acyclic।
6. Technical relationship cycle অনুমোদিত।
7. `self_explained: true` হলে অন্তত একটি published `explains` link ও valid content anchor থাকতে হবে।
8. `explains` link-এর target Knowledge Node হতে হবে; source published Learning Node হতে হবে।
9. `content_ref` path repository-তে বিদ্যমান canonical Markdown file-কে নির্দেশ করবে।
10. Reader Track-এর Learning Node ID বিদ্যমান ও reader-এর জন্য available হতে হবে।

JSON Schema structural validation করবে। Unique cross-file reference, relationship endpoint type, DAG cycle এবং published content reference-এর মতো rule custom semantic validator-এ পরীক্ষা করতে হবে।

## 8. Incremental evolution

পুরো Knowledge Graph, Learning Graph বা Learning Track আগে থেকে তৈরি করতে হবে না।

- Story বা research প্রয়োজন তৈরি করলে নতুন Learning Node যোগ করো।
- Learning Node প্রয়োজন হলে নতুন Knowledge Node যোগ করো।
- নতুন Node-এর stable ID দাও এবং বিদ্যমান Node-এর সঙ্গে explicit relationship যোগ করো।
- Leaf Node-এর explained status 0/100 থাকবে।
- Node বা status পরিবর্তনের পর affected ancestor coverage পুনরায় calculate করো।
- Existing Node-এর পরিচয় অকারণে বদলাবে না; rename বা merge হলে reference migration করো।

Graph-এর উদ্দেশ্য পূর্ণাঙ্গ syllabus আগেভাগে বানানো নয়; গল্প ও learning content-এর সঙ্গে knowledge structure-কে ধাপে ধাপে বাড়ানো।
