# Chapter 01 Background: অক্ষরের আড়ালে Byte

[টুল তৈরির নির্দেশনা ও Byte Inspector specification পড়ো](README.md)।

## অধ্যায়ের গল্প: একই ফাইল, দুই রকম পাঠ

Requester একটি sanitized evidence bundle পাঠিয়েছে। কোনো credential বা বাস্তব user data নেই, কেবল ছোট text export এবং সেটি কীভাবে দেখা হয়েছিল তার নোট। Rayhan file খুলে কিছু অদ্ভুত character দেখে বলল, “Export-এর সময় data নষ্ট হয়েছে মনে হয়।”

Samia একই file নিজের editor-এ খুলল। তার screen-এ কিছু অংশ Rayhan-এর দেখা থেকে আলাদা। “দুইজন একই file খুলেছি, display এক নয়। তাহলে corruption বলছ কীভাবে?”

তারা বুঝল, editor byte-গুলোকে character হিসেবে ব্যাখ্যা করছে। সেই interpretation ভুল হতে পারে। আরেকটি editor দিয়ে খোলার বদলে তারা raw byte inspect করবে। প্রথমে প্রতিটি byte-এর numeric value ও position, পরে hexadecimal view, নির্দিষ্ট offset/length এবং text encoding-এর interpretation। ছোট deterministic fixture দিয়ে শুরু হবে, যাতে প্রত্যাশিত byte আগে থেকেই জানা।

এই tool কোনো payload-এর অর্থ অনুমান করবে না। কাজ হবে data না বদলে দেখা। Readable fragment clue হতে পারে, কিন্তু তার মানে এখনো জানা নেই।

### 01.1: Byte-কে character ভাববে না
Rayhan file-এর কয়েকটি byte হাতে গুনে দেখতে চায়। Samia পরিচিত input-সহ fixture প্রস্তাব করে। প্রথম ধাপে decoding নেই; কেবল position ও numeric value। এতে raw data আর interpretation আলাদা থাকবে।

### 01.2: Hexdump-এ pattern
Numeric value সঠিক হলেও দীর্ঘ sequence চোখে বোঝা কঠিন। Rayhan hexadecimal view চায়। Samia মনে করায়, hexdump presentation, data transformation নয়। Offset ও grouping এমন হতে হবে যাতে fixture হাতে যাচাই করা যায়।

### 01.3: নির্দিষ্ট অংশ পরীক্ষা
বড় file বারবার পুরো পড়া অকার্যকর। Rayhan নির্দিষ্ট range দেখতে চায়। Samia জিজ্ঞেস করে, offset শেষের বাইরে গেলে বা length শূন্য হলে কী হবে? Boundary-গুলো স্পষ্ট করতে হবে।

### 01.4: Byte থেকে Text interpretation
তারা text view যোগ করবে, কিন্তু UTF-8 ও ASCII সব byte একইভাবে ব্যাখ্যা করে না। Invalid sequence নীরবে বাদ দেওয়া যাবে না। Decoded text একটি interpretation; raw byte-ই evidence।

### 01.5: Pipeline-এ Inspector
Samia stdin দিয়ে data পাঠাতে চায়। File-only tool workflow-এ বিচ্ছিন্ন থাকবে। Input source বদলালেও output ও safety limit একই থাকতে হবে।

## সমাপ্তি: পাঠযোগ্যতা নয়, প্রমাণ
Inspector এখন byte-এর value ও position দেখাতে পারে। কিন্তু কোনো sequence-এর অর্থ শুধু উপস্থিতি থেকে জানা যায় না। একটি fragment address-এর মতো দেখালেও সেটি কোন host বা interface-এর, কিংবা reachable কি না, অজানা। পরের অধ্যায়ে নিজেদের network inventory ও controlled TCP test দরকার।

[Chapter 01-এর কারিগরি নির্দেশনা](README.md)