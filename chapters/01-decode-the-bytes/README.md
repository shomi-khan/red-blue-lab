# অধ্যায় ০১: Byte-এর ভেতরটা দেখো, একটি Byte Inspector তৈরি

> **পর্যায়:** ১, ভিত্তি বোঝা  
> **স্তর:** L2, নির্ভরযোগ্য learning tool  
> **প্রধান deliverable:** `byteinspect`, raw file ও stdin-এর byte পরীক্ষা করার CLI tool  
> **পূর্বশর্ত:** [Chapter 00: Your First Security Lab](../00-your-first-security-lab/README.md)

Rayhan স্থানীয় lab থেকে একটি সন্দেহজনক attachment পেয়েছে। ফাইলটির extension `.txt`, কিন্তু text editor-এ খুললে অদ্ভুত চিহ্ন দেখা যায়। Editor আসলে byte-গুলোকে text হিসেবে ব্যাখ্যা করছে। সেই ব্যাখ্যা কাজে লাগতে পারে, কিন্তু সেটি ফাইলের প্রকৃত byte sequence নয়।

Samia চায়, কোনো interpretation-এর কারণে যেন মূল evidence হারিয়ে না যায়। তাই প্রথম প্রশ্নটি খুব সাধারণ: **ফাইলটিতে আসলে কোন byte-গুলো আছে?**

এই অধ্যায়ে ধাপে ধাপে এমন একটি inspector তৈরি করবে, যা raw byte দেখাবে, সেগুলোকে বিভিন্ন representation-এ উপস্থাপন করবে, নির্দিষ্ট range নির্বাচন করবে, ASCII ও UTF-8 ব্যাখ্যা করবে এবং শেষে file অথবা stdin থেকে input নেবে।

## কী তৈরি করবে

শেষে `byteinspect` পারবে:

- File অথবা stdin থেকে raw byte পড়তে।
- Byte-কে decimal, binary, hexadecimal ও hexdump আকারে দেখাতে।
- Zero-based offset ও length দিয়ে নির্দিষ্ট byte range বেছে নিতে।
- ASCII ও UTF-8 interpretation দেখাতে, invalid byte গোপন না করে।
- Empty input, malformed argument, oversized input এবং I/O error নির্দিষ্ট নিয়মে সামলাতে।

এটি inspector, arbitrary file-format decoder নয়। Input execute, modify, repair বা upload করবে না।

## শেখার ফল

অধ্যায় শেষে তুমি পারবে:

1. Binary, decimal ও hexadecimal representation-এর মধ্যে রূপান্তর করতে।
2. Go-তে `[]byte` কীভাবে ordered byte sequence ধরে তা ব্যাখ্যা করতে।
3. Raw byte ও text interpretation-এর পার্থক্য বুঝতে।
4. Encoding বদলালে একই byte sequence-এর অর্থ কেন বদলায় তা ব্যাখ্যা করতে।
5. Zero-based offset দিয়ে নির্দিষ্ট byte range পড়তে।
6. Valid ও invalid UTF-8 শনাক্ত করতে।
7. File ও stdin-কে একই input interface হিসেবে ব্যবহার করতে।
8. Embedded byte sequence ও temporary file দিয়ে deterministic test লিখতে।

## Byte-এর মানসিক মডেল

একটি bit-এর মান 0 অথবা 1। আটটি bit মিলে একটি byte। তাই একটি byte-এর সম্ভাব্য মান ০ থেকে ২৫৫ পর্যন্ত, মোট ২৫৬টি।

Byte নিজে কোনো অক্ষর নয়। এটি একটি সংখ্যা। কোন নিয়মে সেটিকে ব্যাখ্যা করা হচ্ছে, তার ওপর অর্থ নির্ভর করে।

| Representation | মান |
|---|---|
| Binary | `01000001` |
| Decimal | `65` |
| Hexadecimal | `0x41` |
| ASCII interpretation | `A` |

