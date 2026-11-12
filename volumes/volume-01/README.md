# Volume 1: The One-Poisha Theft

> BigBank-এর গ্রাহকদের account থেকে প্রতিদিন এক পয়সা করে উধাও হচ্ছে। Peter-এর চোখে প্রথম ধরা পড়া সেই ক্ষুদ্র ঘাটতিই খুলে দেয় এক বিশাল financial fraud-এর দরজা।

## অধ্যায় ১: এক পয়সার হিসাব

মাসের শেষ বৃহস্পতিবার। BigBrains-এর অফিসে দুপুরের পর কাজের গতি একটু ঢিলে হয়ে এসেছে। কয়েকজন developer lunch-এর পর কফি নিয়ে নিজেদের desk-এ ফিরেছে। Slack-এ release notification, code review আর production metrics-এর ভিড়।

Peter Parker নিজের banking app খুলল।

সে BigBrains-এ backend engineer। তিন বছর আগে BigBrains যখন BigBank-এর নতুন digital banking platform তৈরির contract পায়, Peter তখন সেই development team-এর একজন ছিল। Account service, transaction API এবং ledger integration নিয়ে সে কাজ করেছিল। Production system এখন তার হাতে নেই, আর সে জানে না গত তিন বছরে কী কী বদলেছে। তবু system-এর পুরোনো design decision-গুলো তার মাথায় আছে। কোনো অস্বাভাবিক আচরণ দেখলে সে component আর data flow নিয়ে ভাবতে পারে।

বেতন জমা হয়েছে।

সে প্রথমে payslip-এর সঙ্গে amount মিলিয়ে দেখল। তারপর account statement খুলল। Salary credit-এর পরের balance হিসাব করল। একবার। আবার।

এক পয়সা কম।

Peter ভ্রু কুঁচকে transaction details খুলল। Salary credit-এর amount ঠিক আছে। তার কয়েক মিনিট পর আরেকটি entry:

**Account Adjustment: -৳0.01**

সে লাইনটা কিছুক্ষণ দেখল।

“কী হয়েছে?” পাশের desk থেকে Nadia Karim জিজ্ঞেস করল।

“তোমার salary credit হয়েছে?”

“হ্যাঁ। কেন?”

“একবার statement দেখো তো।”

Nadia নিজের ফোনে banking app খুলল। কয়েক সেকেন্ড পর তার মুখের ভাব বদলে গেল।

“আমারটাতেও?”

“এক পয়সা?”

“হ্যাঁ।”

Ryan Chowdhury পাশ থেকে শুনে হেসে উঠল। “তোমরা দুজন মিলে এক পয়সার তদন্ত কমিটি খুলেছ?”

Peter ফোনটা তার দিকে বাড়িয়ে দিল। “তোমারটাও দেখো।”

Ryan অনিচ্ছায় app খুলল। প্রথমে সে কাঁধ ঝাঁকাল। তারপর statement-এর একই ধরনের entry দেখে হাসি থেমে গেল।

“আচ্ছা, এটা তো সত্যি।”

“তুমি কি কিছু notice করেছ?” Peter জিজ্ঞেস করল।

“না। এক পয়সা। হয়তো bank adjustment।”

“কিসের adjustment?”

Ryan উত্তর দিল না। সে ফোন পকেটে রেখে কাজে ফিরে গেল।

Peter আবার statement দেখল। Salary credit ঠিক। তারপর debit। অর্থাৎ BigBrains payroll file থেকে টাকা কম পাঠানো হয়নি। ব্যাংক account-এ টাকা জমা হওয়ার পর আলাদা transaction ঘটেছে।

এটা গুরুত্বপূর্ণ পার্থক্য।

সে BigBrains-এর payroll portal থেকে payslip download করল। Gross salary, deductions, net payable। সব ঠিক। তারপর ব্যাংকের statement export করল। দুই record পাশাপাশি রাখল।

Nadia তার পাশে এসে দাঁড়াল। “আমারটাও মিলিয়ে দেখবে?”

“অবশ্যই।”

দুটো statement-এ একই adjustment description। Timestamp-ও কাছাকাছি। Ryan-এরটাও প্রায় একই সময়ে।

তিনজনের account। একই bank। একই দিনে। একই অঙ্ক।

Peter তাদের transaction-এর সময় মিলিয়ে দেখল। কয়েক মিনিটের ব্যবধান। Salary credit-এর পরেই adjustment। সে Nadia-কে বলল, “একটা জিনিস খেয়াল করো। Payroll advice-এ net payable ঠিক আছে। Bank প্রথমে পুরো salary credit করেছে। তারপর আলাদা transaction তৈরি হয়েছে। যদি BigBrains কম টাকা পাঠাত, statement-এ salary credit-টাই কম দেখাত।”

Nadia বলল, “মানে সমস্যা payroll-এ নয়, bank-এর পরের processing-এ?”

“এখনই নিশ্চিত নই। কিন্তু আমাদের evidence ওই দিকেই ইঙ্গিত করছে।”

“Customer support-এ জানাও,” Nadia বলল।

Peter মাথা নাড়ল। “জানাব। কিন্তু আগে transaction reference-গুলো লিখে রাখি।”

সে তিনটি reference ID, posting time, amount এবং description একটি ছোট note-এ লিখল। তারপর BigBank-এর support portal-এ complaint তৈরি করল।

**Subject:** Unexplained ৳0.01 debit after salary credit

বর্ণনায় সে লিখল যে salary credit-এর পর account থেকে আলাদা করে এক পয়সা debit হয়েছে। একই ঘটনা তার দুই colleague-এর account-এও দেখা গেছে। সে জানতে চাইল, এই adjustment-এর business purpose কী এবং কোন policy অনুযায়ী এটি নেওয়া হয়েছে।

