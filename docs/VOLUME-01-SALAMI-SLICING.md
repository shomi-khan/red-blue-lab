# Volume 1: The One-Poisha Theft

> BigBank-এর লাখ লাখ customer account থেকে প্রতিদিন এক পয়সা করে সরানো হচ্ছে। Peter প্রথমে নিজের salary account-এ অস্বাভাবিকতা দেখে। কিন্তু এক পয়সার পেছনে লুকিয়ে আছে এমন এক financial attack, যার ক্ষুদ্রতা-ই তার সবচেয়ে বড় camouflage।

## Narrative promise
একটি grounded cyber-security mystery thriller। Peter ও BigBank-এর Technical Head Adrian Rahman evidence ধরে ধরে attack-এর mechanism খুঁজবেন এবং customer-দের অর্থ সরানো বন্ধ করবেন। Larfleeze-কে গ্রেপ্তার করা এই Volume-এর শর্ত নয়।

## Story arc
1. **Opening:** BigBrains-এর salary credit-এর পর Peter ও কয়েকজন colleague এক পয়সার ঘাটতি লক্ষ্য করে।
2. **Dismissal:** BigBank-এর support বিষয়টিকে ক্ষুদ্র adjustment বলে উড়িয়ে দেয়।
3. **Investigation begins:** Adrian Rahman pattern-এর সম্ভাবনা বুঝে Peter-কে যুক্ত করেন।
4. **Scope:** একই ধরনের adjustment বহু account-এ দেখা যায়।
5. **Technical reveal:** একটি compromised operations credential দিয়ে Micro-Adjustment policy বদলানো হয়েছে। অতিরিক্ত permission-যুক্ত service identity সেই policy অনুযায়ী scheduled bulk adjustment চালিয়ে প্রতিটি eligible account থেকে এক পয়সা debit করে একই beneficiary destination-এ matching credit পাঠাচ্ছে।
6. **Root cause:** Ledger mathematically balanced, কিন্তু transaction authorization ও beneficiary governance ব্যর্থ হয়েছে।
7. **Containment:** Bank নির্দিষ্ট adjustment job থামায়, compromised authority revoke করে, evidence সংরক্ষণ করে।
8. **Recovery:** affected customers-কে compensating credit দেওয়া হয়; control redesign ও verification হয়।
9. **Resolution:** টাকা চুরি বন্ধ। Larfleeze-এর পরিচয়/অবস্থান সম্পূর্ণ নিশ্চিত নয়; গ্রেপ্তার হয়নি। Attack বন্ধ করাই resolution।

## Core technical model
- প্রতিটি customer debit-এর matching credit আছে; double-entry ledger তাই মোট অঙ্কে balanced।
- সমস্যা arithmetic imbalance নয়; debit-এর authorization, business purpose এবং beneficiary destination বৈধ ছিল না।
- BigBank-এর Micro-Adjustment Service বৈধ correction workflow-এর জন্য তৈরি। একটি operations credential-এর অপব্যবহারে adjustment policy বদলানো হয়। অতিরিক্ত permission-যুক্ত service identity scheduled batch-এর মাধ্যমে একই ক্ষুদ্র debit বহু account-এ প্রয়োগ করে। Beneficiary change ও bulk scope-এর independent approval দুর্বল ছিল।
- Customer statement-এ debit Account Adjustment নামে দেখা যায়; আলাদা অঙ্ক ছোট হওয়ায় অনেকেই উপেক্ষা করে।
- Fraud detection শুধু amount threshold ও aggregate balancing-এ নির্ভর করায় pattern শুরুতে ধরা পড়ে না।
- Investigation-এর মূল evidence: salary advice বনাম bank statement, adjustment reason code, journal references, beneficiary concentration, service identity audit events, configuration change history, scheduler run metadata।
- Response: job pause, authority revoke, preserve evidence, beneficiary account restriction through authorized bank process, reconcile affected entries, compensating credits, regression checks and control redesign।

## Fictional scale used in the story
Investigation-এর সময় BigBank-এর synthetic internal report-এ প্রায় 2.4 million eligible accounts-এর daily sweep hypothesis আসে। ৳0.01 × 2,400,000 = ৳24,000 per sweep। 30টি daily sweep হলে gross amount ৳720,000। এই সংখ্যা গল্পের fictional estimate; বাস্তব bank data নয়।

## Chapter outline
1. **এক পয়সার হিসাব** — Salary credit-এর পর discrepancy।
2. **যেটা কেউ দেখেনি** — BigBank-এর প্রথম dismissal; Peter evidence গুছিয়ে পাঠায়।
3. **Adrian Rahman** — Technical Head investigation শুরু করেন।
4. **হিসাব মিলে যাচ্ছে** — Double-entry ledger ও reconciliation-এর আপাত paradox।
5. **সালামির এক টুকরো** — Salami slicing ধারণা; Peter-এর hypothesis পরীক্ষা।
6. **অদৃশ্য অনুমতি** — Micro-adjustment workflow, service identity ও approval failure-এর root cause।
7. **বন্ধ করার সময়** — Safe containment, evidence preservation, recovery plan।
8. **শেষ পয়সা** — Verification, customer restoration, Larfleeze-এর অসমাপ্ত ছায়া।

## Character arcs
- Peter: ব্যক্তিগত anomaly থেকে disciplined, evidence-led incident responder হওয়া।
- Adrian: ছোট discrepancy-কে operational risk হিসেবে দেখতে শেখা; Peter-কে সহযোগী হিসেবে গ্রহণ।
- Nadia: record-based corroboration ও methodical investigation-এর মূল্য দেখায়।
- Ryan: এক পয়সা কিছু না মনোভাব থেকে cumulative harm বোঝা।
- Larfleeze: তার পরিকল্পনা ক্ষুদ্রতা ও institutional blind spot-এর ওপর নির্ভর করে; ধরা না পড়লেও attack হারায়।

## Technical learning woven into the story
- Salami slicing attack এবং cumulative impact।
- Account balance, debit/credit ও double-entry ledger।
- Transaction journal, reference IDs এবং audit trail।
- Reconciliation কী প্রমাণ করে এবং কী প্রমাণ করে না।
- Authorization বনাম authentication; service identity ও least privilege।
- Anomaly detection, aggregation ও beneficiary concentration।
- Incident response: containment, evidence preservation, recovery, validation।
- Compensating entries, idempotency ও regression testing।

## Continuity and safety
- Fictional institution ও synthetic records ব্যবহার।
- Real unauthorized intrusion-এর operational instructions নয়।
- Peter production environment-এ অনুমতি ছাড়া পরিবর্তন করে না।
- Observation, hypothesis, inference ও confirmed finding আলাদা রাখা।
- Attack বন্ধ করা primary victory; arrest নয়।
