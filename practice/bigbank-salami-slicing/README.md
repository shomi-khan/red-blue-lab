# Practice: BigBank — The One-Poisha Trail

> **POV:** Peter Parker ও BigBank-এর investigation team  
> **ধরন:** File-based investigation | **সময়:** 2–4 ঘণ্টা | **Difficulty:** Beginner → Intermediate

## ঘটনা

BigBank-এর কয়েকটি customer account-এ অতি ক্ষুদ্র adjustment debit দেখা যাচ্ছে। প্রতিটি transaction আলাদাভাবে দেখলে তেমন কিছু মনে হয় না। Investigation team সন্দেহ করছে, একই ধরনের debit বহু account-এ হচ্ছে এবং credit একটি নির্দিষ্ট beneficiary-তে জমা হচ্ছে।

তোমার কাছে synthetic transaction journal দেওয়া হয়েছে। Peter-এর মতো তোমাকেও একটি transaction নয়, পুরো dataset-এর pattern বুঝতে হবে।

**তোমার দায়িত্ব attacker-কে identify করা নয়। প্রথম দায়িত্ব হলো evidence দিয়ে suspicious transaction pattern শনাক্ত করা।**

## Sample data

- [transactions.csv](./data/transactions.csv) — synthetic debit ও credit journal entry।
- সব account ও beneficiary reference fabricated।
- Timestamp UTC-তে।
- Amount decimal currency unit-এ; `0.01` মানে এক পয়সা।
- `entry_type`: `DEBIT` অথবা `CREDIT`।
- `journal_id` unique ledger entry; `correlation_id` matching debit/credit pair যুক্ত করে।
- `service_identity`, `reason_code`, `beneficiary_ref` ও `batch_id` investigation clue।

## কী tool তৈরি করবে?

একটি **Transaction Evidence Analyzer** তৈরি করো, যা CSV পড়বে এবং suspicious pattern খুঁজতে সাহায্য করবে।

### Minimum requirements

1. CSV parse করে invalid বা incomplete row শনাক্ত করবে।
2. প্রতিটি `correlation_id`-এর debit ও credit pair মিলিয়ে দেখবে।
3. Beneficiary অনুযায়ী credit count, total amount ও সংশ্লিষ্ট account count বের করবে।
4. `service_identity`, `reason_code` ও `batch_id`-এর সঙ্গে repeated micro-debit-এর সম্পর্ক বিশ্লেষণ করবে।
5. Account-level ও aggregate-level summary তৈরি করবে।
6. Findings CSV বা JSON report হিসেবে export করবে।

### Investigation questions

- কতগুলো distinct customer account debit হয়েছে?
- কতগুলো debit-এর amount ঠিক `0.01`?
- কোন beneficiary সবচেয়ে বেশি credit পেয়েছে?
- প্রতিটি debit-এর matching credit আছে কি?
- কোন service identity ও batch এই pattern-এর সঙ্গে সম্পর্কিত?
- কোন entry অন্যগুলোর থেকে আলাদা?
- শুধু ledger balanced হলেই কি transaction বৈধ প্রমাণিত হয়?
- কোন finding নিশ্চিত evidence, কোনটি hypothesis?

### Expected output

কমপক্ষে মোট journal entry, distinct affected account, মোট debit amount, beneficiary অনুযায়ী credit count ও total, service identity অনুযায়ী transaction count, unmatched/malformed correlation এবং সংক্ষিপ্ত evidence summary দেখাবে।

## Suggested workflow

1. Code লেখার আগে dataset ও data shape বোঝো।
2. Hypothesis তৈরি করো: repeated one-paisa debit, beneficiary concentration ইত্যাদি।
3. প্রতিটি hypothesis পরীক্ষা করার aggregation implement করো।
4. Matching debit/credit pair যাচাই করো।
5. False positive ও limitation নথিভুক্ত করো।
6. Evidence-এর ভিত্তিতে concise incident note লেখো।

## Acceptance criteria

- একই input দিলে একই result পাওয়া যাবে।
- Duplicate `journal_id` ও malformed row report হবে।
- Matching logic কেবল amount নয়; `correlation_id`, account, entry type ও amount বিবেচনা করবে।
- Aggregate ও per-beneficiary total reproducible হবে।
- কোনো row নীরবে বাদ পড়বে না।
- Observation ও inference আলাদা থাকবে।

## Optional extensions

- Configurable threshold দিয়ে suspicious pattern flag।
- Date বা batch অনুযায়ী trend।
- Terminal table বা HTML report।
- বড় dataset-এর জন্য streaming CSV processing।
- Malformed ও edge-case fixture-সহ unit test।

## সীমাবদ্ধতা

এই dataset দিয়ে attacker-এর identity, credential compromise বা intent প্রমাণ করা সম্ভব নয়। এটি transaction pattern analysis শেখানোর জন্য। কোনো বাস্তব bank বা production data ব্যবহার করবে না।

## Character lens

Peter প্রথমে নিজের statement-এ anomaly দেখে। পরে aggregate evidence খোঁজে। তোমার tool-ও সেই progression অনুসরণ করবে: **একটি row → repeated pattern → shared destination → evidence-backed finding**。
