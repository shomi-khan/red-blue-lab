# Assessment Architecture

> Status: User-approved architecture direction
> Scope: Assessment definition, deterministic evaluation, authoring validation ও safe code execution
> এই document assessment-এর architectural contract নির্ধারণ করে; এটি runtime implementation specification নয়।

## 1. উদ্দেশ্য ও guiding principle

Assessment-এর উদ্দেশ্য শুধু তথ্য মনে আছে কি না যাচাই করা নয়; learner প্রয়োজনীয় knowledge ও competency বাস্তবে demonstrate করতে পারে কি না যাচাই করা।

**মূল নীতি: Easy to understand, difficult to pass without genuine understanding.**

প্রশ্নের ভাষা ও instruction পরিষ্কার হবে। কঠোরতা আসবে Learning Objective-এর সঙ্গে সামঞ্জস্যপূর্ণ evaluation criteria, evidence-based task এবং critical competency requirement থেকে; অপ্রাসঙ্গিক trick question বা অকারণ জটিলতা থেকে নয়।

Assessment design-এর guiding principle:

**Assessment should measure demonstrated understanding, not memorized information.**

প্রতিটি assessment এক বা একাধিক Learning Objective (LO)-এর সঙ্গে যুক্ত থাকবে। কোনো প্রশ্নের LO-তে অবদান বা স্পষ্ট মূল্য না থাকলে সেটি assessment-এ রাখা যাবে না।

## 2. Non-negotiable evaluation rules

- সব assessment automated ও deterministic হবে।
- কোনো AI-based evaluator বা AI answer validation থাকবে না।
- কোনো human reviewer বা manual grading থাকবে না।
- Free-form text / paragraph / essay answer থাকবে না।
- সব learner submission predefined structured format-এ হবে, অথবা Code Challenge-এর ক্ষেত্রে source code হবে।
- একই assessment version, একই submission, একই evaluator version এবং একই execution environment-এর জন্য একই evaluation result তৈরি হতে হবে।
- Evaluation rules assessment authoring-এর সময় নির্ধারিত থাকবে; runtime-এ subjective interpretation হবে না।

যে উত্তর predefined deterministic rules দিয়ে নির্ভরযোগ্যভাবে যাচাই করা সম্ভব নয়, সেই answer format ব্যবহার করা যাবে না।

## 3. Assessment components

তিনটি primary component আলাদা responsibility পালন করবে।

### 3.1 Markdown Assessment Definition

Markdown হবে assessment content ও author-defined rules-এর canonical source।

এতে থাকবে:

- Assessment identity ও metadata
- সংশ্লিষ্ট Learning Objective
- Learner-facing instructions
- Fixed questions ও fixed question order
- Question type ও structured answer specification
- Visible/hidden test case definitions, যেখানে প্রযোজ্য
- Hints ও deterministic feedback content
- Difficulty indication
- Scoring rules ও question weights
- Passing score ও mandatory pass criteria
- Evaluation criteria
- Prerequisite বা stage relationship, যেখানে প্রযোজ্য

Exact YAML Frontmatter schema এবং identifier convention আলাদা implementation design-এ স্থির হবে। এই document নিজে কোনো unapproved machine-readable schema বাধ্যতামূলক করছে না।

### 3.2 Assessment Engine

Assessment Engine-এর দায়িত্ব:

- Learner submission গ্রহণ করা।
- Assessment definition ও version resolve করা।
- Submission format ও required fields validate করা।
- সংশ্লিষ্ট evaluator নির্বাচন ও invoke করা।
- Evaluator output থেকে score ও status তৈরি করা।
- Deterministic feedback ও explanation সংযুক্ত করা।
- Attempt এবং result সংরক্ষণের উপযোগী structured output তৈরি করা।

Engine নিজে প্রতিটি question type-এর evaluation logic ধারণ করবে না। এটি generic orchestration layer হবে।

### 3.3 Sandboxed Code Runner

Code Runner কেবল Code Challenge-এর code execute করবে। এটি Assessment Engine থেকে আলাদা security boundary-তে থাকবে।

Runner-এর দায়িত্ব:

