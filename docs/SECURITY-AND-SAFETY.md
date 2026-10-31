# Security and Safety Guidelines

এই project offensive ও defensive Cyber Security দুটোই আলোচনা করবে। Authorization, containment, evidence integrity ও harm prevention বাধ্যতামূলক।

## 1. Authorization boundary

অনুমোদিত practical target:
- নিজের local machine বা isolated lab।
- Synthetic fixture।
- Intentionally vulnerable local application।
- Explicitly authorized training environment।

Default learning path local-only। Public IP, production service, third-party account বা অন্যের infrastructure-এ test করার নির্দেশনা দেবে না, যদি না scope ও written authorization স্পষ্টভাবে নির্ধারিত থাকে।

## 2. Offensive learning

শেখানো যেতে পারে:
- Attack surface ও threat modeling।
- Scope-aware reconnaissance concepts।
- Vulnerability class ও root cause।
- Controlled lab-এ safe reproduction।
- Input validation, authentication, authorization ও trust-boundary testing।
- Exploitability ও impact মূল্যায়ন।
- Defensive validation ও regression test।

বাস্তব unauthorized system-এ ক্ষতি করার operational detail দেবে না। Credential theft, malware deployment, persistence, stealth/evasion, destructive payload বা unauthorized compromise walkthrough তৈরি করবে না।

Risky technique-এর ক্ষেত্রে conceptual explanation, isolated simulation, defensive signal, mitigation ও scope স্পষ্ট করো।

## 3. Defensive engineering

শুধু "patch করো" নয়। প্রাসঙ্গিক হলে asset, trust boundary, logging, telemetry, detection logic, false positive, triage, evidence preservation, containment impact, recovery ও verification ব্যাখ্যা করো।

## 4. Evidence integrity

- Synthetic evidence-কে synthetic label করো।
- Timestamp, timezone, source ও integrity context রাখো।
- Observation ও inference আলাদা রাখো।
- Evidence অনুপস্থিত মানেই ঘটনা ঘটেনি নয়।
- Attribution uncertainty স্পষ্ট করো।
- Fictional artifact-কে real-world fact হিসেবে দেখিও না।

## 5. AI security

আলাদা করে বিবেচনা করো:
- Model behavior
- Training data ও pipeline
- Retrieval source / knowledge base
- Prompt ও instruction hierarchy
- Tool invocation / agent permissions
- Identity ও API access
- Deployment infrastructure
- Monitoring, evaluation ও human oversight

AI output trusted fact নয়। Limitation ও system boundary দেখাও।

## 6. Privacy

- Synthetic identity ও fabricated data ব্যবহার।
- Real credential, token, API key বা personal data commit নয়।
- Example log/evidence-এ secret redact।
- Privacy impact ও data minimization বিবেচনা।

## 7. Future lab implementation-এর safe defaults

প্রাসঙ্গিক ক্ষেত্রে:
- Explicit scope ও loopback default।
- Timeout, cancellation, bounded concurrency।
- Request/body/file/memory size limit।
- No secret logging।
- Safe failure behavior।
- Clear output ও error classification।
- Destructive action-এর আগে simulation বা explicit confirmation।
- Deterministic local tests।

## 8. Villain depiction

Villain-এর motive, strategy, impact ও investigation দেখানো যায়। কিন্তু step-by-step operational detail নয় যা বাস্তব ক্ষতিকর কাজ সহজ করে। Suspense তৈরি হবে clue, uncertainty, system consequence, competing hypothesis ও reveal দিয়ে।

## 9. Stop and escalate

Request authorization boundary অতিক্রম করলে বা harmful operational detail চাইলে সেই অংশ তৈরি করবে না। Safe alternative হিসেবে local simulation, toy example, synthetic data, detection logic বা mitigation প্রস্তাব করো। Human review প্রয়োজন হলে বলো।
