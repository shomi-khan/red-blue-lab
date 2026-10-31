# Chapter 00 Background: তদন্তের প্রথম নিয়ম

[টুল তৈরির নির্দেশনা ও Lab specification পড়ো](README.md)।

## অধ্যায়ের গল্প: যে কাজটি শুরু হওয়ার আগেই থেমে গেল

সন্ধ্যার দিকে incident room-এ Rayhan একটি ছোট ticket খুলল। Internal service থেকে পাওয়া response প্রত্যাশিত ছিল না, কিন্তু ticket-এ request, timestamp, target বা reproduction steps নেই। কয়েকজন সহকর্মী একই ফলাফল আবার দেখতে পারেনি। Rayhan-এর প্রথম ইচ্ছা service-টি চালিয়ে দেখা। Samia তাকে থামাল।

“কোন service? কোন environment? আমাদের অনুমতি কোথায় লেখা আছে?”

Requester-এর note-এ isolated training environment-এর কথা আছে, কিন্তু নির্দিষ্ট target বা পরীক্ষার সীমা নেই। তারা বুঝল, ticket-টি কাজ শুরুর অনুমতি নয়। তাই scope পরিষ্কার না হওয়া পর্যন্ত বাইরের কোনো host-এ পরীক্ষা হবে না। নিজেদের machine-এ controlled lab তৈরি হবে, যেখানে প্রতিটি input, output ও failure পুনরায় তৈরি করা যাবে।

“প্রথমে lab, তারপর evidence,” Samia বলল। “যে পরিবেশে কী চলছে জানি না, সেখানে পাওয়া ফল verify করবে কীভাবে?”

তারা challenge specification পড়ার নিয়ম স্থির করল: objective, input, output, constraints, failure behavior এবং acceptance criteria। Rayhan বুঝল, specification কেবল কাজের তালিকা নয়; ভুল problem solve করা থেকে বাঁচার চুক্তি। প্রথমে Go program, তারপর loopback-এ সীমাবদ্ধ TCP server, সবশেষে client দিয়ে নির্দিষ্ট message পাঠিয়ে response যাচাই। এই ক্ষুদ্র exchange incident-এর উত্তর নয়, কিন্তু পরবর্তী তদন্তের নির্ভরযোগ্য fixture হবে।

### 00.1: কাজ শুরুর আগে প্রশ্ন
Rayhan দ্রুত editor খুলতে চেয়েছিল। Samia তাকে specification-এর প্রতিটি বাক্য observable শর্তে ভাঙতে বলল। তারা objective, input, output, constraint ও acceptance criteria আলাদা করল। এতে ধরা পড়ল, ticket-এ মূল target অনির্দিষ্ট। প্রথম milestone-এ পাঠক শিখবে কীভাবে এই অস্পষ্টতা শনাক্ত করে scope লিখে রাখতে হয়।

### 00.2: প্রথম executable evidence
Lab-এর নিয়ম স্থির হলে Rayhan একটি ছোট program চালাতে চায়। Samia বলে, “এখনো network-এ যেও না। আগে toolchain-কে নির্ভরযোগ্য করো।” Go program build, run ও test করে তারা নিশ্চিত হবে, পরবর্তী experiment-এর failure-কে compiler সমস্যার সঙ্গে গুলিয়ে ফেলবে না।

### 00.3: নিয়ন্ত্রিত TCP service
Server প্রয়োজন, কিন্তু Rayhan সব interface-এ bind করতে চাইলে Samia আপত্তি করে। এই অধ্যায়ের লক্ষ্য remote access নয়; local fixture। Server কেবল loopback-এ listen করবে, connection গ্রহণ করবে এবং নির্ধারিত response দেবে।

### 00.4: Client দিয়ে কথোপকথন যাচাই
Server চালু থাকলেই client সঠিকভাবে কথা বলেছে, তা প্রমাণ হয় না। Rayhan নির্দিষ্ট destination-এ connect করে message পাঠাবে ও response পড়বে। Server বন্ধ থাকলে কী হয়, timeout কীভাবে report হয় এবং connection বন্ধ করা হয় কি না, Samia সেগুলোও যাচাই করতে বলবে।

## সমাপ্তি: Lab প্রস্তুত, রহস্য অমীমাংসিত
তারা এখন নিজেদের machine-এ একটি TCP conversation পুনরায় তৈরি করতে পারে। incident-এর উৎস এখনো অজানা। ticket-এর text export-এ কিছু character অদ্ভুতভাবে render হওয়ার কথা আছে। পরের ধাপে readable text-এর ওপর নির্ভর না করে data-কে byte হিসেবে দেখতে হবে।

[Chapter 00-এর কারিগরি নির্দেশনা](README.md)