- নির্ধারিত language/runtime-এ submitted code execute করা।
- Test harness-এর সঙ্গে code চালানো।
- Test result ও execution metadata ফেরত দেওয়া।
- Resource ও execution limit enforce করা।

Runner-এর failure বা compromise যেন Assessment Engine, host infrastructure বা অন্য learner-এর execution environment-এ ছড়িয়ে না পড়ে।

## 4. Assessment types

সব answer predefined এবং machine-verifiable হবে।

| Type | Learner submission | Deterministic evaluation |
|---|---|---|
| Multiple Choice | একটি option নির্বাচন | Exact option matching |
| Multiple Select | একাধিক option নির্বাচন | Defined set comparison |
| True / False | Boolean selection | Exact matching |
| Matching | Predefined pair নির্বাচন | Expected mapping comparison |
| Ordering | Item-গুলোর sequence | Expected order comparison |
| Scenario-based | Structured decision/option selection | Predefined decision rules |
| Evidence Analysis | Finding, indicator বা interpretation নির্বাচন | Expected finding/rule matching |
| Configuration Challenge | Structured configuration | Schema ও policy validation |
| Code Challenge | Source code | Sandboxed execution ও automated tests |

Scenario-based এবং Evidence Analysis-এ paragraph বা free-form explanation চাওয়া যাবে না। Learner predefined options, structured selections বা supported structured fields-এর মাধ্যমে উত্তর দেবে।

**Short Answer / Free-form Text Assessment থাকবে না।**

Assessment-এ শুধু Multiple Choice-এর ওপর নির্ভর করা উচিত নয়। Matching, Ordering, Evidence Analysis, Scenario-based এবং Code Challenge-এর মতো interaction দিয়ে বিভিন্ন ধরনের competency যাচাই করতে হবে।

## 5. Fixed Assessment ও attempt policy

প্রথম সংস্করণে **Fixed Assessment** ব্যবহার হবে।

- একই assessment version-এ question set fixed থাকবে।
- Question order fixed থাকবে।
- প্রতিবার attempt-এ একই প্রশ্ন ও একই order দেখানো হবে।
- Question Pool, random selection, adaptive difficulty বা adaptive assessment থাকবে না।
- Learner-এর attempt সংখ্যা unlimited হবে।
- একই stage-এ learner একই assessment পুনরায় দিতে পারবে।
- প্রতিটি attempt-এর submission ও result আলাদা record হিসেবে সংরক্ষণযোগ্য হতে হবে।

Unlimited attempt মানে assessment-এর criteria শিথিল হবে না। Learner পুনরায় চেষ্টা করতে পারবে, কিন্তু Pass করার জন্য একই competency requirements পূরণ করতে হবে।

## 6. Difficulty ও competency-based rigor

Assessment-এ প্রয়োজন অনুযায়ী Easy, Medium এবং Hard প্রশ্নের মিশ্রণ থাকবে। Difficulty distribution assessment blueprint-এ নির্ধারিত হবে; সব assessment-এ একই fixed ratio বাধ্যতামূলক নয়।

Difficulty label নিজে competency-এর প্রমাণ নয়। প্রশ্নের মান নির্ধারিত হবে সেটি LO-এর কোন capability যাচাই করছে তার ভিত্তিতে।

উদাহরণ: TCP Three-Way Handshake সম্পর্কে learner-কে শুধু SYN, SYN-ACK ও ACK-এর নাম চিনতে পারলেই যথেষ্ট নয়। প্রয়োজন অনুযায়ী তাকে packet sequence trace, sequence number interpret এবং অস্বাভাবিক exchange বিশ্লেষণ করতে হতে পারে।

- Basic question foundational recognition ও understanding যাচাই করতে পারে।
- Intermediate question mechanism trace বা evidence interpret করতে পারে।
- Advanced question unfamiliar context-এ analysis, diagnosis বা engineering decision যাচাই করতে পারে।

কঠিন প্রশ্নের নামে অস্পষ্ট wording, trick বা LO-বহির্ভূত trivia ব্যবহার করা যাবে না।

## 7. Assessment Blueprint ও passing policy

