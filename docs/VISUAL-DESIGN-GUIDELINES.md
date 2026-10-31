# Visual Design Guidelines

Visual decoration নয়; বোঝাপড়া ও storytelling-এর মাধ্যম। সঠিক visual complex system দৃশ্যমান করে, ভুল visual ভুল mental model তৈরি করে।

## 1. দুই ধরনের visual

**Explanatory visuals:** Mermaid flowchart, sequence, architecture, data-flow, state transition, attack-path graph, timeline, table, annotated packet/request/response, ASCII byte layout।

**Narrative images:** Location establishing shot, character interaction, environment, fictional artifact, atmosphere বা scene transition।

Narrative image technical architecture-এর বিকল্প নয়।

## 2. Visual selection flow

~~~mermaid
flowchart TD
 A[কী বোঝাতে হবে?] --> B{System, behavior বা data?}
 B -->|হ্যাঁ| C{কোন সম্পর্ক?}
 C -->|Component| D[Architecture]
 C -->|Time sequence| E[Sequence]
 C -->|Decision| F[Flowchart]
 C -->|State change| G[State diagram]
 C -->|Field/value| H[Table বা annotated layout]
 B -->|Narrative scene| I{ছবি কি imagination উন্নত করবে?}
 I -->|হ্যাঁ| J[Image placeholder + prompt]
 I -->|না| K[শুধু prose]
~~~

## 3. Mermaid rules

- Diagram সরাসরি Markdown-এ embed করো।
- আগে বলো পাঠক কী দেখবে; পরে key takeaway ব্যাখ্যা করো।
- একটি diagram-এ একটি primary question।
- Node label সংক্ষিপ্ত ও পরিষ্কার।
- Direction, trust boundary ও state সঠিক হতে হবে।
- বড় diagram ছোট context/component/sequence/failure diagram-এ ভাঙো।
- Bengali explanatory label; protocol token ও identifier English।
- Decorative diagram বাদ।

## 4. Diagram type

| Visual | ব্যবহার | এড়াতে হবে |
|---|---|---|
| Flowchart | Decision ও investigation logic | সবকিছুকে decision বানানো |
| Sequence | Protocol ও actor interaction | ভুল ordering |
| Architecture | Component ও dependency | Trust boundary বাদ |
| Data-flow | Data source, processing, storage, egress | Sensitive data path লুকানো |
| State | Lifecycle ও transition | Invalid transition |
| Attack-path | Weakness থেকে impact | সম্ভাব্য path-কে confirmed বলা |
| Timeline | Incident chronology | Timestamp/timezone গুলিয়ে ফেলা |
| Table | Field, state, trade-off | prose পুনরাবৃত্তি |

## 5. Narrative image placeholder

এই format ব্যবহার করো:

~~~markdown
> **[IMAGE PLACEHOLDER: IMG-EP01-01]**
>
> - **Placement:** কোন paragraph-এর পরে।
> - **Purpose:** কোন visual context তৈরি করবে।
> - **Caption:** বাংলা caption।
> - **Alt text:** ছবির নিরপেক্ষ বর্ণনা।
> - **Generation prompt (English):**
>   > A cinematic, grounded cyber-thriller establishing shot...
> - **Continuity notes:** Approved reference অনুসরণ।
~~~

Prompt-এ subject/action, environment, composition, lighting/mood, camera framing, style, props ও exclusions উল্লেখ করো। World Bible অনুমোদিত হওয়ার আগে character face, costume বা signature design স্থির করো না।

## 6. Image quality

- Image নতুন context বা atmosphere যোগ করবে।
- শুধু সুন্দর দেখাবে বলে image দেবে না।
- একই ধরনের control-room image বারবার নয়।
- Generated text, UI label বা code সাধারণত image-এ নয়; পরে আলাদা করে যোগ করো।
- Character likeness ও copyright scope বিবেচনা করো।
- Prompt English; caption, placement note ও explanation বাংলা।

## 7. Density ও accessibility

- এক পৃষ্ঠায় অতিরিক্ত visual নয়।
- Dense explanation-এর মাঝে visual break।
- একই concept prose, diagram ও table-এ অকারণে repeat নয়।
- প্রতিটি scene-এ image বাধ্যতামূলক নয়।
- Image alt text থাকবে।
- Diagram-এর takeaway prose-এও থাকবে।
- Meaning শুধু রঙের ওপর নির্ভর করবে না।
