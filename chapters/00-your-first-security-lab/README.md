# অধ্যায় ০০: নিজের Security Lab তৈরি করো

> **পর্যায়:** ১, ভিত্তি তৈরি  
> **স্তর:** L1, Learning  
> **প্রধান deliverable:** Go দিয়ে লেখা একটি loopback-only TCP server এবং তার সঙ্গে যোগাযোগ করতে পারা একটি TCP client  
> **পূর্বশর্ত:** Terminal ও text editor-এর প্রাথমিক ব্যবহার  
> **পরবর্তী অধ্যায়:** [Chapter 01: Byte-এর ভেতরটা দেখো](../01-decode-the-bytes/README.md)

Rayhan নতুন একটি security investigation শুরু করতে যাচ্ছে। Samia তাকে থামিয়ে প্রথমে একটি প্রশ্ন করে: “যে environment-এ পরীক্ষা করবে, সেটি কি তোমার নিয়ন্ত্রণে? আর ফলাফল ভুল হলে তুমি কীভাবে বুঝবে?”

এই অধ্যায়ে আমরা কোনো vulnerability exploit করব না, public host scan করব না, এমনকি কোনো security tool-ও তৈরি করব না। তার বদলে এমন একটি ছোট, নিয়ন্ত্রিত workspace তৈরি করব যেখানে পরের অধ্যায়গুলোর experiment নিরাপদে চালানো যাবে। একই সঙ্গে শিখব, এই curriculum-এ কীভাবে একটি specification পড়ে নিজের implementation তৈরি ও যাচাই করতে হয়।

## এই অধ্যায়ে কী শিখবে

অধ্যায় শেষে তুমি পারবে:

1. Rayhan ও Samia-র Red Team এবং Blue Team perspective ব্যাখ্যা করতে।
2. Authorization, controlled lab এবং নিরাপদ testing-এর সীমা বুঝতে।
3. একটি challenge specification থেকে objective, input, output, constraints ও acceptance criteria খুঁজে বের করতে।
4. Go toolchain install করে version যাচাই করতে।
5. Go program compile ও run করতে।
6. শুধু loopback interface-এ TCP server চালাতে।
7. Server-এর সঙ্গে যোগাযোগ করে response পড়তে পারে এমন TCP client লিখতে।

## Lab-এর নিরাপত্তা-সীমা

এই curriculum-এ **lab** বলতে এমন environment বোঝায় যার target, network path এবং test data তোমার নিয়ন্ত্রণে, অথবা যেটি ব্যবহারের স্পষ্ট অনুমতি তোমার আছে।

- এই অধ্যায়ের সব network exercise কেবল 127.0.0.1 loopback address-এ চলবে।
- localhost ব্যবহার করলে সেটি IPv4 বা IPv6-এ resolve হতে পারে। এই অধ্যায়ের contract-এ নির্দিষ্টভাবে 127.0.0.1 ব্যবহার করবে।
- নিজের কম্পিউটারে চলা server-ও ভুলভাবে 0.0.0.0 বা public interface-এ bind করলে অন্য host থেকে reachable হতে পারে। তা করবে না।
- Public IP, অন্যের Wi-Fi/LAN device, office network বা internet service-এ পরীক্ষা করবে না।
- কোনো target-এর মালিকানা বা লিখিত authorization নিশ্চিত না হলে সেটিকে test target হিসেবে ধরবে না।

### Red Team ও Blue Team-এর দৃষ্টিভঙ্গি

**Rayhan (Red Team)** অনুমোদিত scope-এর মধ্যে system-এর আচরণ পরীক্ষা করে এবং প্রমাণ সংগ্রহ করে।  
**Samia (Blue Team)** সেই আচরণ পর্যবেক্ষণ করে, ঝুঁকি বোঝে, নিরাপদ configuration নিশ্চিত করে এবং evidence যাচাই করে।

দুই perspective-ই প্রয়োজন। অনুমতি ছাড়া পরীক্ষা করা Red Team কাজ নয়; আর evidence ছাড়া কোনো finding-কে সত্য ধরে নেওয়া Blue Team কাজ নয়।