Submit করার পর confirmation screen এল।

Peter browser বন্ধ করল না। সে statement-এর দিকে আরেকবার তাকাল।

এক পয়সা।

অঙ্কটা এত ছোট যে কেউ চাইলে চোখ বুজে পাশ কাটিয়ে যেতে পারে। কিন্তু transaction-টা ঘটেছে। আর software system-এ কোনো transaction নিজে নিজে জন্মায় না। কোনো component সেটি তৈরি করেছে, কোনো rule সেটিকে অনুমতি দিয়েছে, কোনো ledger সেটিকে record করেছে।

কেউ না কেউ এই এক পয়সার হিসাব জানে।

Peter তখনও জানত না, একই মুহূর্তে BigBank-এর লাখ লাখ account-এ একই ছোট entry তৈরি হচ্ছে।

---

## অধ্যায় ২: যেটা কেউ দেখেনি

পরদিন সকালে BigBank-এর support থেকে উত্তর এল।

> আপনার account-এ প্রদর্শিত ৳0.01 adjustment একটি system-generated account adjustment। এটি account maintenance ও balance normalization process-এর অংশ। এতে উদ্বিগ্ন হওয়ার প্রয়োজন নেই।

Peter উত্তরটা দুবার পড়ল।

“Balance normalization?” সে নিজের মনে বলল।

তার account balance আগে থেকেই দুই decimal place-এ প্রদর্শিত হয়। এক পয়সা debit করার প্রয়োজন কী? আর adjustment হলে সেটি কোন rule-এর অধীনে? Customer agreement-এ কি এমন কোনো charge আছে?

সে support ticket-এ reply করল। Policy reference চাইল। Transaction category এবং beneficiary information জানতে চাইল।

দুপুরে আরেকটি উত্তর এল।

> বিষয়টি আমাদের standard processing-এর অংশ। আপনার account নিরাপদ আছে।

এবার Peter বিরক্ত হলো। সে account নিরাপদ কি না জিজ্ঞেস করেনি। সে জানতে চেয়েছে টাকা কেন কাটা হয়েছে।

সে Nadia-কে message করল। Nadia-ও নিজের account-এ একই description পেয়েছে। Ryan বলল, support-এ যোগাযোগ করে লাভ নেই, এক পয়সা নিয়ে আর সময় নষ্ট করতে চায় না।

Oliver Grant, BigBrains-এর team lead, বিষয়টি শুনে বললেন, “Payroll আমাদের দিক থেকে ঠিক আছে। payslip আর payroll export match করছে। Bank-side adjustment হলে সেটা BigBank-এর ব্যাপার।”

“আমি সেটাই বলছি,” Peter উত্তর দিল।

“তাহলে bank-কে জানাও। কিন্তু release-এর deadline ভুলে যেও না।”

Oliver-এর কথায় অসন্তুষ্ট হওয়ার কারণ ছিল না। তার দায়িত্ব BigBrains-এর delivery। ব্যাংকের transaction processing তার নিয়ন্ত্রণে নয়।

Peter নিজের laptop-এ একটি ছোট table বানাল:

| Source | Amount |
|---|---:|
| BigBrains payroll advice | ৳52,500.00 |
| BigBank salary credit | ৳52,500.00 |
| Subsequent account adjustment | -৳0.01 |
| Available balance impact | ৳52,499.99 |

সে আরেকটি বিষয় লক্ষ্য করল। Salary credit আর adjustment-এর timestamp-এর ব্যবধান খুব কম। এটি random manual correction-এর মতো দেখাচ্ছে না। একই pattern Nadia এবং Ryan-এর account-এও।

তিনটি observation থেকে এখনো fraud প্রমাণ হয় না। একই system-generated rule তিনটি account-এ legitimateভাবেও চলতে পারে।

কিন্তু legitimate হলে bank-এর policy থাকা উচিত।

Peter নতুন একটি message লিখল। এবার অভিযোগের বদলে প্রশ্নগুলো সাজাল:

- Adjustment কোন service বা business rule তৈরি করেছে?
- Customer consent বা account terms-এ এর ভিত্তি কী?
- একই সময়ে একাধিক account-এ একই adjustment কেন হয়েছে?
- Adjustment-এর matching credit কোন ledger account-এ গেছে?

শেষ প্রশ্নটি সে ইচ্ছা করেই রেখেছিল। Debit হলে accounting system-এ তার বিপরীত entry থাকা উচিত। টাকা কোথাও না কোথাও গেছে, অথবা কোনো accounting account-এ record হয়েছে।

এইবার সে support ticket-এর পাশাপাশি BigBank-এর official technical contact address-এও লিখল। সে উল্লেখ করল, BigBrains-এর banking platform development team-এ সে আগে কাজ করেছে। সে কোনো privileged access চাইছে না; শুধু একটি unexplained transaction-এর accountable explanation চাইছে।

তারপর সে অপেক্ষা করল।

বিকেলের দিকে Peter পুরোনো project notes খুলল। BigBank-এর platform development-এর সময় তারা transaction processing-কে আলাদা service-এ ভাগ করেছিল। Account service balance ও account state সামলাত; transaction service request validate করে ledger posting শুরু করত; ledger নিজে debit-credit record রাখত। সে মনে করার চেষ্টা করল, Micro-Adjustment Service তখনও ছিল কি না। তার মনে পড়ল, সেটি ছিল Core Operations-এর একটি ছোট internal tool। কিন্তু সে সেটির implementation করেনি।

