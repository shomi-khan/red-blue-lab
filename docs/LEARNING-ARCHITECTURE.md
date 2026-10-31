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