এগুলো একই আটটি bit-এর চারটি রূপ। ASCII-তে 65-এর জন্য `A` নির্ধারিত বলেই শেষের interpretation-টি অর্থবহ।

একটি file হলো byte-এর ordered sequence। যেমন `41 42 00 7F`:

```text
Index:       0       1       2       3
Byte:      0x41    0x42    0x00    0x7F
Decimal:     65      66       0     127
Binary:   01000001 01000010 00000000 01111111
```

Index শূন্য থেকে শুরু হয়। Index 2 হলো তৃতীয় byte। File header বা protocol field পরীক্ষা করার সময় এই পার্থক্য অত্যন্ত গুরুত্বপূর্ণ।

Hexadecimal সুবিধাজনক, কারণ একটি hex digit চারটি bit প্রকাশ করে। দুটি hex digit মিলে একটি byte। তাই `01000001`-এর বদলে `41` দেখে দীর্ঘ dump পড়া সহজ হয়।

**Raw byte, interpretation ও display এক জিনিস নয়:**

- Raw value: input-এ যে byte সত্যিই আছে।
- Interpretation: নির্বাচিত encoding অনুযায়ী byte বা sequence-এর অর্থ।
- Display: মানুষকে দেখানোর জন্য tool যেভাবে সেটি উপস্থাপন করে।

একটি নির্ভরযোগ্য inspector interpretation ব্যর্থ হলেও raw value সংরক্ষণ করে।

---

# 01.1: Byte পড়ো ও দেখাও, এগুলো সংখ্যামাত্র

Rayhan প্রথমে অনুমান নয়, inventory চায়। Samia এমন output চায় যা হাতে হিসাব করে যাচাই করা যায়।

### কী তৈরি করবে

একটি file পড়ে প্রতিটি byte-এর zero-based index, decimal value এবং আট digit-এর binary representation দেখাবে।

### প্রয়োজনীয় ধারণা

Go-তে `byte` হলো `uint8`-এর alias। এর মান 0–255। `[]byte` হলো byte-এর slice।

| Format verb | অর্থ | 10-এর output |
|---|---|---|
| `%d` | Decimal integer | `10` |
| `%08b` | আট digit-এ binary | `00001010` |

Index বলে byte কোথায় আছে; value বলে সেখানে কোন সংখ্যা আছে।

### Challenge-এর শর্ত

**সমস্যা:** একটি file path নিয়ে প্রতিটি byte-এর index, decimal ও binary মান stdout-এ দেখাও।

**Input**
- ঠিক একটি positional argument: regular file-এর path।
- যেকোনো byte value থাকতে পারে, invalid text-ও থাকতে পারে।
- সর্বোচ্চ file size: 1 MiB (1,048,576 bytes)।

**Output**

```text
INDEX  DECIMAL  BINARY
0      65       01000001
1      66       01000010
2      0        00000000
3      127      01111111
```

Spacing তোমার পছন্দমতো হতে পারে, তবে column স্পষ্ট ও স্থিতিশীল হতে হবে। Empty file-এ কোনো data row থাকবে না। Diagnostic যাবে stderr-এ।

**আচরণগত contract**
- File-কে raw byte হিসেবে পড়বে; আগে string-এ রূপান্তর করবে না।
- Index শূন্য থেকে শুরু হবে।
- Decimal value 0–255-এর মধ্যে হবে।
- Binary value ঠিক আট digit হবে।
- Byte order অপরিবর্তিত থাকবে।
- Zero ও non-printable byte বাদ দেওয়া যাবে না।
- Empty file বৈধ।
- Oversized file reject করলে আংশিক output stdout-এ লেখা যাবে না।

**সীমাবদ্ধতা ও নিরাপত্তা**
- Go standard library ছাড়া কিছু নয়।
- 1 MiB-এর বেশি file reject করতে হবে।
- Input পরিবর্তন বা execute করা যাবে না।
- Untrusted input-কে data হিসেবেই বিবেচনা করবে।