তিন বছর আগের architecture diagram production-এর বর্তমান সত্য নয়। Peter নিজেকে মনে করিয়ে দিল, “পুরোনো knowledge hypothesis বানাতে সাহায্য করবে। Evidence-এর বিকল্প হবে না।”

---

## অধ্যায় ৩: Adrian Rahman

BigBank-এর Technical Head Adrian Rahman email-টি পড়লেন সকাল দশটা সতেরো মিনিটে।

তার inbox-এ customer complaint প্রতিদিনই আসে। বেশিরভাগই card decline, failed transfer, delayed notification অথবা app-এর display issue। কিন্তু এই message-টি অন্যরকম।

প্রেরক একজন software engineer। সে transaction-এর amount, timestamp, reference ID এবং একই pattern পাওয়া আরও দুই account-এর কথা উল্লেখ করেছে। সবচেয়ে গুরুত্বপূর্ণ, সে salary credit এবং পরবর্তী debit-কে আলাদা transaction হিসেবে চিহ্নিত করেছে।

Adrian নিচে scroll করলেন।

“Matching credit কোথায় গেছে?”

তিনি লাইনটি আবার পড়লেন।

এক পয়সা। অঙ্কটি তুচ্ছ। কিন্তু প্রশ্নটি তুচ্ছ নয়।

তিনি Head of Core Banking Engineering-কে ডাকলেন। “গত রাতের account adjustment batch-এর summary আনুন।”

দশ মিনিট পর একটি internal dashboard খুলল। Daily micro-adjustment count স্বাভাবিক range-এর মধ্যে। Total debit ও credit সমান। Failed transaction নেই।

“সব ঠিক আছে,” engineer বলল।

Adrian জিজ্ঞেস করলেন, “এই adjustment-এর business owner কে?”

Engineer কিছুক্ষণ থামল। “Core Operations-এর একটি shared workflow। Customer correction আর rounding adjustment-এর জন্য।”

“এটা কি customer fee?”

“না, সাধারণত না। Manual correction এবং system-generated adjustment।”

“তাহলে salary account-এ একই amount-এর debit কেন?”

Engineer উত্তর দিতে পারল না।

Adrian Peter-কে ফোন করলেন।

Adrian প্রথমে নিজের team-কে বলেছিলেন, customer complaint-এ মাত্র এক পয়সা উল্লেখ আছে বলে এটিকে low priority করা যায়। কিন্তু email-এর শেষ প্রশ্নটি তাকে থামিয়েছিল। Matching credit কোথায় গেছে? একজন customer শুধু balance নিয়ে অভিযোগ করলে support ticket হতে পারত। কিন্তু একজন engineer যখন debit-এর opposite side, policy এবং transaction origin জানতে চায়, তখন সেটি system integrity-এর প্রশ্ন।

তিনি জানতেন, bank-এর বড় ঝুঁকি সবসময় বড় অঙ্ক দিয়ে শুরু হয় না। কখনো কখনো বড় ক্ষতির প্রথম চিহ্ন এমন ছোট হয় যে প্রতিষ্ঠান নিজেই সেটিকে গুরুত্ব দিতে চায় না।

“Mr. Parker? আমি Adrian Rahman, BigBank থেকে বলছি। আপনার report পেয়েছি।”

“ধন্যবাদ। আমি শুধু জানতে চাই transaction-টা কেন হয়েছে।”

“আমিও সেটাই জানতে চাই। আপনি কি আজ বিকেলে আমাদের সঙ্গে দেখা করতে পারবেন?”

“পারব।”

“আপনার colleague-দের statement এবং payslip থাকলে আনবেন। Sensitive information ঢেকে দেবেন। আমরা শুধু relevant transaction details দেখতে চাই।”

ফোন রাখার পর Peter কিছুক্ষণ চুপ করে বসে রইল। Support team যেটাকে standard adjustment বলে বন্ধ করতে চেয়েছিল, Technical Head সেটিকে investigation-এর বিষয় হিসেবে দেখছেন।

বিকেলে BigBank-এর conference room-এ Peter-এর সামনে বসে ছিলেন Adrian, Core Banking Engineering-এর Maya Sen এবং Fraud Operations-এর Daniel Brooks।

Adrian শুরু করলেন, “আমরা এখনো জানি না এটা fraud কি না। আপনার observation একটি anomaly। আমাদের কাজ হলো evidence দিয়ে সেটি যাচাই করা।”

Peter মাথা নাড়ল। “আমি একমত।”

Maya তিনটি transaction reference পরীক্ষা করলেন। “এই adjustment আমাদের Micro-Adjustment Service থেকে এসেছে।”

“এই service কী করে?” Peter জিজ্ঞেস করল।

“Customer account-এর ছোট correction, কিছু rounding-related entry, আর approved operational adjustment। সব transaction ledger-এ record হয়।”

“এটা কি প্রতিটি customer account-এ চালানো যায়?”

Maya বললেন, “Service-এর scope বড়। কিন্তু সব operation অনুমোদিত workflow দিয়ে হতে হয়।”

Adrian স্ক্রিনের দিকে তাকালেন। “তাহলে আমরা প্রথমে জানতে চাইব, এই নির্দিষ্ট adjustment-এর authorization কোথা থেকে এসেছে।”

সেদিন Peter কোনো production access পেল না। কোনো secret dashboard-ও খুলে দেওয়া হলো না। কিন্তু সে investigation-এর অংশ হলো।

Adrian একটি সীমা পরিষ্কার করে দিলেন। “আপনি system-এর আগের development team-এ ছিলেন, তাই আপনার context মূল্যবান। কিন্তু production evidence শুধু authorized bank staff সংগ্রহ করবে। আপনি sanitized data নিয়ে analysis করতে পারবেন। আমরা চাই investigation-টা clean থাকুক।”

