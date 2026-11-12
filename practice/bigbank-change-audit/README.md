# Practice: BigBank — Who Changed the Adjustment Rules?

> **POV:** Adrian ও BigBank-এর incident investigation team  
> **ধরন:** File-based investigation | **সময়:** 2–4 ঘণ্টা | **Difficulty:** Intermediate

## গল্পের প্রেক্ষাপট

Volume 1-এর Chapter 6-এ investigation team জানতে পারে, Micro-Adjustment Service-এর configuration ও service authority-তে পরিবর্তন ঘটেছিল। শুধু transaction journal দেখলে কে কখন কোন control বদলেছে, তা বোঝা যায় না। Incident team-কে audit trail, approval record এবং configuration history একসঙ্গে পরীক্ষা করতে হয়।

তোমার কাজ attacker-কে identify করা নয়। তোমার কাজ হলো **কোন change ঘটেছে, কে করেছে, সেটি অনুমোদিত ছিল কি না এবং evidence কী সমর্থন করে** তা নির্ভরযোগ্যভাবে report করা।

## Sample data

- [configuration_audit.csv](./data/configuration_audit.csv): synthetic configuration-change audit events।
- সব actor, service identity, approval reference ও resource fabricated।
- Timestamp UTC-তে।
- approval_ref ফাঁকা থাকলে সেটিকে স্বয়ংক্রিয়ভাবে malicious বলবে না; policy ও event context-এর সঙ্গে মিলিয়ে review flag করবে।

## কী tool তৈরি করবে?

একটি **Configuration Change & Authorization Auditor** তৈরি করো, যা audit event parse করে change timeline ও review findings তৈরি করবে।

### Minimum requirements

1. CSV parse করে malformed row ও duplicate event_id শনাক্ত করবে।
2. timestamp_utc অনুযায়ী change timeline তৈরি করবে।
3. Actor, service identity, resource এবং action অনুযায়ী event group করবে।
4. previous_value ও new_value তুলনা করে কী বদলেছে তা report করবে।
5. approval_ref অনুপস্থিত বা একই actor দ্বারা change ও approval সম্পন্ন হওয়ার মতো policy concern flag করবে।
6. Privileged service identity বা sensitive resource change আলাদা করে দেখাবে।
7. Findings-এ source event ID রাখবে, যাতে প্রতিটি conclusion audit row-এ trace করা যায়।

### Investigation questions

- Bulk adjustment scope বা beneficiary configuration কখন বদলেছে?
- কোন actor বা service identity change করেছে?
- কোন change-এর approval reference নেই?
- একই identity change এবং approval দুটোই করেছে কি?
- কোন event-গুলো নিশ্চিত observation, আর কোনগুলো policy review-এর জন্য flag?
- শুধু audit event থাকলেই কি change-এর business legitimacy প্রমাণ হয়?

### Acceptance criteria

- একই input দিলে deterministic report তৈরি হবে।
- কোনো malformed row নীরবে বাদ যাবে না।
- Event order timestamp দিয়ে নির্ধারিত হবে; CSV row order দিয়ে নয়।
- প্রতিটি finding সংশ্লিষ্ট event_id উল্লেখ করবে।
- Missing approval-কে সরাসরি অপরাধের প্রমাণ বলা যাবে না।
- Tool কোনো live system বা credential access করবে না।

## Optional extensions

- JSON report export।
- Configurable sensitive-resource ও privileged-action policy।
- একই resource-এর before/after state timeline।
- Unit test-এ duplicate event, missing approval ও out-of-order timestamp যোগ করা।

## সীমাবদ্ধতা

Audit log অসম্পূর্ণ, tampered বা ভুলভাবে configured হতে পারে। এই sample দিয়ে কোনো real-world identity বা intent প্রমাণ করা সম্ভব নয়। Correlation ও policy flags তদন্তের lead, verdict নয়।

## Character lens

Adrian-এর দায়িত্ব শুধু suspicious transaction থামানো নয়; কোন control failure সেটিকে সম্ভব করেছে তা evidence দিয়ে বোঝা। ভালো auditor event-এর সারাংশ দেয়, কিন্তু প্রতিটি finding-কে source record পর্যন্ত traceable রাখে।
