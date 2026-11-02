# Knowledge ও Learning Graph Architecture

> Status: User-approved architecture
> Scope: Knowledge Graph, Learning Graph, typed relationships, content gap analysis এবং reader-specific learning progress
> এই document graph-এর data contract নির্ধারণ করে। এটি কোনো application runtime বা Learning Path Generator implementation নয়।

## 1. তিনটি আলাদা দায়িত্ব

| অংশ | কী সংরক্ষণ করে | কী করে না |
|---|---|---|
| **Knowledge Graph** | Domain, Concept, Learning Objective এবং তাদের জ্ঞানগত সম্পর্ক | Reader-এর progress বা learning route সংরক্ষণ করে না |
| **Learning Graph** | Tutorial, Note, Investigation, Experiment ইত্যাদি Learning Node এবং Knowledge Node-এর সঙ্গে typed link | কোনো নির্দিষ্ট reader-এর completion state রাখে না |
| **Reader Learning Track** | একজন reader কোন Learning Node বেছে নিয়েছে, কোন ক্রমে রাখছে এবং তার progress | Shared Knowledge বা Learning Graph পরিবর্তন করে না |

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

## 3. Knowledge Coverage Analysis ও content gap

Percentage-based Knowledge Node coverage, `self_explained` flag এবং ancestor coverage calculation রাখা হবে না। এগুলো content planning-এর জন্য প্রয়োজনীয় নয় এবং completeness সম্পর্কে বিভ্রান্তিকর precision তৈরি করতে পারে।

এর বদলে Agent নতুন বা পরিবর্তিত Learning Node-এর Knowledge links বিশ্লেষণ করে **Knowledge Coverage Analysis** করবে। উদ্দেশ্য হলো কোন ধারণা নতুন করে explain করতে হবে, কোনটি আগের Learning Node থেকে reference করা যায়, আর কোন knowledge এখনো explain করা হয়নি তা শনাক্ত করা।

### 3.1 Analysis-এর নিয়ম

1. নতুন Learning Node-এর সঙ্গে যুক্ত প্রতিটি Knowledge Node-এর scope ও child Concept পরীক্ষা করো।
2. আগের Learning Node-গুলোর `explains` relationship এবং `content_anchor` দেখে কোন Knowledge Node ইতিমধ্যে explain করা হয়েছে তা শনাক্ত করো।
3. কোনো Node আগে explain করা থাকলে একই scope আবার লিখবে না; প্রাসঙ্গিক পুরোনো Learning Node-এ `references` link দাও এবং নতুন material-এ প্রয়োজনীয় নতুন context, application বা deeper scope যোগ করো।
4. Parent Concept explain করা থাকলেই তার child Concept explain হয়েছে ধরে নিও না। যেমন `Authentication` explain করা থাকলেও `Password Authentication` বা `Session Authentication` আলাদা করে explain না হলে সেগুলো content gap।
5. Child Concept explain করা থাকলেও parent Concept-এর নিজস্ব general scope explain হয়েছে ধরে নিও না।
6. পূর্বের Learning Node-গুলো published content হিসেবে গণ্য হবে। আলাদা publication status field বা publication workflow প্রয়োজন নেই।
7. প্রতিটি link-এর উদ্দেশ্য স্পষ্ট করো: `explains`, `introduces`, `demonstrates`, `applies`, `investigates`, `plans` অথবা `references`।

### 3.2 Authentication উদাহরণ

ধরা যাক Learning Node A `Authentication` এবং `Password Authentication` explain করেছে। পরে Learning Node B-তে `Authentication` এবং `Session Authentication` প্রাসঙ্গিক হলো।

- `Authentication`: আগে explain করা হয়েছে; নতুন করে general explanation নয়, Node A-তে reference।
- `Password Authentication`: আগে explain করা হয়েছে; Node B-তে পুনরাবৃত্তির প্রয়োজন নেই।
- `Session Authentication`: এখনো explain করা হয়নি; Node B-তে এর explanation দিতে হবে।

এতে নতুন Learning Node শুধু নতুন knowledge যোগ করবে, পুরোনো explanation পুনরাবৃত্তি করবে না।

### 3.3 সীমা

- কোনো Learning Node-এর সঙ্গে link থাকলেই সেটি explained নয়; `explains` relationship এবং নির্দিষ্ট `content_anchor` থাকতে হবে।
- `introduces`, `demonstrates`, `applies`, `investigates`, `plans` বা `references` একা কোনো Knowledge Node-কে explained হিসেবে চিহ্নিত করে না।
- Parent-child hierarchy নিজে থেকে explanation inheritance তৈরি করে না।
- Analysis হলো Agent-এর content planning সহায়তা; এটি explanation quality, correctness, reader mastery বা competency score নয়।
- Agent uncertainty পেলে Node-কে already explained ধরে নেবে না; gap বা review প্রয়োজন বলে চিহ্নিত করবে।

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
7. `explains` link-এর target Knowledge Node হতে হবে; source একটি বিদ্যমান Learning Node হতে হবে এবং valid content anchor থাকতে হবে।
9. `content_ref` path repository-তে বিদ্যমান canonical Markdown file-কে নির্দেশ করবে।
10. Reader Track-এর Learning Node ID বিদ্যমান ও reader-এর জন্য available হতে হবে।


## 8. Incremental evolution

পুরো Knowledge Graph, Learning Graph বা Learning Track আগে থেকে তৈরি করতে হবে না।

- Story বা research প্রয়োজন তৈরি করলে নতুন Learning Node যোগ করো।
- Learning Node প্রয়োজন হলে নতুন Knowledge Node যোগ করো।
- নতুন Node-এর stable ID দাও এবং বিদ্যমান Node-এর সঙ্গে explicit relationship যোগ করো।
- Existing Node-এর পরিচয় অকারণে বদলাবে না; rename বা merge হলে reference migration করো।

Graph-এর উদ্দেশ্য পূর্ণাঙ্গ syllabus আগেভাগে বানানো নয়; গল্প ও learning content-এর সঙ্গে knowledge structure-কে ধাপে ধাপে বাড়ানো।