Peter এতে স্বস্তি পেল। সে সাহায্য করতে এসেছে, নিজের পুরোনো access দেখাতে নয়।

Conference room থেকে বের হওয়ার আগে Adrian বললেন, “এক পয়সা ছোট হতে পারে। কিন্তু যদি একই কাজ হাজার হাজার account-এ ঘটে, সেটা আর ছোট থাকে না।”

Peter উত্তর দিল, “আমি সেটাই ভাবছি।”

---

## অধ্যায় ৪: হিসাব মিলে যাচ্ছে

পরের দিন Maya একটি sanitized transaction extract নিয়ে এলেন। এতে customer name, account number বা ব্যক্তিগত তথ্য ছিল না। শুধু synthetic investigation ID, amount, timestamp, transaction type, source reference এবং destination ledger reference।

Peter প্রথমে amount column দেখল।

সব debit ৳0.01।

সে তারপর transaction count দেখল। সংখ্যাটা তার প্রত্যাশার চেয়ে অনেক বেশি।

“এগুলো সব Micro-Adjustment Service-এর?” সে জিজ্ঞেস করল।

Maya বললেন, “হ্যাঁ। তবে সবগুলো একই batch-এর নয়।”

Daniel বললেন, “আমাদের fraud system amount threshold ব্যবহার করে। এক পয়সার transaction আলাদা করে high-risk হিসেবে mark হয়নি।”

Peter বলল, “কিন্তু amount ছোট হলেই risk ছোট হয় না।”

Adrian বললেন, “সেটা প্রমাণ করতে হবে।”

Maya ledger summary খুললেন। প্রতিটি debit-এর বিপরীতে matching credit আছে। Journal total balanced।

Peter কিছুক্ষণ স্ক্রিনের দিকে তাকিয়ে রইল।

“তাহলে arithmetic mismatch নেই।”

“ঠিক,” Maya বললেন। “Ledger-এর debit ও credit সমান।”

Peter টেবিলে কলম রাখল। “কিন্তু transaction বৈধ ছিল, সেটা কি ledger balance প্রমাণ করে?”

ঘরে নীরবতা নেমে এল।

Maya মাথা নাড়লেন। “না। Ledger balance শুধু বলে accounting entry-গুলো গাণিতিকভাবে মিলে গেছে। কে অনুমোদন করেছে, কেন করেছে, beneficiary সঠিক কি না, এগুলো আলাদা প্রশ্ন।”

Adrian বললেন, “আমাদের investigation-এ এই distinction-টাই ধরে রাখতে হবে।”

### Double-entry ledger: হিসাবের দুই দিক

একটি ব্যাংকিং ledger-এ প্রতিটি financial transaction-এর accounting effect থাকে। Double-entry bookkeeping-এ একটি transaction-এর debit ও credit side সমানভাবে record হয়। ফলে মোট হিসাব balanced থাকে।

উদাহরণ:

| Entry | Debit | Credit |
|---|---:|---:|
| Customer account | ৳0.01 | |
| Destination account | | ৳0.01 |

এখানে ledger গাণিতিকভাবে ঠিক। কিন্তু destination account-এ টাকা পাঠানোর অনুমতি ছিল কি না, customer-এর কাছ থেকে debit করার বৈধ business reason ছিল কি না, সেটি ledger-এর যোগ-বিয়োগ দিয়ে বোঝা যায় না।

এটাই investigation-এর গুরুত্বপূর্ণ বাঁক।

**A balanced ledger is not proof of an authorized transaction.**

Reconciliation-ও একইভাবে দুই বা তার বেশি independent record মিলিয়ে পার্থক্যের কারণ খোঁজে। এটি transaction completeness ও accounting consistency যাচাইয়ে সাহায্য করে; কিন্তু ভুল business rule বা unauthorized beneficiary-কে নিজে থেকে বৈধ করে না।

Adrian একটি প্রশ্ন করলেন, “যদি সব debit-এর matching credit একই account-এ যায়?”

Peter এবার ledger-এর দিকে নয়, transaction-এর business meaning-এর দিকে তাকাল। “আমরা যদি শুধু debit total আর credit total মিলাই, তাহলে money movement-এর arithmetic বুঝব। কিন্তু customer কেন টাকা দিল, সেই debit-এর authority কী, beneficiary কে, এবং adjustment code-টা সেই কাজের জন্য অনুমোদিত কি না, সেগুলো আলাদা control।”

Maya বললেন, “তুমি ঠিক বলছ। Ledger আমাদের বলে কী record হয়েছে। Authorization record বলে কে কী করতে পারত। Business policy বলে কোন কাজটি করা উচিত ছিল।”

Maya report filter করলেন।

একটি destination reference বারবার দেখা যাচ্ছে।

Daniel সামনে ঝুঁকলেন। “এটা কি suspense account?”

“না,” Maya বললেন। “এটি একটি beneficiary-linked internal destination।”

Peter বলল, “তাহলে আমরা এখন জানি টাকা হারায়নি। কোথায় গেছে, সেটি trace করা সম্ভব।”

Adrian বললেন, “আমরা এখনো জানি না beneficiary-এর পরিচয় বা transaction-এর intent। কিন্তু pattern পেয়েছি।”

Peter-এর মনে হলো, এক পয়সার ঘটনাটি আর বিচ্ছিন্ন নেই। এটি একটি system-level behavior।

---

## অধ্যায় ৫: সালামির এক টুকরো

