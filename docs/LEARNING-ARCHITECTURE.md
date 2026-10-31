# Learning Architecture

## 1. লক্ষ্য

লক্ষ্য professional security engineering-এর জন্য connected mental model তৈরি করা। Professional security একটি বিস্তৃত ক্ষেত্র; novel বা curriculum কাউকে স্বয়ংক্রিয়ভাবে professional বানায় না। তবে বাস্তবসম্মত, ধারাবাহিক ও hands-on learning শক্তিশালী foundation ও specialization pathway তৈরি করতে পারে।

## 2. Learning-এর মূল unit

**Concept → System Model → Evidence → Experiment → Engineering Judgment**

| ধাপ | পাঠকের কাজ |
|---|---|
| Concept | ধারণা ও সীমা বোঝা |
| System Model | Component, data flow, trust boundary ও dependency কল্পনা |
| Evidence | বাস্তব বা synthetic observation পড়া |
| Experiment | Safe environment-এ behavior পরীক্ষা |
| Engineering Judgment | Risk, trade-off, mitigation ও uncertainty মূল্যায়ন |

Tool তৈরি optional branch, বাধ্যতামূলক ধাপ নয়।

## 3. Learning domain taxonomy

Project-এর approved domain taxonomy, six-layer ecosystem, cross-cutting capabilities, T-shaped competency strategy এবং companion repository mapping-এর canonical source হলো [Learning Domains](LEARNING-DOMAINS.md)। এই file-এর পরের competency map সংক্ষিপ্ত reference হিসেবে থাকবে; taxonomy-এর বিকল্প নয়।

## 3. Competency domain map

এটি সম্ভাব্য coverage map, final syllabus নয়। World ও story arc স্থির হলে sequence ও depth নির্ধারিত হবে।

| Domain | সম্ভাব্য competency |
|---|---|
| Computing Foundations | Binary, CPU/memory, process, file system |
| Programming & Systems | Go বা নির্বাচিত language, concurrency, I/O, debugging, testing |
| Networking | Ethernet, IP, TCP, UDP, routing, DNS, sockets, packet analysis |
| Protocol Engineering | HTTP, TLS, authentication protocols, serialization, state machines |
| Linux & OS | Process model, permissions, system calls, namespaces, isolation |
| Web & Application Security | Trust boundary, input handling, sessions, authn/authz, common flaws |
| Secure Software Engineering | Threat modeling, code review, dependency risk, secure design |
| Cryptography | Primitives, key lifecycle, signatures, certificates, TLS |
| Identity & Enterprise | Identity systems, directory services, federation, privilege boundaries |
| Cloud Security | IAM, network controls, storage, secrets, workload identity, logging |
| Containers | Image provenance, runtime isolation, Kubernetes control plane |
| Infrastructure Security | Segmentation, exposure, service discovery, secure configuration |
| Offensive Security | Reconnaissance, vulnerability validation, controlled exploitation concepts |
| Defensive Security | Telemetry, detection logic, triage, hardening |
| Digital Forensics | Evidence handling, artifacts, timelines, integrity, chain of custody |
| Incident Response | Identification, containment, eradication, recovery, lessons learned |
| Reverse Engineering | File formats, static/dynamic analysis, behavior observation |
| Threat Intelligence | TTPs, indicators, intelligence lifecycle, attribution uncertainty |
| AI & ML Security | Prompt injection, data poisoning, model supply chain, retrieval/agent risks |
| Security Architecture | Threat modeling, trust zones, resilience, defense in depth |
| Governance & Communication | Risk explanation, responsible disclosure, reporting, privacy, ethics |

## 4. Tool strategy

Tool-কে curriculum index হিসেবে ব্যবহার করবে না। Tool তৈরির আগে জিজ্ঞেস করো:

1. কোন বাস্তব প্রশ্নের উত্তর দেবে?
2. Diagram বা experiment যথেষ্ট কি?
3. Existing utility ব্যবহার করাই ভালো কি?
4. Implementation করলে কোন engineering judgment শেখা হবে?
5. Output কী evidence দেবে এবং limitation কী?
6. Safe local scope-এ পরীক্ষা করা যাবে কি?