**Edge cases**
- Empty file।
- এক byte `0x00`, এক byte `0xFF`।
- `0x00` থেকে `0xFF` পর্যন্ত সব value।
- Invalid UTF-8।
- ঠিক 1 MiB এবং 1 MiB + 1 byte।

**Error behavior**
- Path নেই বা একাধিক path: stderr-এ usage, non-zero exit।
- File নেই বা পড়া যায় না: stderr-এ সংক্ষিপ্ত error, non-zero exit।
- Size limit অতিক্রম: stderr-এ error, non-zero exit, stdout-এ partial dump নয়।
- সফল হলে exit 0।

**Acceptance criteria**
- `41 42 00 7F` চারটি সঠিক row তৈরি করে।
- Binary field আট digit-এর।
- Empty file সফলভাবে zero row দেয়।
- Missing ও oversized file non-zero exit করে।
- Input file অপরিবর্তিত থাকে।

**Tests:** Temporary file দিয়ে known fixture, empty input, one-byte value, maximum size এবং limit-এর এক byte বেশি পরীক্ষা করো।

**সম্পন্ন হওয়ার শর্ত:** গ্রহণযোগ্য file-এর প্রতিটি byte একবার, সঠিক ক্রমে এবং সঠিক index-সহ দেখানো যায়।

---

# 01.2: Hexdump-এ Byte দেখো

প্রতি byte-এর জন্য আলাদা line সঠিক হলেও বড় file পড়া কঠিন। Hexdump একই সঙ্গে offset, hexadecimal value এবং printable ASCII-এর সংক্ষিপ্ত দৃশ্য দেয়।

### কী তৈরি করবে

একটি অস্থায়ী `--hex` flag যোগ করবে। প্রতি row-তে ১৬টি byte থাকবে। 01.5-এ এটি unified `--format hex` দিয়ে প্রতিস্থাপিত হবে; final tool-এ `--hex` থাকবে না।

### ধারণা ও দৃশ্য

প্রতি row-তে তিনটি অংশ:

1. Offset: row-এর প্রথম byte-এর অবস্থান।
2. Hex columns: প্রতিটি byte-এর দুই digit-এর hex value।
3. ASCII sidebar: শুধু printable ASCII।

```text
00000000  48 65 6c 6c 6f 00 57 6f 72 6c 64 0a              |Hello.World.|
^^^^^^^^  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ^^^^^^^^^^^^^
offset    hex bytes                                        ASCII view
```

শুধু `0x20`–`0x7E` printable হিসেবে দেখাবে। অন্য সব byte-এর জায়গায় `.`। শেষ row-তে ১৬টির কম byte থাকলে alignment-এর জন্য hex area pad হবে, কিন্তু sidebar-এ phantom byte দেখানো যাবে না।

### Challenge specification

**Input:** 01.1-এর file path এবং `--hex` flag। Size limit 1 MiB।

**Contract**
- প্রতি row-তে সর্বোচ্চ ১৬টি consecutive byte।
- Offset আট digit-এর, zero-padded, lowercase hexadecimal।
- Hex value দুই digit-এর।
- ASCII sidebar একই byte থেকে তৈরি হবে।
- Non-printable byte `.` হবে।
- Empty input-এ row থাকবে না।
- আগের decimal/binary behavior অক্ষত থাকবে।
- Raw control byte terminal-এ পাঠানো যাবে না।

**Edge cases:** Empty, 1, 15, 16 ও 17 byte; `00`, `09`, `0A`, `7F`; printable boundary `20` ও `7E`।

**Acceptance criteria**
- ১৬ byte-এ একটি row, ১৭ byte-এ দ্বিতীয় row offset `00000010`।
- প্রতিটি hex value দুই digit।
- Sidebar printable ASCII ও period সঠিকভাবে দেখায়।
- Padding কোনো অতিরিক্ত byte তৈরি করে না।
- 01.1-এর test অক্ষত থাকে।