সেদিন রাতে Peter বাসায় ফিরে laptop খুলল। Adrian-এর অনুমতিতে পাওয়া sanitized extract তার সামনে। সে কোনো live system-এ যুক্ত হয়নি। শুধু অনুমোদিত evidence নিয়ে কাজ করছে।

প্রথমে সে transaction count এবং destination reference-এর frequency তুলনা করল। একই destination-এ বহু ছোট credit যাচ্ছে।

তার মাথায় একটি পুরোনো ধারণা ফিরে এল। ক্ষুদ্র অঙ্ক, বহু account, একই beneficiary, পুনরাবৃত্তি।

সে search করল: **Salami Slicing Attack**।

কিছুক্ষণ পড়ার পর সে চেয়ারে হেলান দিল।

Salami slicing হলো এমন financial fraud, যেখানে প্রতিটি victim-এর কাছ থেকে খুব অল্প পরিমাণ অর্থ নেওয়া হয়। আলাদা করে দেখলে প্রতিটি ঘটনা তুচ্ছ মনে হয়; কিন্তু বহু account বা বহু transaction জুড়ে সেই ক্ষুদ্র অংশগুলো জমে বড় অঙ্ক তৈরি করে। ঐতিহাসিক উদাহরণে rounding calculation-এর discarded fraction অন্য account-এ জমা করার কৌশলও দেখা যায়।

এখানে Larfleeze-এর সম্ভাব্য পদ্ধতি আরও সরাসরি: প্রতিটি eligible account থেকে এক পয়সা debit, তারপর matching credit নিজের নিয়ন্ত্রণাধীন destination-এ।

Peter কাগজে হিসাব করল।

ধরা যাক, একটি sweep-এ 2.4 million account থেকে এক পয়সা করে নেওয়া হলো।

৳0.01 × 2,400,000 = ৳24,000।

এক দিনে চব্বিশ হাজার টাকা।

ত্রিশ দিনে?

৳24,000 × 30 = ৳720,000।

প্রতিটি customer হয়তো এক পয়সা দেখে shrug করবে। কিন্তু সব customer-এর ক্ষতি একসঙ্গে করলে সেটি আর ছোট নয়।

পরদিন সে Adrian-কে বলল, “আমার মনে হয় এটা Salami Slicing Attack-এর একটি variation।”

Adrian বললেন, “নামটা শুনেছি। কিন্তু আমি চাই তুমি নামের সঙ্গে evidence-ও দেখাও।”

Peter একটি ছোট calculation sheet দেখাল। “একটি account-এ এক পয়সা। দশটি account-এ দশ পয়সা। এক লাখ account-এ এক হাজার টাকা। প্রতিটি customer-এর চোখে amount প্রায় অদৃশ্য, কিন্তু system-এর aggregate view-তে সেটা আলাদা হওয়া উচিত।”

Nadia report-এ account count-এর distribution যোগ করল। Ryan timestamp group করল। তারা কেউই attacker-এর intent প্রমাণ করতে পারছিল না, কিন্তু একই service path ও beneficiary-এর সঙ্গে repeated one-paisa entry-এর সম্পর্ক ক্রমশ স্পষ্ট হচ্ছিল।

Adrian জিজ্ঞেস করলেন, “তুমি কতটা নিশ্চিত?”

“এখনো hypothesis। কিন্তু repeated micro-debit, একই destination, আর একই service path—এই তিনটি clue একসঙ্গে আছে।”

Daniel বললেন, “আমাদের fraud model individual transaction amount দেখে। এক পয়সা threshold-এর নিচে।”

Peter উত্তর দিল, “তাহলে amount নয়, pattern দেখতে হবে। কতগুলো account আক্রান্ত, একই destination-এ কত credit, একই service identity থেকে কত adjustment, এবং সময়ের সঙ্গে total কত বাড়ছে।”

Maya report-এ aggregate view যোগ করলেন।

একটি daily pattern স্পষ্ট হতে শুরু করল। Adjustment-এর সংখ্যা অস্বাভাবিকভাবে বড়। প্রতিটি amount ছোট, কিন্তু destination concentration অত্যন্ত বেশি।

“এটা rounding residue নয়,” Maya বললেন। “Rounding residual বিভিন্ন transaction থেকে আসতে পারে। কিন্তু এখানে প্রতিটি debit-এর amount একই এবং destination-ও একই।”

Adrian ধীরে বললেন, “তাহলে কেউ একটা legitimate workflow-কে অন্য কাজে ব্যবহার করছে।”

Peter স্ক্রিনে তাকিয়ে রইল।

“কেউ জানে Micro-Adjustment Service কীভাবে কাজ করে। অথবা কেউ এমন access পেয়েছে, যেটা দিয়ে service-কে ভুল নির্দেশ দেওয়া যায়।”

### অন্য প্রান্তে

একটি ছোট ঘরে Larfleeze monitor-এর দিকে তাকিয়ে ছিল। তার সামনে কোনো flashy dashboard ছিল না। কয়েকটি সংখ্যা, একটি running total, আর প্রতিদিনের status। প্রতিটি account থেকে কাটা অংশ এত ক্ষুদ্র যে আলাদা করে কেউ সময় নষ্ট করবে না, এটাই তার ধারণা। তার কাছে customer-দের সংখ্যা ছিল opportunity; আর bank-এর routine adjustment process ছিল আড়াল।

সে balance বাড়তে দেখল। পরিমাণটা এখনও তার প্রত্যাশার তুলনায় ছোট, কিন্তু প্রতিদিনের পুনরাবৃত্তি তাকে ধৈর্য ধরতে শিখিয়েছে। সে জানত, বড় চুরি মানুষের চোখে পড়ে। ছোট চুরি মানুষের অভ্যাসের ফাঁক দিয়ে ঢুকে যায়।