প্রতিটি assessment-এর একটি Blueprint থাকবে। Blueprint-এ অন্তত নিচের বিষয়গুলো নির্ধারিত হবে:

- কোন LO বা LO-গুলো যাচাই হচ্ছে।
- কোন competency বা capability যাচাই হবে।
- কোন question type ব্যবহার হবে।
- Question difficulty এবং question weight।
- Scoring policy।
- Overall passing score।
- Mandatory pass criteria, যেখানে critical competency আছে।

Scoring policy configurable হতে পারে:

- Exact / all-or-nothing score
- Partial score
- Weighted score
- নির্ধারিত penalty, যদি assessment-এর জন্য যুক্তিযুক্ত হয়

### Mandatory pass criteria

শুধু overall score অর্জন করলেই সবসময় Pass হবে না। কোনো LO-এর critical competency যাচাইয়ের জন্য নির্দিষ্ট question বা criterion বাধ্যতামূলক করা যেতে পারে।

Pass হওয়ার জন্য:

1. Overall passing score অর্জন করতে হবে।
2. Assessment-এ নির্ধারিত সব mandatory pass criteria পূরণ করতে হবে।

কোনো mandatory criterion fail হলে overall score threshold অতিক্রম করলেও assessment status হবে Fail। Mandatory criterion assessment definition-এ স্পষ্টভাবে চিহ্নিত থাকতে হবে।

## 8. Deterministic feedback ও result

Assessment result শুধু Pass/Fail এবং total score-এ সীমাবদ্ধ থাকবে না।

সম্ভব হলে result-এ থাকবে:

- Overall status ও score
- Passing threshold
- Question-level status ও score
- কোন evaluation criteria পূরণ হয়েছে বা হয়নি
- Pre-authored explanation ও hint
- Code Challenge-এর ক্ষেত্রে test case result ও নিরাপদ execution summary

Feedback content assessment definition বা deterministic evaluator থেকে আসবে। AI-generated বা human-authored-at-runtime interpretation থাকবে না।

Feedback learner-কে ভুলের জায়গা বুঝতে সাহায্য করবে, কিন্তু assessment-এর answer disclosure policy আলাদা করে নির্ধারণ করা যেতে পারে।

## 9. Assessment versioning ও reproducibility

Published assessment পরিবর্তন করলে নতুন version তৈরি হবে। পুরোনো version-এর definition overwrite করে পুরোনো attempt-এর meaning পরিবর্তন করা যাবে না।

প্রতিটি attempt-এর সঙ্গে অন্তত এগুলো trace করা সম্ভব হতে হবে:

- Assessment ID ও version
- Submitted answer / code-এর reference বা immutable record
- Evaluator identity ও version
- Score, status ও question-level result
- Code Challenge হলে runner image/runtime ও test harness version

এর ফলে পুরোনো result তার সময়কার assessment ও evaluation rules অনুযায়ী ব্যাখ্যা এবং প্রয়োজনে reproduce করা যাবে।

## 10. Evaluator architecture

Assessment Engine generic থাকবে। আলাদা deterministic evaluator assessment type অনুযায়ী evaluation করবে।

উদাহরণ:

- Multiple Choice Evaluator
- Multiple Select Evaluator
- Matching / Ordering Evaluator
- Scenario Evaluator
- Evidence Evaluator
- Configuration Evaluator
- Code Evaluator

Evaluator-এর contract হবে স্পষ্ট: validated input গ্রহণ, deterministic evaluation এবং standardized structured result ফেরত দেওয়া।

নতুন assessment type যোগ করতে হলে নতুন evaluator যুক্ত করা যাবে; core Engine-এর orchestration logic অকারণে পরিবর্তন করতে হবে না।

## 11. Assessment Authoring Validation Tooling

Authoring Validator learner submission evaluate করবে না। এটি author-এর Markdown assessment definition publish করার আগে validate করবে।

প্রস্তাবিত validation:

