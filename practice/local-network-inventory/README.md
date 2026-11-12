# Practice: Who Is on My Local Network?

> **POV framing:** তুমি নিজের অনুমোদিত local network-এর দায়িত্বে থাকা engineer।  
> **ধরন:** Environment-based practice | **সময়:** 1–3 ঘণ্টা | **Difficulty:** Beginner → Intermediate

## ঘটনা

একটি ছোট office/home lab-এর network inventory হালনাগাদ করতে হবে। আগে থেকে sample file দেওয়া হচ্ছে না। নিজের computer-এর local network stack থেকে পাওয়া তথ্য সংগ্রহ করে এমন tool বানাও, যা সম্প্রতি দেখা device-গুলোর inventory তৈরি করবে।

এটি file-based investigation নয়। এখানে **নিজের environment থেকে evidence সংগ্রহ → parse → normalize → classify → report** করতে হবে।

## কী tool তৈরি করবে?

একটি **Local Network Inventory Tool**। প্রথম সংস্করণে active network scan করবে না। Operating system-এর local neighbor/ARP table থেকে পাওয়া তথ্য parse করবে।

### Step 1: নিজের environment বুঝে নাও

নিজের operating system অনুযায়ী read-only command চালাও:

- Linux: `ip neigh show` অথবা `arp -a`
- macOS: `arp -a`
- Windows: `arp -a`

Command-এর output local machine-এর neighbor cache/table দেখায়। এটি network-এর প্রতিটি connected device-এর পূর্ণ তালিকা নয়; যে device-এর সঙ্গে যোগাযোগ হয়েছে বা যার entry cache-এ আছে, মূলত সেগুলোই দেখা যেতে পারে।

Output text file হিসেবে save করতে পারো, অথবা tool-কে stdin থেকে input নিতে দিতে পারো।

## Minimum requirements

1. Linux `ip neigh` এবং অন্তত একটি `arp -a` output format parse করবে।
2. IP address, MAC address ও interface (যদি পাওয়া যায়) normalize করবে।
3. Neighbor state থাকলে সংরক্ষণ করবে; state না থাকলে অনুমান করবে না।
4. Duplicate entry শনাক্ত করবে।
5. Invalid line বাদ না দিয়ে parse warning হিসেবে report করবে।
6. Human-readable table এবং JSON export দেবে।
7. Output-এ data source ও collection time থাকবে।

## Investigation questions

- Local neighbor table-এ কতটি unique IP আছে?
- কতটি unique MAC address পাওয়া গেছে?
- কোন entry-র state `REACHABLE`, `STALE`, `DELAY` বা `FAILED`?
- একই MAC একাধিক IP-তে দেখা যাচ্ছে কি?
- কোনো entry incomplete বা malformed কি?
- কোন তথ্য থেকে device-এর manufacturer বা owner নির্ভরযোগ্যভাবে জানা যায় না?
- কেন neighbor table-কে “এখন network-এ connected সব device” বলা যাবে না?

## Acceptance criteria

- Offline sample text input দিয়েও tool test করা যাবে।
- Linux ও ARP output-এর parser আলাদা test fixture দিয়ে যাচাই হবে।
- IPv4/IPv6 input এলে crash করবে না; unsupported format হলে warning দেবে।
- Duplicate ও malformed entry report হবে।
- Tool কোনো packet পাঠাবে না, host probe করবে না এবং network configuration পরিবর্তন করবে না।
- Output-এ limitation স্পষ্ট থাকবে: neighbor cache পূর্ণ device inventory নয়।

## Optional extensions

- নিজের router-এর DHCP lease export import।
- User-provided vendor mapping দিয়ে MAC prefix annotate; vendor lookup-কে নিশ্চিত device identity বলবে না।
- Previous inventory snapshot-এর সঙ্গে তুলনা।
- Device label manually assign করা।

## Safety boundary

- কেবল নিজের machine ও নিজের/অনুমোদিত local network ব্যবহার করবে।
- এই practice-এ subnet sweep, port scan, packet capture বা third-party network discovery প্রয়োজন নেই।
- অন্যের Wi-Fi/LAN-এ অনুমতি ছাড়া probe করবে না।
- Default behavior passive local data parsing-এ সীমাবদ্ধ থাকবে।

## Character lens

একজন engineer network inventory তৈরি করার সময় শুধু device-এর সংখ্যা গোনে না। সে data কোথা থেকে এসেছে, কতটা complete, কোন state বোঝায় এবং কোন conclusion টানা যায় না, সেটাও জানে।