সে জানত না, BigBank-এর ভেতরে কয়েকজন মানুষ ইতিমধ্যে সেই pattern গুনতে শুরু করেছে।

---

## অধ্যায় ৬: অদৃশ্য অনুমতি

Maya investigation room-এর display-তে Micro-Adjustment Service-এর architecture দেখালেন।

~~~mermaid
flowchart TD
    A[Approved Adjustment Request] --> B[Authorization Check]
    B --> C[Micro-Adjustment Service]
    C --> D[Core Ledger]
    D --> E[Customer Account Debit]
    D --> F[Beneficiary Credit]
    D --> G[Audit Journal]
    G --> H[Reconciliation]
~~~

“এই service-এর উদ্দেশ্য খারাপ নয়,” Maya বললেন। “Operational correction-এর জন্য দরকার হয়। কোনো ভুল posting হলে approved correction করা যায়। কিন্তু production-এ এর ক্ষমতা সীমাবদ্ধ থাকা উচিত।”

Peter diagram-এর Authorization Check অংশে আঙুল রাখল।

“এই check কী যাচাই করে?”

“Request এসেছে approved service identity থেকে কি না, request type অনুমোদিত কি না, আর operator approval আছে কি না।”

“কিন্তু কোন account debit হবে আর কোন beneficiary credit পাবে, সেটা কি একই approval-এর মধ্যে বাঁধা?”

Maya কিছুক্ষণ চুপ করে থাকলেন। “এটাই আমরা যাচাই করছি।”

Audit team configuration history পরীক্ষা করল। কয়েক সপ্তাহ আগে Micro-Adjustment workflow-এর একটি policy change হয়েছিল। Change request-এ routine maintenance লেখা ছিল। কিন্তু change-এর scope ও approval trail যথেষ্ট পরিষ্কার ছিল না।

আরও গভীরে গিয়ে তারা একটি service identity পেল, যার permission প্রয়োজনের চেয়ে বেশি। এটি operational correction-এর জন্য তৈরি, কিন্তু তার authority দিয়ে অনেক account-এ adjustment চালানো সম্ভব।

Peter বলল, “তাহলে authentication ঠিক থাকলেও authorization ভুল হতে পারে।”

Adrian মাথা নাড়লেন। “একটি পরিচয় বৈধ হতে পারে। কিন্তু সেই পরিচয়ের প্রতিটি কাজ বৈধ হয় না।”

### Authentication বনাম Authorization

- **Authentication:** কে বা কোন service request পাঠাচ্ছে, তা যাচাই।
- **Authorization:** সেই identity নির্দিষ্ট resource-এ নির্দিষ্ট কাজ করতে পারবে কি না, তা যাচাই।

একটি service identity authenticated হলেই সেটিকে সব account থেকে টাকা debit করার ক্ষমতা দেওয়া উচিত নয়। Least Privilege-এর অর্থ হলো প্রতিটি identity-কে কাজের জন্য যতটুকু permission প্রয়োজন, ততটুকুই দেওয়া।

Investigation team আরও তিনটি control gap চিহ্নিত করল:

1. একই service identity বহু customer account-এ adjustment করতে পারছিল।
2. Beneficiary destination পরিবর্তনের জন্য independent approval যথেষ্ট শক্ত ছিল না।
3. Monitoring individual amount দেখলেও beneficiary concentration এবং repeated pattern যথেষ্ট গুরুত্ব দিয়ে দেখছিল না।

এখনো তারা জানত না Larfleeze ঠিক কীভাবে initial access পেয়েছে। Configuration change-এর audit trail সন্দেহজনক, কিন্তু attribution-এর জন্য আরও evidence দরকার।

Maya একটি গুরুত্বপূর্ণ finding তুলে ধরলেন। Micro-Adjustment Service-এর service identity আগে সীমিত correction request process করত। পরে তার scope বাড়ানো হয়েছিল। নতুন permission-এ bulk account adjustment এবং beneficiary mapping-এর মতো sensitive operation এসে যায়। Change request-এ business justification ছিল, কিন্তু risk review এবং independent approval-এর evidence অসম্পূর্ণ।

“এই change কে করেছে?” Peter জিজ্ঞেস করল।

“একটি authorized operator identity দিয়ে change submit হয়েছে,” Maya বললেন। “কিন্তু identity ব্যবহার করেছে যে ব্যক্তি, সে-ই প্রকৃত actor কি না, সেটা আমরা এখনো জানি না।”

Adrian বললেন, “Attribution পরে। এখন আমরা জানি, একটি identity-র ক্ষমতা প্রয়োজনের চেয়ে বেশি। আর সেই ক্ষমতা ব্যবহার করে customer account থেকে debit তৈরি করা হয়েছে।”

Peter বলল, “আমরা attacker-এর নাম জানার অপেক্ষা করতে পারি না। এই permission দিয়ে টাকা সরানো সম্ভব হলে আগে সেই পথ বন্ধ করতে হবে।”

Adrian তার দিকে তাকালেন। “ঠিক। প্রথম লক্ষ্য containment।”

---

## অধ্যায় ৭: বন্ধ করার সময়

Adrian incident response team-কে আনুষ্ঠানিকভাবে সক্রিয় করলেন।

তারা প্রথমে কোনো code deploy করল না। কোনো database row delete করল না। কোনো log পরিষ্কার করল না।

প্রথম কাজ ছিল evidence সংরক্ষণ।

