# Learning Domains

> Status: User-approved learning direction, version 1.0
> Scope: Broad Cyber Security + Systems Engineering knowledge ecosystem
> এই document domain taxonomy ও learning strategy নির্ধারণ করে। এটি chapter-by-chapter final syllabus নয়।

## 1. লক্ষ্য ও পরিচয়

এই project শুধু Cyber Security শেখানোর জন্য নয়। লক্ষ্য হলো পাঠককে একজন **Systems-minded Security Engineer**-এর মতো চিন্তা করতে সাহায্য করা: system কীভাবে তৈরি, কীভাবে চলে, কোথায় trust স্থাপিত, কীভাবে failure ঘটে, evidence কী বলে এবং কীভাবে নিরাপদ ও resilient design করা যায়।

Learning scope তাই **Broad Cyber Security + Systems Engineering Education**। Computing, Networking, Operating Systems, Programming, Distributed Systems, Hardware ও Control Systems-এর প্রয়োজনীয় foundation থাকবে; Security হবে এগুলোর ওপর দাঁড়ানো একটি গভীর প্রয়োগক্ষেত্র।

সব domain-এর সব topic সমান গভীরতায় শেখানো হবে না। Broad foundation-এর পর গল্প, incident ও reader interest অনুযায়ী কিছু বিষয়ে specialization তৈরি হবে।

## 2. Domain ecosystem

নিচের ছয়টি layer domain-গুলোকে সংগঠিত করার একটি mental map। এগুলো rigid syllabus order নয়। কোনো incident-এর জন্য prerequisite concept আগে দরকার হলে optional bridge বা just-in-time explanation দেওয়া যাবে।

### Layer 1: Computing Foundations

পরবর্তী systems ও security concept বোঝার ভিত্তি।

- Computer Architecture
- Binary, Hexadecimal ও Number Systems
- CPU, Memory ও Storage
- Operating System Fundamentals
- Process, Thread ও Scheduling
- Programming Fundamentals
- Data Structures & Algorithms
- Memory Management
- Concurrency ও Synchronization

**উদ্দেশ্য:** Application-এর নিচে computation, memory, execution ও resource কীভাবে কাজ করে তা বোঝা।

### Layer 2: Systems & Networking

একটি machine এবং machine-গুলোর মধ্যে communication কীভাবে ঘটে।

- Networking Fundamentals
- OSI ও TCP/IP Models
- Ethernet, MAC Address ও ARP
- IP Addressing, IPv4/IPv6 ও Subnetting
- Routing ও Switching
- TCP, UDP ও ICMP
- DNS ও DHCP
- HTTP/HTTPS
- TLS
- Linux Internals
- System Calls
- Sockets ও Network Programming

**উদ্দেশ্য:** Request, packet, process ও operating-system behavior trace এবং troubleshoot করতে পারা।

### Layer 3: Software & Application Engineering

বাস্তব software system-এর design, implementation ও operation।

- Programming Languages ও Runtime
- Backend Architecture
- API Design
- Web Architecture
- Databases ও Storage
- Authentication ও Authorization
- Session Management
- Secure Coding
- Software Testing ও Debugging
- Dependency ও Package Management
- Distributed Systems
- Message Queues ও Event-driven Architecture

**উদ্দেশ্য:** Software-এর behavior, trust boundary, dependency এবং design decision থেকে security risk বুঝতে পারা।

### Layer 4: Cyber Security Core

Offensive, Defensive ও Engineering perspective-এ security fundamentals।

| Domain | সম্ভাব্য coverage |
|---|---|
| Security Fundamentals | CIA Triad, threat modeling, attack surface, risk |
| Cryptography | Encryption, hashing, MAC, digital signatures, key management, PKI |
| Identity Security | IAM, SSO, MFA, federation, privilege boundaries |
| Web & Application Security | OWASP concepts, injection, XSS, SSRF, access-control flaws |
| Network Security | Firewall, IDS/IPS, segmentation, secure communication |
| Offensive Security | Reconnaissance concepts, weakness discovery, controlled validation |
| Defensive Security | Detection, hardening, monitoring, containment |
| Vulnerability Research | Root cause, exploitability, impact, responsible disclosure |
| Secure Engineering | Secure design, security architecture, verification, resilience |

**উদ্দেশ্য:** Security control শুধু ব্যবহার নয়, তার mechanism, assumptions, limitations ও trade-off বিচার করতে পারা।

### Layer 5: Advanced Security & Investigation

গভীর investigation, response এবং production-scale security।

- Digital Forensics
- Incident Response
- Threat Intelligence
- Malware Analysis
- Reverse Engineering
- Binary Analysis
- Memory Forensics
- Security Operations
- Detection Engineering
- Cloud Security
- Container Security
- Infrastructure Security
- Supply Chain Security
- Security Automation

**উদ্দেশ্য:** জটিল incident-এর evidence সংগ্রহ, বিশ্লেষণ, containment, recovery এবং systemic improvement করতে পারা।

### Layer 6: Emerging & Specialized Systems

উন্নত, বিশেষায়িত এবং ভবিষ্যৎমুখী system-এর security ও engineering।

- AI & ML Security
- LLM Security
- Distributed AI Systems
- Embedded Systems Security
- IoT Security
- Hardware Security
- Firmware Analysis
- Industrial Control Systems (ICS)
- Operational Technology (OT)
- SCADA Security
- Control Systems
- Robotics Security
- Cyber-Physical Systems
- Quantum Computing ও Post-Quantum Cryptography

**উদ্দেশ্য:** Software-এর বাইরেও physical process, hardware, autonomous system ও emerging computation-এর risk বুঝতে পারা।

## 3. Cross-cutting capabilities