## এই curriculum কীভাবে চলবে

প্রতিটি chapter একই শেখার চক্র অনুসরণ করে:

~~~mermaid
flowchart LR
    A["সমস্যা ও গল্প"] --> B["দৃশ্যমান করে বোঝা"]
    B --> C["প্রয়োজনীয় ধারণা শেখা"]
    C --> D["নিজে তৈরি করা"]
    D --> E["পরীক্ষা ও যাচাই"]
    E --> F["ফলাফল বিশ্লেষণ"]
    F --> G["পরের ধাপে ব্যবহার"]
~~~

তুমি implementation নিজে লিখবে। Chapter-এ থাকবে প্রয়োজনীয় ধারণা, diagram, সুনির্দিষ্ট behavior contract এবং acceptance criteria। নিয়মিত chapter body-তে পূর্ণ implementation বা এমন starter code থাকবে না, যা challenge আগেই সমাধান করে দেয়।

### Specification পড়ার পাঁচটি সূত্র

| বিষয় | যে প্রশ্নের উত্তর খুঁজবে |
|---|---|
| Objective | কাজ শেষে কোন capability থাকতে হবে? |
| Inputs | Program কী data বা argument গ্রহণ করবে? |
| Outputs | কী ফলাফল কোথায় দেখাবে? |
| Constraints | কোন সীমা বা নিয়ম মানতে হবে? |
| Acceptance criteria | কীভাবে প্রমাণ করবে কাজটি সম্পন্ন? |

এর সঙ্গে **edge case** (সাধারণ input-এর বাইরের গুরুত্বপূর্ণ পরিস্থিতি), **error behavior** (ব্যর্থ হলে কী হবে) এবং **security consideration** (কোন নিরাপত্তা-শর্ত বজায় রাখতে হবে) খুঁজবে।

---

# 00.1: Lab-এর নিয়ম জানো, Specification পড়তে শেখো

Rayhan একটি challenge description পেল। সে সরাসরি editor খুলতে যাচ্ছিল। Samia বলল, “আগে বুঝে নাও, তোমাকে কী বানাতে বলা হয়েছে। ভুল problem solve করলে সুন্দর code-ও ভুল ফল।”

### কী তৈরি করবে

কোনো program নয়। একটি sample challenge specification পড়ে তার অংশগুলো চিহ্নিত করবে।

### প্রয়োজনীয় ধারণা

**Authorization** মানে কোনো system পরীক্ষা করার স্পষ্ট অনুমতি। কোনো service internet-এ reachable হলেই সেটি পরীক্ষা করার অনুমতি পাওয়া যায় না।

**Controlled lab** হলো এমন test environment যেখানে target ও test activity নির্দিষ্ট এবং নিয়ন্ত্রিত। Loopback address 127.0.0.1 একই machine-কে নির্দেশ করে; এই অধ্যায়ে server ও client একই machine-এ থাকবে।

### Sample challenge specification

নিচের sample-টি পড়ো। প্রতিটি paragraph বা bullet কোন specification element-এর উদাহরণ, তা নিজে চিহ্নিত করো।

> **Problem:** নিজের machine-এ একটি TCP service চালু আছে কি না, তা যাচাই করার জন্য একটি ছোট client তৈরি করো।  
>
> **Objective:** Client নির্দিষ্ট local port-এ connect করে server-এর greeting পড়বে।  
>
> **Input:** Command line থেকে একটি TCP port; target address হবে 127.0.0.1।  
>
> **Output:** Server-এর পাঠানো greeting এবং client-এর measured elapsed time terminal-এ দেখাবে।  
>
> **Behavior:** Connection সফল হলে server-এর পাঠানো data সম্পূর্ণ পড়ে EOF পর্যন্ত অপেক্ষা করবে।  
>
> **Constraints:** কেবল 127.0.0.1-এ connect করবে। Port hard-code করা যাবে না।  
>
> **Edge cases:** Invalid port, server বন্ধ থাকা, connection refused, server-এর empty response।  
>
> **Error behavior:** Invalid input হলে connection attempt করবে না এবং error stderr-এ দেখাবে। Server বন্ধ থাকলে connection error দেখাবে।  
>
> **Security:** Public বা অন্য host-এ connect করার option থাকবে না।  
>
> **Acceptance criteria:** Valid local server চালু থাকলে client greeting ও duration দেখাবে; server বন্ধ থাকলে পরিষ্কার error দেখাবে।  
>
> **Verification:** একই machine-এ server ও client চালিয়ে success এবং server বন্ধ রেখে failure, দুই অবস্থাই পরীক্ষা করো।