**Tests:** Embedded fixture দিয়ে row count, offset, sidebar ও short-row alignment যাচাই করো। প্রয়োজনে `xxd` বা `hexdump -C` দিয়ে manual cross-check করা যায়, তবে test-এর dependency নয়।

---

# 01.3: Offset ও Length দিয়ে নির্দিষ্ট অংশ পরীক্ষা করো

বড় binary file-এর নির্দিষ্ট অংশ পরীক্ষা করতে পুরো file dump করার দরকার নেই। Offset বলে কোথা থেকে শুরু হবে, length বলে কত byte নেওয়া হবে।

### কী তৈরি করবে

`--offset N` ও `--length N` flag যোগ করবে।

Range হলো `[offset, offset+length)`: শুরু অন্তর্ভুক্ত, শেষ অন্তর্ভুক্ত নয়। Length byte গুনে, character নয়। Go slice-ও একই convention ব্যবহার করে।

### Challenge specification

**Input**
- আগের file ও output mode।
- `--offset N`: non-negative base-10 integer, default 0।
- `--length N`: non-negative integer, optional।
- Length না দিলে offset থেকে শেষ পর্যন্ত।

**Contract**
- Length 0 হলে কোনো data row নয়।
- Offset file length-এর সমান হলে length 0 বা omitted বৈধ, কারণ range empty।
- Offset file length-এর বেশি হলে invalid।
- Length remaining byte-এর বেশি হলে reject; silently clamp নয়।
- Hexdump offset এবং decimal index original input-এর absolute position দেখাবে।
- Integer overflow এড়াতে unchecked `offset + length` ব্যবহার করবে না।
- 1 MiB limit অপরিবর্তিত।

**Edge cases**
- Offset 0, length 0।
- শেষ byte-এ offset ও length 1।
- Offset file length-এর সমান, length 0 বা 1।
- Offset file length-এর বেশি।
- Length remaining byte-এর সমান বা এক byte বেশি।
- অত্যন্ত বড় numeric argument।
- Empty file।

**Error behavior:** Negative/malformed value, offset out of range, অথবা length অতিরিক্ত হলে stderr ও non-zero exit। Valid zero-length range সফল।

**Acceptance criteria**
- `--offset 4 --length 8` ঠিক আট byte দেখায়।
- Absolute index/offset বজায় থাকে।
- Invalid range panic করে না বা নীরবে ছোট হয় না।
- আগের milestone-এর test পাস করতে হবে।

**Tests:** Table-driven test; empty file, last-byte selection, exact remaining length, one-byte overflow এবং huge integer।

---

# 01.4: Text Encoding অনুযায়ী Byte ব্যাখ্যা করো

একটি byte sequence প্রায় readable message-এর মতো দেখাতে পারে, কিন্তু মাঝখানে invalid byte থাকতে পারে। সেটিকে প্রশ্নবোধক চিহ্ন দিয়ে বদলে দিলে evidence হারিয়ে যায়।

### কী তৈরি করবে

`--decode ascii` ও `--decode utf8` mode। Invalid বা non-ASCII byte-কে annotation-সহ দেখাবে, বাদ দেবে না।

### প্রয়োজনীয় ধারণা

ASCII হলো 7-bit character encoding; এর standard value 0–127। এর মধ্যেও control character আছে। `0x7F` হলো delete control। 127-এর বেশি value ASCII নয়।

UTF-8 Unicode code point-কে এক থেকে চার byte-এ encode করে। সাধারণ ASCII character UTF-8-এ একই single-byte value ব্যবহার করে।

| Leading byte range | ভূমিকা |
|---|---|
| `00`–`7F` | এক byte-এর ASCII-compatible code point |
| `C2`–`DF` | দুই byte sequence শুরু |
| `E0`–`EF` | তিন byte sequence শুরু |
| `F0`–`F4` | চার byte sequence শুরু |
| `80`–`BF` | Continuation byte |
| অন্যান্য | Invalid leading byte |

