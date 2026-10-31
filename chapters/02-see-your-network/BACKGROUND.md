# Chapter 02 Background: Network-এর মানচিত্র

[টুল তৈরির নির্দেশনা ও Network Diagnostic specification পড়ো](README.md)।

## অধ্যায়ের গল্প: ঠিকানা জানা মানেই পৌঁছানো নয়

Byte Inspector-এর output-এ একটি readable fragment address-এর মতো দেখায়। Rayhan বলে, “ঠিকানাটা পাওয়া গেছে। এবার service-টা দেখি।” Samia fragment-টি আবার পড়ে। “তুমি জানো না এটি কোন interface-এর, prefix কী বোঝায়, কিংবা আমাদের lab-এর অংশ কি না। Address থাকলেই service reachable হয় না।”

তারা প্রথমে local network inventory তৈরি করবে। একটি machine-এ loopback, Ethernet, Wi-Fi ও virtual interface থাকতে পারে। Interface up থাকলেও কোনো নির্দিষ্ট TCP port-এ service listening করছে এমন নিশ্চয়তা নেই। IP address-এর সঙ্গে CIDR prefix থাকলে সেটি network range-ও নির্দেশ করে। এরপর কেবল নিজেদের loopback lab-এ TCP connection পরীক্ষা হবে।

Rayhan সব output এক report-এ চায়। Samia-র শর্ত, একটি independent observation ব্যর্থ হলে অন্যগুলো হারানো চলবে না। প্রতিটি section-এর status ও error আলাদা থাকবে। Report কোনো একক verdict নয়; কোন evidence পাওয়া গেছে, কোনটি পাওয়া যায়নি, তা সংরক্ষণের উপায়।

### 02.1: Interface চেনা
Rayhan fragment-এর address-টি machine-এর সঙ্গে মেলাতে চায়। Samia আগে interface inventory দেখতে বলে। কোন interface up, কোন address কোথায় bind করা, তা না জেনে destination নিয়ে সিদ্ধান্ত নয়।

### 02.2: Address ও Prefix
Address পাওয়া গেলেও prefix-এর অর্থ পরিষ্কার নয়। Tool-কে host address, network address ও prefix length আলাদা করতে হবে। IPv4/IPv6 এবং malformed input-ও সঠিকভাবে সামলাতে হবে।

### 02.3: TCP endpoint যাচাই
তারা Chapter 00-এর loopback server ব্যবহার করবে। Successful handshake connection স্থাপনের প্রমাণ, application health-এর নয়। Refusal ও timeout-ও আলাদা observation।

### 02.4: এক Report-এ Observation
তিনটি command-এর ফল একত্র হবে, কিন্তু একটি section ব্যর্থ হলে অন্য ফল থাকবে। Report-এর উদ্দেশ্য uncertainty মুছে ফেলা নয়।

## সমাপ্তি: মানচিত্রের পরের প্রশ্ন
তারা local interface, address/prefix এবং নির্দিষ্ট endpoint সম্পর্কে snapshot পায়। কিন্তু host-এ আর কোন TCP port listening করছে তা অজানা। পরের অধ্যায়ে explicit scope, timeout, bounded concurrency ও cancellation-সহ port scanner তৈরি হবে।

[Chapter 02-এর কারিগরি নির্দেশনা](README.md)