### Challenge

উপরের sample থেকে আলাদা করে লিখে ফেলো:

1. Problem ও objective।
2. Input এবং output।
3. Behavioral constraint ও security constraint।
4. Edge case ও error behavior।
5. Acceptance criteria ও verification পদ্ধতি।

তারপর প্রতিটি item-এর পাশে sample-এর সংশ্লিষ্ট বাক্য বা bullet উল্লেখ করো।

### Acceptance criteria

- পাঁচটি মূল element (objective, inputs, outputs, constraints, acceptance criteria) সঠিকভাবে চিহ্নিত করতে পারবে।
- Edge case, error behavior এবং security consideration-কে এক জিনিস হিসেবে গুলিয়ে ফেলবে না।
- কোন target-এ পরীক্ষা করার অনুমতি আছে, তা specification থেকে বলতে পারবে।

### যাচাই

নিজের তালিকা sample-এর সঙ্গে মিলিয়ে দেখো। কোনো requirement যদি sample-এ না থাকে, সেটি নিজের অনুমান থেকে যোগ করবে না।

**সম্পন্ন হওয়ার শর্ত:** Code লেখা শুরু করার আগে একটি specification থেকে কী বানাতে হবে এবং কোন সীমা মানতে হবে, তা নিজের ভাষায় ব্যাখ্যা করতে পারবে।

### Debrief

Samia-র নিয়মটি মনে রাখো: **প্রথমে scope, তারপর implementation, শেষে evidence।** পরের প্রতিটি chapter-এ এই অভ্যাস কাজে লাগবে।

---

# 00.2: Go চালু করো, প্রথম Program লেখো

Lab-এর নিয়ম বোঝা হয়েছে। এবার Rayhan ও Samia এমন একটি toolchain চায়, যা দিয়ে পরের chapter-গুলোতে program তৈরি ও পরীক্ষা করা যাবে।

### কী তৈরি করবে

Go-এর standard library ব্যবহার করে একটি ছোট command-line program, যা greeting-এর সঙ্গে বর্তমান সময় দেখাবে।

### Go toolchain

**Toolchain** হলো program তৈরি ও চালানোর জন্য প্রয়োজনীয় compiler, command এবং supporting tools-এর সমষ্টি।