Tool থাকলে contract, edge case, failure classification, resource constraint, test, false positive ও integration বোঝাও। Tool count, LOC বা feature count success metric নয়।

## 5. Visualization-first concept design

| Conceptual problem | Visual |
|---|---|
| Component ও dependency | Architecture / component diagram |
| Request বা protocol exchange | Sequence diagram |
| Decision ও branching | Flowchart |
| Lifecycle / state transition | State diagram |
| Data movement | Data-flow diagram |
| Trust boundary | Trust-zone / boundary diagram |
| Attack chain | Attack-path graph |
| Incident chronology | Timeline |
| Packet / protocol fields | Annotated byte layout বা table |
| Trade-off | Comparison table |

একটি diagram-এ সবকিছু ঢোকাবে না। Context → component → sequence → failure/threat path হিসেবে ভাঙতে পারো।

## 6. Depth progression

| স্তর | প্রত্যাশিত সক্ষমতা |
|---|---|
| Recognize | Term ও component চিনতে পারা |
| Explain | Mechanism নিজের ভাষায় ব্যাখ্যা |
| Trace | Data/control flow অনুসরণ |
| Analyze | Evidence, failure ও boundary বিশ্লেষণ |
| Test | Hypothesis safe environment-এ verify |
| Design | Mitigation ও architecture trade-off প্রস্তাব |
| Evaluate | Limitation, residual risk ও uncertainty বিচার |

সব topic-কে একই depth-এ নিতে হবে না।

## 7. Three perspectives

- 🔴 **Offensive:** Weakness আবিষ্কার, validate ও controlled lab-এ reproduce।
- 🔵 **Defensive:** Exposure কমানো, detect, contain ও recover।
- 🟣 **Engineering:** কোন design বা implementation flaw সমস্যা তৈরি করেছে, কীভাবে architecture উন্নত হবে।

সব episode-এ তিনটি সমান থাকবে না; পুরো project-এ meaningful balance দরকার।

## 8. Learning artifact

Concept explainer, architecture diagram, protocol walkthrough, safe experiment, synthetic evidence pack, threat model, code review, lab specification, detection exercise, incident report বা design review হতে পারে। Narrative event অনুযায়ী নির্বাচন করো।

## 9. Verification signals

পাঠক diagram দেখে data flow ব্যাখ্যা করতে পারে; packet/log/request থেকে কী জানা যায় ও যায় না আলাদা করতে পারে; hypothesis test করতে পারে; vulnerability root cause ব্যাখ্যা করতে পারে; mitigation ও regression verify করতে পারে; uncertainty-সহ report লিখতে পারে।

## 10. Sequencing policy

- Prerequisite dependency স্পষ্ট করো।
- Advanced topic-এর আগে foundation নিশ্চিত করো।
- Story chronology ও prerequisite সংঘর্ষ করলে optional bridge তৈরি করো।
- পূর্বের concept reference করে নতুন depth যোগ করো।
- শুধু completeness-এর জন্য domain যোগ করো না।
- Roadmap review-এর মাধ্যমে evolve করবে।


## 11. Integrated narrative learning

Learning-এর reader-facing flow:

**Story → Curiosity → Knowledge → Exploration → Discovery → Engineering Judgment**

Story কোনো প্রশ্ন, failure, investigation বা character need তৈরি করবে। সেই moment-এর পর সংশ্লিষ্ট detailed learning material narrative sequence-এর অংশ হিসেবে আসবে; এরপর character-এর প্রয়োগ, পরীক্ষা, সিদ্ধান্ত বা consequence-এ গল্প এগোবে।

