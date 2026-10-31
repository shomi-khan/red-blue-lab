# Content Templates

Template consistency দেয়, rigid formula নয়। অপ্রাসঙ্গিক section বাদ দাও; placeholder রেখে দিও না।

## 1. Volume / story arc

~~~markdown
# [Volume Title]

> [Spoiler-free premise]

## Narrative promise
[Genre tone ও reader expectation]

## Story arc
[Opening, escalation, midpoint shift, climax, consequence]

## Central mystery
[প্রধান প্রশ্ন; reveal timing planning note-এ]

## Character arcs
[Approved goal, conflict, change, unresolved tension]

## Continuity dependencies
[আগের ঘটনা, evidence ও character knowledge]

## Optional learning connections
[সম্ভাব্য domain; plot-কে dictate করবে না]
~~~

## 2. Episode

~~~markdown
# [Episode Title]

[Novel prose: scene, dialogue, conflict, investigation, discovery ও consequence]

> **[IMAGE PLACEHOLDER: IMG-[EPISODE-ID]-01]**
>
> - **Placement:**
> - **Purpose:**
> - **Caption:**
> - **Alt text:**
> - **Generation prompt (English):**
>   > [Detailed prompt]
> - **Continuity notes:**

## Continuity update
- New facts:
- Character knowledge changes:
- Evidence introduced:
- Hypotheses changed:
- Unresolved questions:
- Next episode dependencies:
~~~

Novel-এর মধ্যে বাধ্যতামূলক Learning Objectives, What you will build বা Challenge section ঢোকাবে না।

## 3. Concept Note

~~~markdown
# [Concept Title]

## কেন গুরুত্বপূর্ণ
[প্রশ্ন বা সমস্যা]

## এক নজরে
[সংক্ষিপ্ত mental model]

## Visual model
[Diagram]

## ধাপে ধাপে ব্যাখ্যা
[Mechanism ও data/control flow]

## Concrete example
[Accurate example]

## Failure modes ও security implications
[কী ভুল হতে পারে]

## কী জানা যায় / যায় না
[Evidence ও limitation]

## Experiment (optional)
[Local/synthetic observation]

## Further reading
[Authoritative source]
~~~

## 4. Lab Specification

~~~markdown
# [Lab Title]

## Narrative connection
[কোন প্রশ্নের সঙ্গে সম্পর্ক]

## Problem ও learning scope
[কী বোঝা বা verify করা হবে]

## Prerequisites
[আগের knowledge]

## Environment and authorization
[Local target, fixture, explicit scope]

## System model
[Diagram ও explanation]

## Requirements
[Observable behavior, input/output, constraints]

## Edge cases and failure behavior
[Boundary, timeout, error, ambiguity]

## Security invariants
[যে property ভাঙা যাবে না]

## Verification
[Test ও experiment expectation]

## Reflection
[কী প্রমাণিত, কী অপ্রমাণিত]

## Optional extension
[আরও গভীর exploration]
~~~

## 5. Visual specification

~~~markdown
## Visual: [ID] — [Title]

- Purpose:
- Type: flowchart / sequence / architecture / timeline / image
- Placement:
- Question it answers:
- Required elements:
- Must not imply:
- Caption:
- Alt text:

### Diagram source
[Mermaid বা annotated text]

### Image generation prompt (narrative image হলে)
> [English prompt]
~~~

## 6. Synthetic Evidence Pack

~~~markdown
# Evidence Pack: [Scenario ID]

> Synthetic training data. বাস্তব system থেকে সংগৃহীত নয়।

## Scenario context
## Scope
## Artifacts
## Timestamp and timezone
## Integrity metadata
## Known facts
## Unknowns
## Investigation questions
~~~

## 7. Review report

~~~markdown
# Review: [Artifact]

## Summary
## Critical issues
## Narrative
## Technical accuracy
## Learning depth
## Visuals
## Language
## Safety
## Continuity
## Suggested changes
## Decision: Ready / Needs revision / Blocked
~~~