Go-এর official installation নির্দেশনা অনুসরণ করে তোমার operating system-এর উপযোগী Go install করো: [Install Go](https://go.dev/doc/install)।

Terminal নতুন করে খুলে যাচাই করো:

~~~sh
go version
~~~

Command-টি Go version দেখালে installation যাচাই হয়েছে। Command পাওয়া না গেলে PATH বা installation নির্দেশনা আবার পরীক্ষা করো।

### প্রয়োজনীয় ধারণা

- go run source file compile করে program চালায়।
- go build executable তৈরি করে, যা পরে আলাদাভাবে চালানো যায়।
- fmt.Println terminal-এ text output দেয়।
- time.Now() বর্তমান সময়ের একটি value দেয়।
- time.RFC3339 timestamp-এর একটি standard textual format।

এই milestone-এ শুধু Go standard library ব্যবহার করবে। আলাদা third-party package প্রয়োজন নেই।

### Challenge specification

**Problem:** Go environment ঠিকমতো কাজ করছে কি না, তা যাচাই করার জন্য প্রথম program লেখো।

**Objective:** Program একটি greeting এবং program চালানোর সময়ের timestamp দেখাবে।

**Input:** কোনো command-line input প্রয়োজন নেই।

**Output:** এক লাইনে greeting এবং RFC3339 format-এ timestamp। উদাহরণস্বরূপ:

~~~text
Hello from my security lab | time=2026-10-31T08:30:00+06:00
~~~

উপরের timestamp কেবল format-এর উদাহরণ; তোমার program-এ বাস্তব current time দেখাতে হবে।

**Behavioral contract**
- Program চালালে একবার output দেবে এবং স্বাভাবিকভাবে শেষ হবে।
- Timestamp program execution-এর সময় নিতে হবে; source code-এ fixed value রাখা যাবে না।
- Timestamp RFC3339 format-এ হবে।
- Output stdout-এ যাবে।

**Constraints**
- Go standard library ছাড়া dependency নয়।
- Program compile ও run হতে হবে।
- এই milestone-এর জন্য Go module বা repository-wide project structure তৈরি করার প্রয়োজন নেই। একটি standalone source file যথেষ্ট।

**Edge cases:** System clock ভুল বা অস্বাভাবিক হলেও program-এর দায়িত্ব শুধু system-provided time দেখানো; নিজে সময় সংশোধন করার চেষ্টা করবে না।

**Error behavior:** Source compile না হলে compiler-এর error দেখবে এবং সেই error ঠিক করবে। Program-এর runtime error হলে সেটি আড়াল করবে না।

### Acceptance criteria

- go version সফলভাবে চলে।
- Program go run দিয়ে চলে এবং timestamp-সহ greeting দেখায়।
- go build দিয়ে executable তৈরি হয়।
- তৈরি executable চালালেও একই output contract বজায় থাকে।

### Verification

1. Source file লেখো।
2. go run দিয়ে চালাও।
3. go build দিয়ে executable তৈরি করো।
4. Executable-টি আলাদাভাবে চালাও।
5. দুইবার চালিয়ে timestamp পরিবর্তিত হচ্ছে কি না দেখো।

**সম্পন্ন হওয়ার শর্ত:** নিজের লেখা Go program source থেকে এবং compiled executable থেকে চালাতে পারবে।

### Debrief

এখন তোমার machine শুধু Go install করা অবস্থায় নেই; তুমি source code থেকে executable তৈরি করতে পারছ। Chapter 01 থেকে এই মৌলিক workflow-এর ওপর ভিত্তি করেই tool তৈরি হবে।

---

# 00.3: TCP Server চালাও, Local Connection গ্রহণ করো

Rayhan এবার একটি local service তৈরি করতে চায়। Samia-র শর্ত: service-টি যেন কেবল নিজের machine থেকেই reachable হয়।

### কী তৈরি করবে

একটি TCP server, যা loopback address-এ listen করবে, client connection গ্রহণ করবে এবং প্রতিটি client-কে একটি fixed greeting পাঠাবে।

### প্রয়োজনীয় ধারণা

**TCP (Transmission Control Protocol)** হলো connection-oriented transport protocol। Client ও server-এর মধ্যে connection স্থাপনের পর দুই দিকেই byte stream আদান-প্রদান করা যায়।

**Listener** হলো এমন endpoint, যা incoming connection-এর অপেক্ষা করে। Go-তে net.Listen দিয়ে TCP listener তৈরি করা যায় এবং Accept দিয়ে connection গ্রহণ করা যায়। একটি accepted connection হলো net.Conn।

এই milestone-এ এক সময়ে একটি connection process করবে। একাধিক connection সামলাতে goroutine বা concurrent worker লাগবে না; sequential loop-ই যথেষ্ট।

### Connection-এর প্রবাহ

~~~mermaid
sequenceDiagram
    participant C as Client
    participant S as Loopback TCP Server
    C->>S: TCP connection request
    S-->>C: Connection accepted
    S->>C: Greeting line
    S-->>C: Connection close
    Note over S: পরের client-এর অপেক্ষা
~~~

Server greeting পাঠিয়ে connection বন্ধ করবে। এরপর listener চালু থাকবে এবং পরের client-এর অপেক্ষা করবে।

### Challenge specification

**Problem:** নিজের machine-এ একটি TCP service তৈরি করো, যা একাধিক client-কে একের পর এক greeting দিতে পারে।

**Objective:** Server একটি TCP connection গ্রহণ করবে, client-কে fixed greeting পাঠাবে, connection বন্ধ করবে এবং পরবর্তী connection গ্রহণ করতে থাকবে।

**Input**
- Command line থেকে একটি port।
- Port-এর valid range 1–65535।

**Output**
- Server startup-এ কোন local address-এ listen করছে তা দেখাবে।
- প্রতিটি accepted connection-এর remote address log করবে।
- Client-কে একটি newline-terminated greeting পাঠাবে।

**Behavioral contract**
- Listener অবশ্যই 127.0.0.1:<port>-এ bind করবে।
- Port argument ছাড়া server চালানো যাবে না।
- একটি connection গ্রহণের পর greeting লিখে connection cleanly close করবে।
- Connection close করার পর server পরের connection-এর জন্য অপেক্ষা করবে।
- Server process চলমান থাকা পর্যন্ত listener চালু থাকবে।
- Server বন্ধ করতে Ctrl-C ব্যবহার করা যাবে।

**Constraints**
- 0.0.0.0, public interface, LAN address বা wildcard bind করা যাবে না।
- এই milestone-এ connection sequential হবে; এক সময়ে একটি connection process করবে।
- Greeting-এর content স্থির থাকবে এবং প্রতিটি client একই greeting পাবে।
- Connection handle শেষ হলে সেটি close করতে হবে।

**Edge cases:** Invalid port, port ইতিমধ্যে ব্যবহৃত, client মাঝপথে disconnect, write failure, server startup failure, একাধিক sequential client।

**Error behavior**
- Missing বা invalid port হলে stderr-এ error এবং non-zero exit; listener তৈরি করবে না।
- Port ব্যবহৃত থাকলে bind failure দেখাবে এবং server চালু হয়েছে এমন দাবি করবে না।
- কোনো client connection-এ write failure হলে error log করবে, connection close করবে এবং server পরবর্তী connection গ্রহণের চেষ্টা চালিয়ে যাবে।
- Listener-এর unrecoverable accept failure হলে error দেখিয়ে server বন্ধ হবে।

**Security considerations**
- Bind address 127.0.0.1 হতে হবে, 0.0.0.0 নয়।
- এই chapter-এ server-কে অন্য machine থেকে access করার চেষ্টা করবে না।
- প্রতিটি connection বন্ধ করতে হবে; resource leak রাখা যাবে না।

### Acceptance criteria

- Server কেবল 127.0.0.1-এ listen করে।
- প্রথম client greeting পায়।
- Server restart না করেই দ্বিতীয় client-কে greeting দিতে পারে।
- প্রতিটি connection-এর remote address server log-এ দেখা যায়।
- প্রতিটি client connection শেষে close হয়।
- Invalid port ও port conflict স্পষ্টভাবে handle হয়।

### Verification

1. Server চালু করো।
2. আলাদা terminal থেকে nc 127.0.0.1 <port> চালিয়ে greeting দেখো। nc না থাকলে অন্য local TCP client ব্যবহার করতে পারো।
3. একই কাজ দ্বিতীয়বার করো, server restart না করে।
4. Server log-এ দুইটি connection-এর remote address দেখো।
5. একই port-এ দ্বিতীয় server চালিয়ে bind failure যাচাই করো।
6. Server বন্ধ করে দাও।

সব network verification loopback-এ করবে।

**সম্পন্ন হওয়ার শর্ত:** Server একটি local client-কে greeting দিয়ে connection বন্ধ করার পরও পরবর্তী local client গ্রহণ করতে পারে।

### Red/Blue debrief

Rayhan এখন local service তৈরি করতে পারে। Samia নিশ্চিত করেছে service-টি public interface-এ expose হয়নি। একই TCP server pattern পরের chapter-গুলোতে controlled test fixture হিসেবে কাজে লাগবে।

---

# 00.4: TCP Client দিয়ে Server-এর উত্তর যাচাই করো

Server তৈরি হয়েছে। কিন্তু server চালু আছে দেখলেই client থেকে যোগাযোগ সফল হয়েছে প্রমাণ হয় না। Rayhan এবার এমন একটি client লিখবে, যা নিজে connect করে server-এর response পড়বে। Samia চায় client-এর target যেন loopback-এর বাইরে যেতে না পারে।

### কী তৈরি করবে

একটি TCP client, যা 127.0.0.1-এর নির্দিষ্ট port-এ connect করবে, server-এর পাঠানো data EOF পর্যন্ত পড়বে এবং elapsed time দেখাবে।

### প্রয়োজনীয় ধারণা

**TCP client** হলো connection শুরু করা program। Go-তে net.Dial TCP connection তৈরি করতে পারে। Connection থেকে data পড়ার সময় Read এবং server-এর দিক থেকে stream শেষ হলে **EOF (End of File)** পাওয়া যায়।

TCP একটি byte stream। একটি Read call-এ server-এর সম্পূর্ণ message একবারে আসবে, এমন নিশ্চয়তা নেই। তাই client-কে stream শেষ হওয়া পর্যন্ত পড়তে হবে।

**Elapsed time** হলো operation শুরু থেকে শেষ পর্যন্ত কেটে যাওয়া সময়। এখানে connection শুরু করার ঠিক আগে timer শুরু হবে এবং server-এর response পড়া শেষ হলে duration গণনা হবে।

### Client-server exchange

~~~mermaid
sequenceDiagram
    participant C as Local TCP Client
    participant S as Loopback Server
    C->>S: Connect to 127.0.0.1:port
    S-->>C: Connection accepted
    S->>C: Greeting bytes
    S-->>C: Close connection
    C->>C: Read until EOF
    C-->>C: Print greeting and elapsed time
~~~

### Challenge specification

**Problem:** Local TCP server-এর response যাচাই করার জন্য একটি client তৈরি করো।

**Objective:** Client command line থেকে port নেবে, কেবল 127.0.0.1-এ connect করবে, server-এর পাঠানো সম্পূর্ণ greeting পড়বে এবং elapsed time দেখাবে।

**Input**
- Command line থেকে একটি port।
- Port-এর valid range 1–65535।
- Target address স্থিরভাবে 127.0.0.1; target host argument গ্রহণ করবে না।

**Output**
- Server থেকে পাওয়া সম্পূর্ণ greeting।
- Connection শুরু থেকে EOF পর্যন্ত elapsed time, milliseconds-এ।

**Behavioral contract**
- Port hard-code করা যাবে না; command line থেকে নিতে হবে।
- Connect target সবসময় 127.0.0.1:<port>।
- Connection establish করতে সর্বোচ্চ 3 seconds অপেক্ষা করবে।
- Connection সফল হলে response পড়ার জন্য আলাদা 3-second read deadline থাকবে; deadline-এর আগে EOF না এলে timeout error দেখাবে।
- Connection সফল হলে server stream-এর সব data EOF পর্যন্ত পড়বে।
- একবার Read করেই সম্পূর্ণ message পাওয়া গেছে ধরে নেওয়া যাবে না।
- EOF স্বাভাবিক completion; EOF-কে error হিসেবে দেখাবে না।
- Response পড়া শেষ হলে client connection close করবে।
- Elapsed time connection attempt শুরুর আগে থেকে EOF পর্যন্ত মাপবে।

**Constraints**
- Client-এ remote host বা arbitrary IP দেওয়ার option থাকবে না।
- কোনো external network access নয়।
- Server ও client একই machine-এ চলবে।
- এই milestone-এ fixed greeting server-ই response-এর একমাত্র উৎস।

**Edge cases:** Missing/invalid port, server বন্ধ, connection refused, connect timeout, server response না দিয়ে connection খোলা রাখা, empty response, response একাধিক read-এ আসা, unexpected read error।

**Error behavior**
- Invalid port হলে connection attempt-এর আগে error এবং non-zero exit।
- Server বন্ধ থাকলে connection error stderr-এ দেখাবে।
- Connection বা response deadline শেষ হলে timeout error দেখাবে এবং non-zero exit করবে; client অনির্দিষ্টকাল অপেক্ষা করবে না.
- Connection সফল হলেও EOF-এর আগে কোনো byte না এলে server-এর greeting contract ভঙ্গ হয়েছে বলে stderr-এ error দেখাবে এবং non-zero exit করবে।
- EOF-এর আগে unexpected read error হলে error দেখাবে এবং success output হিসেবে অসম্পূর্ণ response উপস্থাপন করবে না।
- EOF-এ পৌঁছানোর আগে কোনো data না পেলে empty greeting-কে protocol failure হিসেবে দেখাবে।
- Connection close করতে ব্যর্থ হলে error report করবে।

**Security considerations**
- Client-এর destination অবশ্যই 127.0.0.1; hostname বা user-supplied IP দিয়ে scope বাড়ানো যাবে না।
- Server-এর port user input হলেও valid range যাচাই করতে হবে।

### Acceptance criteria

- Client command line থেকে port নেয়।
- Client কেবল 127.0.0.1-এ connect করে।
- Server-এর সম্পূর্ণ greeting পড়ে।
- Greeting ও elapsed time দেখায়।
- Server বন্ধ থাকলে স্পষ্ট connection error দেখায়।
- Invalid port-এ কোনো connection attempt হয় না।

### Verification

1. Chapter 00.3-এর server চালু করো।
2. Client-কে server-এর port দিয়ে চালাও।
3. Server-এর greeting এবং elapsed time মিলিয়ে দেখো।
4. Server বন্ধ করো এবং client আবার চালাও।
5. এমন একটি controlled local test server দিয়ে যাচাই করো, যা connection গ্রহণ করে কিন্তু response/EOF দেয় না; client read deadline-এ থামতে হবে।
6. Invalid port দিয়ে চালিয়ে input validation যাচাই করো।
7. চাইলে server-এর response একাধিক write-এ পাঠিয়ে client সব data পড়ছে কি না যাচাই করতে পারো; তবে server-এর observable greeting contract অপরিবর্তিত থাকবে।

**সম্পন্ন হওয়ার শর্ত:** Client কেবল loopback-এ connect করে server-এর সম্পূর্ণ response পড়ে এবং সফল ও ব্যর্থ দুই অবস্থাই সঠিকভাবে প্রকাশ করে।

### Red/Blue debrief

Rayhan একটি local service-এর সঙ্গে যোগাযোগ করে observable evidence পেয়েছে। Samia নিশ্চিত করেছে client-এর destination সীমাবদ্ধ এবং failure-কে success হিসেবে দেখানো হয়নি। পরবর্তী chapter-এ এই একই discipline byte-level data inspection-এ কাজে লাগবে।

---

## অধ্যায় সম্পন্ন করার Checklist

- [ ] Lab, authorization এবং allowed target-এর পার্থক্য ব্যাখ্যা করতে পারি।
- [ ] Sample challenge specification-এর objective, inputs, outputs, constraints ও acceptance criteria চিহ্নিত করতে পারি।
- [ ] Go install করে go version যাচাই করেছি।
- [ ] নিজের লেখা Go program go run ও go build দিয়ে চালিয়েছি।
- [ ] 127.0.0.1-এ TCP server চালিয়ে একাধিক sequential connection গ্রহণ করেছি।
- [ ] TCP client দিয়ে greeting পড়েছি এবং elapsed time দেখিয়েছি।
- [ ] Server ও client-এর failure behavior যাচাই করেছি।
- [ ] কোনো exercise public বা unauthorized target-এ চালাইনি।

## পরবর্তী অধ্যায়

[Chapter 01: Byte-এর ভেতরটা দেখো](../01-decode-the-bytes/README.md)-তে আমরা network ও file data-র সবচেয়ে ছোট building block, byte, সরাসরি inspect করতে শুরু করব।
