# Chapter 03 Background: কে শুনছে?

[টুল তৈরির নির্দেশনা ও TCP Port Scanner specification পড়ো](README.md)।

## অধ্যায়ের গল্প: একটি উত্তর, নাকি অনেক অজানা?

Network Diagnostic report-এ loopback endpoint-এর connection সফল। Rayhan বলে, “আমরা জানি service reachable। এবার দেখি host-এ আর কী চলছে।” Samia সম্মতি দেয়, তবে scope স্পষ্ট করে: নিজেদের controlled lab host এবং explicit port selection। একটি connection সফল হয়েছে বলে পুরো machine সম্পর্কে কিছু জানা যায় না।

তারা একটি port দিয়ে শুরু করবে। Successful dial, explicit refusal এবং timeout আলাদা state হবে। Timeout মানে closed নয়; network path-এ নীরবতার একাধিক কারণ থাকতে পারে। Rayhan একাধিক port পরীক্ষা করতে চাইলে Samia বলে selection validate না করে network activity শুরু করা যাবে না। Sequential scan-এর correctness প্রতিষ্ঠার পর bounded worker pool যোগ হবে। Unbounded concurrency file descriptor, memory এবং target capacity-তে চাপ ফেলতে পারে।

Scanner-কে timeout মানতে হবে, Ctrl-C-তে থামতে হবে এবং completed result রাখতে হবে। অসম্পূর্ণ scan-কে complete বলা যাবে না। শেষ output শুধু terminal-এর জন্য নয়, পরবর্তী tool-এর জন্য structured JSON/NDJSON-ও হবে। এই tool service-এর পরিচয় নিশ্চিত করবে না; এটি কেবল নির্দিষ্ট TCP port-এ controlled connection attempt-এর evidence দেবে।

### 03.1: একটি Port, একটি Observation
Rayhan একটি port পরীক্ষা করবে। Successful dial, refusal ও timeout-এর অর্থ আলাদা না করলে multiple port-এ যাওয়া যাবে না। Scanner service health নিয়ে অযাচিত দাবি করবে না।

### 03.2: Port Selection
Single port-এর পর range ও list আসবে। Malformed বা out-of-range selection network activity-এর আগেই reject হবে। Duplicate বাদ দিয়ে প্রথমে sequential execution থাকবে।

### 03.3: নীরবতার অর্থ
একটি probe সময়মতো উত্তর দেয়নি। Rayhan closed লিখতে চাইলে Samia মনে করায়, timeout অপেক্ষার সীমা, verdict নয়। Typed error semantics দিয়ে refusal ও অন্যান্য error আলাদা হবে।

### 03.4: সীমাবদ্ধ গতি
Rayhan worker pool প্রস্তাব করে। Samia জানতে চায় একসঙ্গে কত dial চলবে এবং ফলাফল execution order-এর ওপর নির্ভর করবে কি না। Bounded concurrency ও deterministic output জরুরি।

### 03.5: Scan থামানো
ভুল target selection বুঝতে পেরে Rayhan Ctrl-C চাপবে। নতুন কাজ বন্ধ, in-flight কাজ cancel, completed result অক্ষত এবং interrupted/unattempted count আলাদা থাকতে হবে।

### 03.6: Machine-readable Output
Samia ফলাফল পরের tool-এ দিতে চায়। JSON record-এর schema স্থিতিশীল হবে; timestamp ও duration স্বাভাবিকভাবেই বদলাবে। Diagnostic text stdout-এ মিশবে না।

## সমাপ্তি: Inventory মানে নিশ্চয়তা নয়
Scanner নির্বাচিত TCP port-এ probe চালাতে, uncertainty প্রকাশ করতে, concurrency নিয়ন্ত্রণ করতে এবং partial result রাখতে পারে। Open port service-এর পরিচয় নিশ্চিত করে না। পরবর্তী অধ্যায়ে open-port finding হবে service identification-এর candidate, চূড়ান্ত verdict নয়।

[Chapter 03-এর কারিগরি নির্দেশনা](README.md)