Audit log, configuration version, service identity event, batch metadata, journal reference এবং beneficiary mapping-এর read-only copy তৈরি করা হলো। প্রতিটি artifact-এর collection time ও integrity metadata নথিভুক্ত করা হলো।

তারপর team containment plan তৈরি করল।

**প্রথম সিদ্ধান্ত:** Micro-Adjustment Service-এর scheduled bulk operation সাময়িকভাবে pause করা হবে।

**দ্বিতীয় সিদ্ধান্ত:** সন্দেহজনক service identity-এর ক্ষমতা revoke বা সীমিত করা হবে। Legitimate correction-এর জন্য আলাদা, narrowly scoped approval path রাখা হবে।

**তৃতীয় সিদ্ধান্ত:** সন্দেহজনক beneficiary account-এর ওপর bank-এর authorized fraud-control process অনুযায়ী restriction আরোপ করা হবে। এটি evidence ও legal process বিবেচনা করে করা হবে।

**চতুর্থ সিদ্ধান্ত:** আক্রান্ত account-গুলোর তালিকা তৈরি করে প্রতিটি debit-এর matching credit ও journal reference যাচাই করা হবে।

Peter একটি বিষয় জোর দিয়ে বলল। “পুরোনো ledger entry মুছে ফেললে হবে না। Original event থাকতে হবে। ভুল transaction-এর বিপরীতে compensating entry দিতে হবে।”

Maya বললেন, “ঠিক। আমরা original journal preserve করব, তারপর authorized reversal বা compensating credit post করব।”

### কেন original transaction মুছে ফেলা যাবে না?

Financial ledger হলো system of record। কোনো ভুল entry ঘটলে সেটিকে চুপচাপ delete করে history পাল্টে দেওয়া উচিত নয়। বরং original entry traceable রেখে correction entry যোগ করা হয়।

এতে audit trail থাকে, কে কখন কী সংশোধন করেছে তা বোঝা যায়, এবং reconciliation করা সম্ভব হয়।

Team একটি controlled recovery batch তৈরি করল। প্রথমে synthetic test environment-এ কয়েকটি test account দিয়ে যাচাই করা হলো:

- একই debit যেন দ্বিতীয়বার reverse না হয়।
- যে account-এ debit হয়েছিল, কেবল সেই account-ই credit পায়।
- Original transaction reference-এর সঙ্গে compensating entry link থাকে।
- Total debit ও credit আবার reconcile হয়।
- Retry হলে duplicate refund তৈরি না হয়।

শেষের বিষয়টি গুরুত্বপূর্ণ। Distributed system-এ retry স্বাভাবিক। কোনো request-এর response হারিয়ে গেলে client বা scheduler আবার চেষ্টা করতে পারে। Idempotency এমনভাবে operation design করে, যাতে একই logical request একাধিকবার এলেও duplicate financial effect না ঘটে।

সব test pass করার পর Adrian production change অনুমোদন করলেন।

তবে containment-এর আগে তারা একটি শেষ প্রশ্ন করল: Micro-Adjustment Service পুরোপুরি বন্ধ করলে legitimate customer correction আটকে যাবে কি না? Operations team জানাল, manual exception process চালু আছে। Bulk sweep বন্ধ রেখেও জরুরি correction dual approval দিয়ে করা যাবে। তাই bank পুরো ledger বা transaction platform বন্ধ না করে শুধু সন্দেহজনক scheduled path pause করার সিদ্ধান্ত নিল।

এটাই ছিল proportionate containment: ঝুঁকির পথ বন্ধ করা, কিন্তু প্রয়োজনীয় banking service অকারণে অচল না করা।

Micro-Adjustment bulk job বন্ধ হলো।

একটি ছোট status update screen-এ দেখা গেল:

**Scheduled sweep: PAUSED**

কেউ হাততালি দিল না। কাজ শেষ হয়নি। এখনো জানতে হবে কত account আক্রান্ত, কত টাকা সরানো হয়েছে, আর customer-দের balance কীভাবে ঠিক করা হবে।

তবু বহু দিনের মধ্যে প্রথমবারের মতো নতুন এক পয়সা আর সরানো হচ্ছে না।

---

## অধ্যায় ৮: শেষ পয়সা

পরবর্তী আটচল্লিশ ঘণ্টা ছিল হিসাব, verification আর customer protection-এর।

Bank team আক্রান্ত account-এর population নির্ধারণ করল। প্রতিটি debit-এর বিপরীতে destination credit এবং journal record মিলিয়ে দেখা হলো। কোনো transaction বাদ পড়েছে কি না, duplicate হয়েছে কি না, বা অন্য কোনো adjustment category একই mechanism ব্যবহার করেছে কি না, তা পরীক্ষা করা হলো।

Peter ও Nadia sanitized report নিয়ে কাজ করল। Ryan-ও এবার সাহায্য করল। সে প্রথম দিন যে এক পয়সাকে তুচ্ছ বলেছিল, এখন প্রতিটি row মন দিয়ে দেখছে।

“এই একটা column দেখো,” Ryan বলল। “Beneficiary reference-এর distribution।”

Peter তাকাল।

একটি destination reference অস্বাভাবিকভাবে বেশি credit পেয়েছে। তবে তারা সেটিকে একাই অপরাধের প্রমাণ বলল না। Bank-এর internal ownership record, approval history এবং audit event-এর সঙ্গে মিলিয়ে দেখা হলো।

Adrian recovery report review করলেন। Affected customer account-গুলোতে compensating credit পাঠানোর পরিকল্পনা অনুমোদিত হলো। প্রতিটি correction original debit reference-এর সঙ্গে যুক্ত। Customer communication-এ বলা হলো, bank একটি unauthorized account adjustment শনাক্ত করেছে, প্রভাবিত balance সংশোধন করছে এবং সংশ্লিষ্ট control উন্নত করছে।

