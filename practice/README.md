# Practice Lab

এখানে পাঠক গল্পের character-দের বাস্তব engineering ও investigation problem হাতে-কলমে সমাধান করবে। প্রতিটি practice আলাদা, self-contained folder। কোনো practice শুধু tool-এর সংখ্যা বাড়ানোর জন্য যোগ করা হবে না: গল্পে তার প্রয়োজন, সংশ্লিষ্ট character-এর কাজ এবং শেখানো knowledge থাকতে হবে।

## Volume 1 practices

### 1. [BigBank: The One-Poisha Trail](./bigbank-salami-slicing/)
- **ধরন:** File-based investigation
- **POV:** Peter Parker ও BigBank investigation team
- **গল্পের প্রয়োজন:** বহু account-এ repeated micro-debit এবং একই beneficiary-তে credit-এর pattern শনাক্ত করা।
- **তৈরি করবে:** Transaction Evidence Analyzer
- **প্রধান কাজ:** journal validation, debit/credit correlation, beneficiary concentration, service/batch aggregation ও evidence report।

### 2. [BigBank: Who Changed the Adjustment Rules?](./bigbank-change-audit/)
- **ধরন:** File-based investigation
- **POV:** Adrian ও BigBank-এর incident investigation team
- **গল্পের প্রয়োজন:** Micro-Adjustment Service-এর configuration ও authorization control কীভাবে বদলেছে, audit evidence থেকে তা বোঝা।
- **তৈরি করবে:** Configuration Change & Authorization Auditor
- **প্রধান কাজ:** change timeline, actor/service identity, approval chain, privileged change ও policy violation শনাক্ত করা।

### 3. [BigBank: Verify the Recovery](./bigbank-recovery-validation/)
- **ধরন:** File-based investigation
- **POV:** Nadia ও BigBank-এর recovery/verification team
- **গল্পের প্রয়োজন:** customer balance সংশোধনের সময় প্রতিটি original debit-এর বিপরীতে traceable compensating credit হয়েছে কি না এবং retry-তে duplicate financial effect তৈরি হয়েছে কি না যাচাই করা।
- **তৈরি করবে:** Recovery & Reconciliation Validator
- **প্রধান কাজ:** original-to-compensation matching, amount validation, missing/duplicate correction শনাক্তকরণ ও reconciliation report।

## কাজ করার নিয়ম

1. প্রতিটি practice-এর README-তে থাকা story context, scope ও objective আগে পড়ো।
2. সংশ্লিষ্ট chapter এবং technical notes দেখে নাও।
3. README-তে constraint না থাকলে নিজের পছন্দের language ও library বেছে নাও।
4. ছোট, testable version দিয়ে শুরু করো।
5. Acceptance criteria দিয়ে কাজ যাচাই করো।
6. Observation, evidence, hypothesis, limitation ও conclusion আলাদা করে লেখো।

## Safety ও data boundary

- সব sample data synthetic; বাস্তব customer, credential বা production data নয়।
- Practice-গুলো offline file analysis-এর জন্য। কোনো live banking system-এ connect করবে না।
- গল্পের fictional incident-এর বাইরের identity, motive বা ঘটনা sample data থেকে অনুমান করবে না।
- Tool-এর output evidence-এর সীমা স্পষ্ট করবে; কোনো correlation-কে একা proof হিসেবে দেখাবে না।

Practice optional। গল্প পড়তে এগুলো করা বাধ্যতামূলক নয়।
