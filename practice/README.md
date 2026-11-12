# Practice Lab

এখানে পাঠক গল্পের character-দের মতো বাস্তব engineering ও investigation problem হাতে-কলমে সমাধান করবে। প্রতিটি practice আলাদা, self-contained folder।

## Practice-এর ধরন

| ধরন | কী পাবে | কী করবে |
|---|---|---|
| **File-based investigation** | Synthetic evidence file, README ও investigation brief | নিজের tool তৈরি করে দেওয়া data বিশ্লেষণ করবে |
| **Environment-based practice** | README-তে problem statement, scope ও constraints | নিজের অনুমোদিত local environment থেকে data সংগ্রহ করে tool তৈরি ও ব্যবহার করবে |

## Practice তালিকা

### 1. [BigBank: The One-Poisha Trail](./bigbank-salami-slicing/)
- **ধরন:** File-based investigation
- **POV:** Peter Parker ও BigBank investigation team
- **সমস্যা:** বহু account-এ repeated micro-debit এবং একই beneficiary-তে credit-এর pattern খুঁজে বের করা।
- **তৈরি করবে:** Transaction evidence analyzer।

### 2. [Who Is on My Local Network?](./local-network-inventory/)
- **ধরন:** Environment-based practice
- **সমস্যা:** নিজের machine-এর local network থেকে পাওয়া neighbor/ARP তথ্য parse করে device inventory তৈরি করা।
- **তৈরি করবে:** Local network inventory tool।

## কাজ করার নিয়ম

1. প্রতিটি practice-এর README-তে থাকা scope ও objective আগে পড়ো।
2. গল্পে শেখানো concept এবং প্রয়োজনীয় technical note দেখে নাও।
3. README-তে constraint না থাকলে নিজের পছন্দের language ও library বেছে নাও।
4. ছোট, testable version দিয়ে শুরু করো।
5. Acceptance criteria দিয়ে কাজ যাচাই করো।
6. Hypothesis, evidence, limitation ও conclusion আলাদা করে লেখো।

## Safety

- File-based practice-এর data synthetic; বাস্তব customer বা credential data নয়।
- Environment-based practice কেবল নিজের machine, নিজের local network বা অনুমোদিত lab-এ চালাবে।
- কোনো third-party network scan, credential collection বা unauthorized probing করবে না।
- কোনো practice active probing অনুমোদন না করলে passive local OS data দিয়েই কাজ করবে।

Practice optional। গল্প পড়তে এগুলো করা বাধ্যতামূলক নয়।
