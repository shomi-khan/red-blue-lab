# Volume 1 — Technical Notes

এই নোটগুলো গল্পের প্রযুক্তিগত বিষয়গুলো আরেকটু বিস্তারিত বোঝার জন্য। BigBank কাল্পনিক; এখানে দেখানো architecture বাস্তব সব ব্যাংকের architecture নয়। শেখার সুবিধার জন্য একটি বিশ্বাসযোগ্য উদাহরণ হিসেবে তৈরি করা হয়েছে।

## 1. Salami Slicing Attack

Salami slicing-এ আক্রমণকারী প্রতিটি account বা transaction থেকে খুব অল্প অঙ্ক সরায়। একজন গ্রাহকের ক্ষতি এত ছোট হয় যে তিনি হয়তো খেয়াল করেন না। কিন্তু অনেক account-এ একই কাজ বারবার হলে সব ক্ষুদ্র অঙ্ক মিলে বড় অঙ্ক হয়।

গল্পের fictional model:
- Eligible account count: 2,400,000
- Per-account debit: ৳0.01
- One sweep: ৳24,000
- 30 daily sweeps: ৳720,000

Formula: total = per_account_amount × affected_account_count × sweep_count

এটি একটি conceptual example; বাস্তব bank dataset নয়।

## 2. Salami slicing-এর classic rounding variant

কিছু পরিচিত উদাহরণে calculation অনেক decimal place পর্যন্ত হয়, কিন্তু customer account-এ কম precision-এ amount post হয়। Discarded fractional remainder গোপনে আলাদা destination-এ জমা করা হয়। এ ধরনের rounding manipulation-ও salami technique-এর পরিচিত pattern।

তবে Volume 1-এর BigBank incident-এ সরাসরি ৳0.01 account adjustment ব্যবহৃত হয়েছে। তাই এটি rounding residue-এর সঙ্গে গুলিয়ে ফেলা যাবে না। গল্পে attacker বৈধ micro-adjustment workflow অপব্যবহার করে fixed one-poisha debit তৈরি করছে।

## 3. Double-entry ledger

Double-entry bookkeeping-এ প্রতিটি transaction-এর debit ও credit side থাকে। Amount balanced হওয়া accounting arithmetic-এর consistency দেখায়; এটি নিজে থেকে authorization বা business legitimacy প্রমাণ করে না।

গল্পের উদাহরণ:

| Account | Debit | Credit |
|---|---:|---:|
| Customer account | ৳0.01 | |
| Beneficiary account | | ৳0.01 |

দুই side মিলে গেলেও customer debit-এর authority ও beneficiary destination-এর legitimacy আলাদা করে যাচাই করতে হয়।

## 4. Reconciliation-এর সীমা

Reconciliation বিভিন্ন independent record মিলিয়ে discrepancy শনাক্ত ও explain করে। কিন্তু দুই record-এ একই ভুল transaction থাকলে arithmetic match-ও ভুল activity-কে বৈধ করে না। তাই reconciliation-এর সঙ্গে authorization review, business-rule validation ও beneficiary analysis প্রয়োজন।

## 5. Root cause: control failure

Volume 1-এ আক্রমণটি কয়েকটি দুর্বলতার সমন্বয়ে সম্ভব হয়েছে:
- Micro-Adjustment Service-এর operations credential-এর অপব্যবহার করে adjustment policy বদলানো হয়েছে।
- Service identity-কে প্রয়োজনের চেয়ে বেশি ক্ষমতা দেওয়া হয়েছিল।
- Bulk adjustment চালানোর আগে account scope ও beneficiary destination যথেষ্ট শক্তভাবে যাচাই করা হয়নি।
- Beneficiary পরিবর্তনে স্বাধীন অনুমোদন বাধ্যতামূলক ছিল না।
- Monitoring একেকটি transaction-এর অঙ্ক দেখেছে; একই destination-এ জমা হওয়া ক্ষুদ্র credit-গুলোর মোট প্রভাব ধরতে পারেনি।

### Least privilege ও authorization boundary

Least Privilege-এর অর্থ, কোনো user বা service identity-কে তার কাজের জন্য যতটুকু permission দরকার, ঠিক ততটুকুই দেওয়া। কোনো পরিচয় সঠিকভাবে যাচাই হয়েছে (authentication) মানেই সে সব account থেকে টাকা কাটতে বা beneficiary বদলাতে পারবে, এমন নয়। Authorization-এ দেখতে হয়: কে কাজটি করছে, কী কাজ করছে, কোন account বা resource-এ করছে, কেন করছে, কত বড় পরিসরে করছে এবং প্রয়োজনীয় অনুমোদন আছে কি না।

## 6. Incident response

- **Evidence preservation:** audit log, configuration history, batch metadata ও journal reference-এর অপরিবর্তিত কপি সংরক্ষণ।
- **Containment:** সন্দেহজনক scheduled job থামানো এবং অতিরিক্ত permission বাতিল বা সীমিত করা।
- **Scope:** কোন কোন account ও transaction আক্রান্ত হয়েছে, তা নির্ধারণ।
- **Recovery:** পুরোনো ledger entry না মুছে তার বিপরীতে traceable compensating credit দেওয়া।
- **Validation:** হিসাব মিলিয়ে দেখা, duplicate credit ঠেকানো, regression test চালানো এবং নতুন sweep হচ্ছে কি না পর্যবেক্ষণ।

## 7. Key engineering lessons

1. Authentication এবং authorization আলাদা।
2. Least privilege service identity-র ক্ষেত্রেও প্রযোজ্য।
3. Amount threshold একা anomaly detection-এর জন্য যথেষ্ট নয়।
4. Aggregate behavior, beneficiary concentration ও repeated patterns গুরুত্বপূর্ণ।
5. Balanced ledger transaction-এর legitimacy প্রমাণ করে না।
6. Financial correction traceable হতে হবে; history নীরবে delete করা যাবে না।
7. Idempotent recovery duplicate financial effect ঠেকাতে সাহায্য করে।

## 8. Further reading

- Na et al., Analysis of Computer Crime Cases in Singapore: https://www.las.org.sg/wp/sjlim/files/SJLIM2009NaCrime.pdf
- IRS Internal Revenue Manual, double-entry system overview: https://www.irs.gov/irm/part4/irm_04-010-003
- IMF, bank reconciliation and fiscal data integrity: https://www.elibrary.imf.org/view/journals/061/2016/004/article-A001-en.xml
- Reserve Bank of India, internal controls and authorization, reconciliation and segregation: https://www.rbi.org.in/scripts/PublicationReportDetails.aspx?ID=514

These sources provide general background. The fictional BigBank design and events are invented for the story.