শুধু byte range দেখে UTF-8 validity নির্ধারণ করা যায় না। Overlong encoding, surrogate এবং Unicode range-এর বাইরের value-ও invalid। Go-এর `unicode/utf8` ব্যবহার করে validation করতে হবে।

যেমন `€` হলো U+20AC এবং UTF-8 byte `E2 82 AC`। Range যদি মাঝখান থেকে শুরু হয়, নির্বাচিত fragment নিজে incomplete হতে পারে এবং সেটিকে invalid হিসেবে দেখাতে হবে।

### Challenge specification

**Input:** আগের file/range option এবং `--decode ascii|utf8`।

**ASCII output**
- 0–127 ASCII range-এর মধ্যে।
- `0x20`–`0x7E` printable।
- Control value non-printable হিসেবে চিহ্নিত।
- `0x7F`-এর বেশি value `[non-ASCII]`।

**UTF-8 output**
- Valid sequence decode হবে।
- Invalid byte/sequence `[invalid]` annotation পাবে; raw hex value দৃশ্যমান থাকবে।
- Unicode General_Category `Cc`-এর control character, C0/C1-সহ, দৃশ্যমান escape হবে; যেমন ESC: `\\u{001B}`। LF, TAB-সহ কোনো control character literal terminal-এ পাঠানো যাবে না।
- Byte order বজায় থাকবে।
- Invalid byte repair, normalize, skip বা গোপনে replace করা যাবে না।

**Edge cases:** Empty input, pure ASCII, NUL/TAB/CR/LF, valid 2/3/4-byte UTF-8, lone continuation byte, incomplete sequence, invalid leading byte, overlong encoding, surrogate, U+10FFFF-এর বেশি value, multi-byte sequence-এর মাঝখানে শুরু/শেষ হওয়া range।

**Error behavior**
- Unknown decode mode: stderr, non-zero।
- Invalid range: 01.3-এর নিয়ম।
- Invalid UTF-8 data command error নয়; annotation-সহ সফলভাবে দেখাবে।
- File/I/O error আগের মতো।

**Security:** Control character escape করবে, যাতে untrusted input terminal state বদলাতে না পারে। Raw byte evidence অক্ষত থাকবে।

**Acceptance criteria**
- Emoji-সহ valid sequence সঠিকভাবে চিহ্নিত।
- Lone continuation ও incomplete sequence invalid।
- ASCII-তে 0x7F-এর বেশি non-ASCII।
- Control character raw output নয়।
- Invalid byte-এর original hex value পাওয়া যায়।
- Split range-এ incomplete fragment সঠিকভাবে চিহ্নিত।
- আগের সব test অক্ষত।

**Tests:** Embedded fixture দিয়ে valid 1–4 byte sequence, lone continuation, incomplete, overlong, surrogate ও out-of-range code point পরীক্ষা করো। Locale বা terminal encoding-এর ওপর নির্ভর করবে না।

---

# 01.5: Stdin ও একাধিক Format গ্রহণ করো

Samia এবার pipeline থেকে byte পেয়েছে, file হিসেবে নয়। একই tool যেন file এবং stdin দুই উৎস থেকেই পড়তে পারে। Input কোথা থেকে এসেছে, তার ওপর output বদলানো চলবে না।

### কী তৈরি করবে

File path অথবা stdin input এবং unified `--format` option:

- `hex`
- `decimal`
- `binary`
- `utf8`
- `ascii`

Default format: `hex`।

### প্রয়োজনমতো Theory

File argument একটি named file চিহ্নিত করে। Standard input (stdin) shell, pipe বা অন্য process থেকে stream পায়।

```text
producer stdout ───────► byteinspect stdin
```

Stream-এর মোট size আগে থেকে জানা নাও থাকতে পারে। তাই পড়ার সময় limit enforce করতে হবে।

### Challenge specification

**Input**
- Optional একটি positional file path।
- Path না থাকলে stdin।
- একাধিক path invalid।
- `--format`-এ উপরের পাঁচটি value।
- `--offset`, `--length` আগের নিয়মে।
- Default format `hex`।
- সর্বোচ্চ input: 10 MiB (10,485,760 bytes)।

