# Practice: BigBank — Verify the Recovery?

> **POV:** Nadia ও BigBank-এর recovery/verification team  
> **ধরন:** File-based investigation | **সময়:** 2–4 ঘণ্টা | **Difficulty:** Intermediate

## গল্পের প্রেক্ষাপট

Volume 1-এর Chapter 8-এ BigBank customer account-এ compensating credit পাঠায়। Original debit মুছে ফেলা হয় না; নতুন credit entry দিয়ে correction traceable রাখা হয়। Recovery team-কে নিশ্চিত হতে হয়, প্রতিটি correction সঠিক original transaction-এর সঙ্গে যুক্ত, amount ঠিক এবং retry-এর কারণে duplicate financial effect তৈরি হয়নি।

তোমার কাজ হলো recovery dataset-এর integrity যাচাই করা। Sample-এ ইচ্ছাকৃতভাবে কিছু test anomaly রাখা হয়েছে। এগুলো গল্পের final outcome-এর দাবি নয়, validator পরীক্ষা করার synthetic edge case।

## Sample data

- [recovery_entries.csv](./data/recovery_entries.csv): original debit ও compensating credit journal entries।
- [recovery_requests.csv](./data/recovery_requests.csv): recovery request ও idempotency outcome।
- সব account/reference fabricated; amount BDT-তে decimal currency unit।
- original_journal_id compensating credit-কে original debit-এর সঙ্গে যুক্ত করে।
- idempotency_key একই logical recovery request-এর retry শনাক্ত করতে ব্যবহৃত।

## কী tool তৈরি করবে?

একটি **Recovery & Reconciliation Validator** তৈরি করো, যা original journal এবং recovery request মিলিয়ে correction integrity report তৈরি করবে।

### Minimum requirements

1. দুই CSV parse করে malformed row ও duplicate identifier শনাক্ত করবে।
2. প্রতিটি original debit-এর জন্য compensating credit আছে কি না যাচাই করবে।
3. Original ও compensation amount সমান কি না এবং account reference সঠিক কি না যাচাই করবে।
4. একটি original debit-এর বিপরীতে একাধিক effective compensation আছে কি না শনাক্ত করবে।
5. একই idempotency_key-এর retry request এবং তাদের outcome বিশ্লেষণ করবে।
6. Missing, duplicate, mismatched ও valid recovery আলাদা category-তে report করবে।
7. প্রতিটি finding-এ original journal ID এবং সংশ্লিষ্ট recovery/request ID রাখবে।

### Investigation questions

- কতগুলো original debit recovery-এর জন্য এসেছে?
- সব original debit-এর compensating credit আছে কি?
- কোনো credit ভুল account বা ভুল amount-এ গেছে কি?
- একই idempotency key একাধিকবার এসেছে কি?
- Retry request-এর পর duplicate financial effect হয়েছে কি, নাকি retry safely deduplicated হয়েছে?
- কোন discrepancy-র জন্য manual review দরকার?

### Acceptance criteria

- Money calculation floating-point arithmetic দিয়ে করবে না; decimal-safe representation ব্যবহার করবে।
- Original journal entry delete বা overwrite করবে না।
- Retry event এবং posted ledger credit-কে আলাদা করে বিবেচনা করবে।
- একই input-এ deterministic result হবে।
- কোনো unmatched row নীরবে বাদ পড়বে না।
- Tool report-এ discrepancy এবং limitation স্পষ্ট থাকবে।

## Optional extensions

- Reconciliation summary JSON/CSV export।
- Recovery batch অনুযায়ী totals।
- Duplicate retry simulation ও idempotency test।
- Property-based test: একই request যতবার retry হোক, effective credit একবারের বেশি হবে না।

## সীমাবদ্ধতা

এই sample recovery validation শেখানোর জন্য, production banking integration নয়। শুধু amount match হলেই customer identity, authorization বা business legitimacy প্রমাণিত হয় না। বাস্তব recovery workflow-এ independent approval ও audit evidence-ও প্রয়োজন।

## Character lens

Nadia-র কাজ হলো শুধু “refund পাঠানো হয়েছে” বলা নয়। প্রতিটি customer correction যেন original debit পর্যন্ত trace করা যায় এবং retry-তে দ্বিতীয়বার টাকা credit না হয়, সেটি প্রমাণ করা।