এগুলো আলাদা chapter group বা security specialty নয়। সব layer ও domain-এর মধ্যে প্রয়োগ হবে।

### 3.1 Systems Thinking

- System boundary ও component relationship
- Dependency mapping
- Failure modes ও failure propagation
- Feedback loops
- Fault tolerance ও resilience
- Reliability engineering

### 3.2 Psychology & Human Factors

- Social engineering
- Cognitive bias
- Decision-making under uncertainty
- Human error
- Behavioral manipulation
- Usability, trust ও security friction

### 3.3 Engineering Judgment

- Trade-off analysis
- Root Cause Analysis
- Architecture review
- Risk assessment
- Verification ও validation
- Technical communication

## 4. Three perspectives across domains

প্রতিটি domain-কে প্রয়োজন অনুযায়ী তিনটি perspective থেকে দেখা হবে। প্রতিটি chapter বা incident-এ তিনটি perspective সমানভাবে থাকা বাধ্যতামূলক নয়; পুরো project-এ meaningful coverage থাকতে হবে।

- 🔴 **Offensive:** System-এর weakness, attack surface ও failure কীভাবে আবিষ্কার বা validate করা যায়?
- 🔵 **Defensive:** কীভাবে exposure কমানো, detect, prevent, contain ও recover করা যায়?
- 🟣 **Engineering:** কোন design বা implementation decision ঝুঁকি তৈরি করেছে, এবং কীভাবে system আরও secure ও resilient করা যায়?

Offensive learning safe, controlled ও authorized environment-এ সীমাবদ্ধ থাকবে। ক্ষতিকর operational instructions নয়, reasoning, observable behavior, defensive implication ও mitigation অগ্রাধিকার পাবে।

## 5. T-shaped competency strategy

পাঠক সব domain-এ সমান expert হবে না।

- **Broad foundation:** Computing, Systems, Networking, Programming ও Security-এর গুরুত্বপূর্ণ ভিত্তি।
- **Deep expertise:** গল্পের চরিত্র, incident এবং reader-এর নির্বাচিত interest অনুযায়ী কিছু domain-এ গভীরতা।
- **Integration:** একাধিক domain-এর knowledge একসঙ্গে ব্যবহার করে system-level problem বোঝা ও সমাধান করা।

কোনো character-এর expertise তার role, experience, resource ও limitation-এর সঙ্গে সামঞ্জস্যপূর্ণ হবে। Character বা reader-এর progression-কে সব topic-এ mastery হিসেবে দেখানো যাবে না।

## 6. Learning order ও dependency

Domain layer-গুলো conceptual grouping, বাধ্যতামূলক linear syllabus নয়।

1. প্রতিটি advanced concept-এর prerequisite ও dependency চিহ্নিত করো।
2. Story incident প্রয়োজন তৈরি করলে just-in-time learning ব্যবহার করো।
3. Prerequisite পূরণ না হলে optional bridge বা foundational note দাও।
4. Story chronology-কে rigid curriculum-এর অধীন কোরো না।
5. আগে শেখা concept পরবর্তী incident-এ reinforce, integrate ও progressively harder context-এ reuse করো।
6. Topic যোগ করো যখন story, system understanding বা competency-তে বাস্তব মূল্য যোগ হয়।

Knowledge Dependency Graph prerequisite, concept relationship এবং incident-to-knowledge mapping দেখাবে। এর exact schema ও maintenance process আলাদা design decision।

## 7. Knowledge integration ও verification

শুধু কোনো term মনে রাখতে পারা যথেষ্ট নয়। পাঠককে progressively নিচের কাজগুলো করতে সক্ষম হতে হবে:

**Recognize → Explain → Trace → Analyze → Test → Design → Evaluate**

উদাহরণ: TCP সম্পর্কে সংজ্ঞা জানা এক ধরনের knowledge। কিন্তু TCP behavior, Linux networking, packet capture এবং firewall policy একত্রে ব্যবহার করে কোনো incident-এর সম্ভাব্য failure boundary নির্ধারণ করতে পারা knowledge integration-এর প্রমাণ।

Verification-এ দেখা হবে পাঠক:
- একাধিক domain-এর concept একত্রে প্রয়োগ করতে পারে কি না।
- Evidence ও assumption আলাদা রাখতে পারে কি না।
- Hypothesis test করতে পারে কি না।
- Root cause, limitation ও residual risk ব্যাখ্যা করতে পারে কি না।
- Trade-off-সহ design বা mitigation প্রস্তাব করতে পারে কি না।

## 8. Existing learning repositories-এর সঙ্গে সম্পর্ক

এই project-এর domain map standalone এবং বিস্তৃত থাকবে। বিদ্যমান repository-র content duplicate করার প্রয়োজন নেই; প্রয়োজনমতো সেগুলোকে companion learning resource হিসেবে reference করা যাবে।

- **network-stack:** Networking fundamentals, protocols, addressing, routing, TLS, network security, production networking ও troubleshooting-এর companion resource।
- **trust-stack:** Authentication, authorization, session, token, OAuth/OIDC এবং web identity security-এর companion resource।

এই দুই repository পুরো Learning Domain cover করে না। Computing foundations, OS internals, distributed systems, forensics, reverse engineering, AI/ML, embedded, hardware ও control systems-এর মতো বিষয় এই project-এর broader scope-এর অংশ থাকবে।

## 9. Scope ও evolution

এই taxonomy approved learning direction, exhaustive syllabus বা chapter commitment নয়। Story arc, technical research ও reader needs অনুযায়ী topic-এর depth, order এবং specialization evolve করতে পারে। বড় structural পরিবর্তন DECISIONS.md-এ review ও approval-এর মাধ্যমে নথিভুক্ত করতে হবে।