| Validation area | কী পরীক্ষা করবে |
|---|---|
| Frontmatter | Required metadata ও schema |
| ID integrity | Missing বা duplicate ID |
| LO references | Referenced Learning Objective আছে কি না |
| Question structure | Question type অনুযায়ী required fields ও valid options |
| Answer key | Correct answer / expected mapping valid কি না |
| Evaluator availability | সংশ্লিষ্ট evaluator registered ও supported কি না |
| Scoring | Weight, score ও passing criteria consistent কি না |
| Mandatory criteria | Referenced question/criterion আছে কি না |
| Test cases | Input, expected output ও case definition valid কি না |
| Fixed order | Question order explicit ও unambiguous কি না |
| Feedback | Feedback/hint reference valid কি না |
| Version metadata | Published version ও references consistent কি না |

### Authoring tools

**Assessment Linter:** Markdown structure, metadata, references ও authoring convention পরীক্ষা করবে।

**Assessment Test Harness:** Sample submissions দিয়ে evaluator চালাবে এবং expected result-এর সঙ্গে actual result তুলনা করবে। PASS, FAIL ও PARTIAL-এর মতো representative case থাকতে হবে।

**Assessment Preview:** Learner-facing instructions, questions, options ও ordering publish করার আগে preview করতে দেবে।

এই tooling-ও deterministic হবে। Validation error ও warning স্পষ্টভাবে report করবে।

## 12. Sandboxed Code Runner security boundary

Learner-submitted code untrusted input হিসেবে বিবেচিত হবে।

Runner-এর জন্য security requirements:

- প্রতিটি execution isolated environment-এ চলবে।
- Network access default হিসেবে disabled থাকবে।
- CPU, memory, process count, disk ও execution time সীমিত থাকবে।
- Filesystem access সীমিত থাকবে।
- Host privilege, secrets ও অন্য execution-এর data access করা যাবে না।
- Output size সীমিত থাকবে।
- Execution শেষে ephemeral environment destroy করা হবে।
- Runtime, dependency ও test harness version controlled/pinned থাকবে।
- Runner কেবল structured result Assessment Engine-এ ফেরত দেবে।

Visible test case learner-এর কাছে প্রকাশ করা যেতে পারে। Hidden test case final evaluation-এর জন্য গোপন থাকবে। Hidden test case-এর output বা implementation details learner-facing feedback-এ leak করা যাবে না।

প্রথম সংস্করণে কোন language/runtime support হবে এবং infrastructure-level isolation কীভাবে implement হবে, তা আলাদা technical design-এ নির্ধারিত হবে।

## 13. High-level evaluation flow

~~~mermaid
flowchart TD
    A[Markdown Assessment Definition] --> B[Assessment Authoring Validator]
    B --> C[Validated Assessment Repository]
    D[Student Submission] --> E[Assessment Engine]
    C --> E
    E --> F{Evaluator Registry}
    F --> G[Structured Evaluators]
    F --> H[Code Evaluator]
    H --> I[Sandboxed Code Runner]
    G --> J[Scoring and Feedback]
    I --> J
    J --> K[Deterministic Result]
    K --> L[Attempt History]
~~~

## 14. Out of scope for the initial design

প্রথম সংস্করণে নিচের বিষয়গুলো implement বা finalize করা হচ্ছে না:

- Dynamic Question Pool ও random selection
- Adaptive Assessment
- Free-form text / essay answer
- AI-based grading বা AI validation
- Human review / manual grading
- Multiple learner-specific assessment paths
- Production deployment topology ও runner orchestration
- Supported programming language/runtime-এর চূড়ান্ত তালিকা
- Exact YAML Frontmatter schema ও evaluator API contract
- Database schema ও analytics implementation

## 15. Open technical design work

পরবর্তী implementation planning-এ নির্ধারণ করতে হবে:

- Assessment metadata ও Markdown content schema
- Stable Assessment ID ও version convention
- Evaluator input/output contract
- Scoring calculation ও rounding rules
- Attempt/result persistence model
- Feedback ও hint disclosure policy
- Authoring Validator CLI/API ও CI integration
- Code Runner isolation technology, supported runtimes ও resource limits
- Assessment preview ও learner-facing rendering contract

এই সিদ্ধান্তগুলো আলাদা review-এর মাধ্যমে স্থির হবে। এই architecture document implementation detail অনুমান করে চূড়ান্ত করছে না।