**Behavioral contract**
- ঠিক একটি input source ব্যবহার করবে।
- File ও stdin-এ একই byte এবং option দিলে output অভিন্ন হবে।
- Range validation দুই input source-এ একই।
- Limit detect করতে সর্বোচ্চ 10 MiB + 1 byte পড়বে।
- EOF ও size check সফল হওয়ার আগে stdout-এ formatted output লিখবে না।
- Limit ছাড়ালে stderr-এ error, non-zero exit এবং stdout-এ কোনো partial dump নয়।
- Limit-এর সমান বা কম stream বৈধ; empty stream-ও বৈধ।
- Unsupported format error; silent fallback নয়।
- `hex` 01.2-এর hexdump, `decimal` 01.1-এর index/value, `binary` আট digit, `utf8`/`ascii` 01.4-এর নিয়ম অনুসরণ করবে।
- File ও stdin-এর read error স্পষ্টভাবে জানাবে।
- Input read-only থাকবে।

**Edge cases:** Empty stdin, exact 10 MiB, 10 MiB + 1, file বনাম pipe-এর অভিন্ন data, invalid format, একাধিক path, invalid range, stream read error, EOF-এর ঠিক আগে/পরে limit।

**Acceptance criteria**
- File ও stdin একই output দেয়।
- Default format hex।
- পাঁচটি format সঠিক।
- Range semantics অপরিবর্তিত।
- Oversized stream-এ stdout খালি থাকে।
- কোনো unbounded read বা partial dump নেই।
- আগের সব milestone test পাস।

**Tests:** In-memory reader, temporary file ও pipe-like reader ব্যবহার করো। Exact limit এবং limit+1 byte পরীক্ষা করো। Read error inject করো। Public network বা machine-specific file-এর ওপর নির্ভর করবে না।

## চূড়ান্ত Tool contract

| বিষয় | চূড়ান্ত নিয়ম |
|---|---|
| Tool | `byteinspect` |
| Input | একটি file path অথবা stdin |
| Default format | `hex` |
| Formats | `hex`, `decimal`, `binary`, `utf8`, `ascii` |
| Range | Zero-based byte offset ও length |
| Maximum input | 10 MiB |
| Invalid UTF-8 | Annotation-সহ raw evidence বজায় |
| Terminal safety | Control character escape |
| Side effects | কোনো file পরিবর্তন/execute/upload নয় |
| Maturity | L2 |

## Red Team ও Blue Team-এর শেখা

🔴 **Rayhan:** Synthetic fixture-এর byte signature, control byte, printable ASCII ও invalid UTF-8 খুঁজে বের করো। প্রতিটি finding-এর offset ও raw hex value নথিভুক্ত করো। Interpretation-কে raw evidence হিসেবে উপস্থাপন করবে না।

🔵 **Samia:** একই fixture দিয়ে নিশ্চিত করো, inspector control byte terminal-এ পাঠায় না, oversized stream-এ partial output দেয় না এবং invalid byte বাদ দেয় না। Test-এ raw byte ও rendered output তুলনা করো।

## অধ্যায় সমাপ্তির checklist

- [ ] Decimal/binary inventory সঠিক।
- [ ] ১৬-byte hexdump row ও absolute offset সঠিক।
- [ ] Range validation overflow-safe।
- [ ] ASCII/UTF-8 interpretation invalid byte সংরক্ষণ করে।
- [ ] Unicode control character escape হয়।
- [ ] File ও stdin একই format contract মেনে চলে।
- [ ] 10 MiB limit bounded এবং oversized input-এ stdout আংশিক নয়।
- [ ] সব milestone-এর regression test আছে।
- [ ] Input কখনো পরিবর্তিত বা execute হয় না।
- [ ] Red/Blue উভয় exercise-এর evidence যাচাই করা হয়েছে।