- Learning material শুধু Peter-এর জন্য নয়; বর্তমান POV character-এর কাজ ও knowledge context অনুযায়ী হবে।
- Character study, research, investigation, experiment, design এবং tool-building learning-এর স্বাভাবিক উৎস হতে পারে।
- Learning material-এর নিজস্ব heading, diagram, evidence বা explanatory structure থাকতে পারে; কিন্তু story experience থেকে বিচ্ছিন্ন classroom interruption হবে না।
- Novel ও learning material independently readable থাকবে। এটি content organization-এর স্বাধীনতা দেয়, reader experience-এ বিচ্ছিন্নতা বাধ্যতামূলক করে না।

## 12. Hybrid Knowledge Graph

Knowledge Graph-এর দায়িত্ব knowledge structure ও relationship প্রকাশ করা; এটি নিজে learner-এর route generate করবে না। Learning Path Generator ভবিষ্যতে graph ব্যবহার করে learner route তৈরি করতে পারে, তবে সেটি আলাদা component।

### Node types

- **Domain:** Knowledge-এর logical area; একটি knowledge item একাধিক domain-এর সঙ্গে যুক্ত হতে পারে।
- **Concept:** Technical knowledge unit, যেমন TCP, SYN flag, sequence number, digital signature বা certificate authority।
- **Learning Objective (LO):** Learner কী ব্যাখ্যা, trace, analyze, test, design বা evaluate করতে পারবে তার নির্দিষ্ট statement।

Concept ও LO আলাদা node। Concept-এর canonical identity একটিই থাকবে; একই concept একাধিক domain, LO ও learning artifact-এর সঙ্গে সম্পর্কিত হতে পারে।

### Relationship families

- **Concept-to-Concept:** Technical relationship, যেমন uses, contains, depends_on বা interacts_with। এগুলো knowledge relationship; learner prerequisite নয়।
- **LO-to-Concept:** LO অর্জনের সঙ্গে concept-এর সম্পর্ক: **Required**, **Supporting** অথবা **Related**। Classification প্রতিটি LO–Concept pair-এর জন্য নির্ধারিত হবে।
- **LO-to-LO:** Strict learning prerequisite। Prerequisite LO সম্পন্ন না হলে dependent LO-তে অগ্রসর হওয়া যাবে না।

**Related** কোনো prerequisite edge নয়। Technical Concept-to-Concept relationship থেকেও strict learning prerequisite অনুমান করা যাবে না।

### Graph constraints

- Mandatory LO prerequisite subgraph acyclic (DAG) হতে হবে।
- Whole knowledge graph-এ technical relationship-এর cycle থাকতে পারে।
- Concept node তৈরি হবে যখন knowledge item independently meaningful, reusable, একাধিক LO-তে প্রাসঙ্গিক, অথবা নিজস্ব explanation/experiment/assessment পাওয়ার যোগ্য। প্রতিটি atomic detail আলাদা node হওয়া বাধ্যতামূলক নয়।
- Graph structure ও learning path generation আলাদা দায়িত্ব।

**Open:** Concrete node/edge schema, metadata fields, graph storage/format, validation tooling ও maintenance workflow।


## 13. Content storage format

Project-এর মূল narrative ও learning content **Markdown file**-এ canonicalভাবে সংরক্ষিত হবে।

- **Markdown:** Novel, Concept Note, Lab, evidence pack, reference ও explanatory content-এর মূল format।
- **YAML Frontmatter:** Content-এর structured metadata রাখার format। নির্দিষ্ট field schema ও validation rules পরবর্তী design phase-এ স্থির হবে।
- **Mermaid:** Markdown-এর মধ্যে text-based diagram লেখার preferred option; diagram প্রয়োজন অনুযায়ী ব্যবহার হবে।
- **Knowledge Graph:** ভবিষ্যতে Markdown content-এর structured metadata ও explicit references থেকে generate করা যেতে পারে। Graph আলাদা করে content-এর duplicate source of truth হবে না।

JSON বা database-কে মূল content storage হিসেবে ব্যবহার করা হবে না। ভবিষ্যতে derived graph, index বা tooling-এর জন্য সেগুলো ব্যবহার করা যেতে পারে, যদি প্রয়োজন ও design অনুমোদিত হয়।
