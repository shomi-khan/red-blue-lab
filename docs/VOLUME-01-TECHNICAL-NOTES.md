# Volume 1 — Technical Notes

এই নোটগুলো গল্পে ব্যবহৃত system model-এর technical companion। Fictional BigBank-এর architecture বাস্তব ব্যাংকের একমাত্র বা universal design নয়; এটি শেখার জন্য একটি grounded model।

## 1. Salami Slicing Attack

Salami slicing-এ attacker প্রতিটি transaction বা account থেকে খুব অল্প অঙ্ক সরায়। Individual loss এত ছোট হয় যে victim বা monitoring threshold সেটিকে উপেক্ষা করতে পারে। বহু victim ও repeated execution-এ aggregate amount বড় হয়।

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

Volume 1-এর root cause একটি single magic exploit নয়। এটি একাধিক control weakness-এর সমন্বয়:
- Over-privileged service identity।
- Bulk adjustment-এর জন্য দুর্বল authorization boundary।
- Beneficiary change-এর independent approval যথেষ্ট নয়।
- Monitoring amount-centric; aggregate pattern ও destination concentration কম দেখা হয়।
- Business purpose ও customer-level authorization যথাযথভাবে enforce হয় না।

### Least privilege ও authorization boundary

Least Privilege হলো কোনো user বা service identity-কে তার নির্দিষ্ট কাজ সম্পন্ন করার জন্য প্রয়োজনীয় সর্বনিম্ন permission দেওয়া। একটি identity authenticated হলেই সে সব account debit, beneficiary change বা bulk operation চালাতে পারবে, এমন নয়। Authorization-এ identity, action, resource, business purpose, scope এবং approval context যাচাই করা প্রয়োজন।

## 6. Incident response

- **Containment:** সন্দেহজনক scheduled job pause; অতিরিক্ত permission revoke/limit।
- **Evidence preservation:** logs, configuration history, batch metadata, journal references read-only preserve।
- **Scope:** affected account ও transaction population নির্ধারণ।
- **Recovery:** original ledger entry না মুছে compensating credit/reversal।
- **Validation:** reconciliation, duplicate prevention, regression test এবং নতুন sweep হচ্ছে কি না monitor।

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