Peter-এর account-এও correction এলো।

**Adjustment Reversal: +৳0.01**

সে transaction details খুলে দেখল। Original debit মুছে যায়নি। তার বিপরীতে নতুন credit entry এসেছে।

“এবার ঠিক?” Nadia জিজ্ঞেস করল।

“আমার account-এ হ্যাঁ। কিন্তু শুধু আমারটা ঠিক হলেই হবে না।”

Bank-wide verification চলল। নতুন sweep আর তৈরি হয়নি।

তারা শুধু একটি successful test দেখে থামেনি। পরবর্তী scheduled window-গুলোতে নতুন debit তৈরি হচ্ছে কি না পর্যবেক্ষণ করা হলো। Monitoring alert-এ beneficiary concentration, per-account adjustment frequency, service identity এবং reason-code distribution যোগ করা হলো। Bulk adjustment-এর জন্য maximum scope, explicit business purpose, independent approval এবং time-bound authorization বাধ্যতামূলক করা হলো।

Adrian একটি review meeting-এ বললেন, “আমরা শুধু এই attack বন্ধ করব না। একই control weakness অন্য কোনো service-এ আছে কি না, সেটাও খুঁজব।” Suspicious service identity-এর authority সীমিত। Beneficiary configuration change-এ dual approval বাধ্যতামূলক। Monitoring rule-এ amount threshold-এর পাশাপাশি account count, shared destination, service identity এবং repeated adjustment pattern যোগ হয়েছে।

Reconciliation report-এ সব affected entry explain করা গেছে। কোনো unexplained difference বাকি নেই। Recovery batch-এর duplicate effect পাওয়া যায়নি।

Adrian conference room-এ Peter-কে ডাকলেন।

“তুমি প্রথম দিন শুধু এক পয়সা নিয়ে প্রশ্ন করেছিলে,” তিনি বললেন। “আজ আমরা জানি, সেটি ছিল অনেক বড় সমস্যার সবচেয়ে ছোট দৃশ্যমান অংশ।”

Peter জানালার বাইরে তাকাল। “আমি শুধু জানতে চেয়েছিলাম টাকা কোথায় গেল।”

“আর তুমি সেটা খুঁজে বের করতে সাহায্য করেছ।”

Peter মাথা নাড়ল। “আমরা সবাই করেছি।”

Adrian একটি report বন্ধ করলেন। “আমাদের তদন্ত এখনো শেষ হয়নি। কে প্রথম configuration বদলেছে, তার পেছনে কে ছিল, সব প্রশ্নের উত্তর পাইনি। কিন্তু unauthorized sweep বন্ধ। Customers-এর ক্ষতি সংশোধন হচ্ছে। আপাতত সেটাই সবচেয়ে জরুরি।”

সেদিন সন্ধ্যায় Peter BigBrains-এ ফিরল।

Oliver তার desk-এর পাশে এসে দাঁড়াল। “তোমার bank investigation কেমন হলো?”

“একটা বড় problem ছিল। আমরা সেটা থামিয়েছি। এখন recovery আর verification চলছে।”

Oliver বললেন, “তুমি তো ওই system বানানোর সময় team-এ ছিলে। কেমন লাগছে?”

Peter কিছুক্ষণ ভেবে বলল, “একটা system তৈরি করার সময় আমরা feature আর correctness নিয়ে ভাবি। কিন্তু production-এ system-এর permission, operation আর oversight ঠিক আছে কি না, সেটাও সমান জরুরি। Code ঠিক থাকলেও control ভুল হতে পারে।” Ryan তার desk-এর পাশে এসে দাঁড়াল।

“এক পয়সা,” Ryan বলল, “শেষ পর্যন্ত বেশ দামি হয়ে গেল।”

Peter হেসে ফেলল। “এক পয়সা দামি ছিল না। আমরা সেটাকে গুরুত্ব দিইনি, সেটাই দামি হয়ে যাচ্ছিল।”

অন্যদিকে, শহরের অন্য প্রান্তে একটি অন্ধকার ঘরে কেউ একটি account dashboard বন্ধ করল।

Larfleeze-এর প্রত্যাশিত balance আর বাড়ছে না।

সে কোনো arrest notice দেখল না। কোনো police siren শুনল না। শুধু একটি scheduled transfer status বদলে গেছে।

**FAILED — AUTHORIZATION REVOKED**

সে কিছুক্ষণ screen-এর দিকে তাকিয়ে রইল।

তারপর ধীরে laptop বন্ধ করল।

Peter জানত না Larfleeze কোথায়। Adrian-ও জানতেন না। কিন্তু BigBank-এর customer account থেকে আর এক পয়সাও ওই পথে যাচ্ছে না।

সেই রাতের জন্য, সেটাই যথেষ্ট ছিল।

---

## সমাপ্তি

একটি ক্ষুদ্র transaction পুরো banking system-এর integrity প্রশ্নের মুখে ফেলেছিল। Peter-এর জয় কোনো spectacular hack নয়। সে anomaly দেখেছে, evidence সংগ্রহ করেছে, hypothesis পরীক্ষা করেছে এবং bank-এর authorized team-এর সঙ্গে attack বন্ধ করেছে।

Larfleeze-কে ধরা যায়নি। কিন্তু তার পরিকল্পনা থেমেছে।

**একটি নিরাপদ system শুধু হিসাব মেলালেই নিরাপদ হয় না। প্রতিটি transaction-এর বৈধ উদ্দেশ্য, অনুমোদন এবং traceable history থাকতে হয়।**
