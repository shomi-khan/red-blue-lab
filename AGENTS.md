# AGENTS.md — Instructions for AI-Assisted Work on red-blue-lab

This file governs how AI agents should contribute to this repository. Read it completely before making any changes.

---

## Primary Sources of Truth

| Document | Purpose |
|---|---|
| [`docs/CURRICULUM.md`](docs/CURRICULUM.md) | Canonical chapter plan, milestone blueprints, tool lifecycles, dependencies |
| [`docs/CONTENT-GUIDELINES.md`](docs/CONTENT-GUIDELINES.md) | Chapter structure, writing rules, challenge format, visual rules, quality checklist |
| This file | Agent-specific behavioural constraints |

Before authoring or modifying a chapter, read the relevant entries in `CURRICULUM.md` and the complete `CONTENT-GUIDELINES.md`.

---

## When Authoring a Chapter

### Read first, write second

1. Read the chapter's full entry in `CURRICULUM.md`: identity, outcomes, prerequisites, milestone plan, tool lifecycle, testing strategy, Red/Blue learning, and visual plan.
2. Read `CONTENT-GUIDELINES.md` in full if you have not done so in this session.
3. Identify which existing tools or chapters the new chapter depends on. Read them if they exist in `chapters/`.

### Respect the milestone structure

- Each subchapter corresponds to exactly one milestone from the curriculum plan.
- Do not combine milestones or skip ahead because they seem minor.
- Each milestone must end with the learner holding a working, testable increment.

### Preserve independent challenges

- Do not include implementation code in the regular chapter body.
- Do not provide a starter implementation that effectively solves the challenge.
- Do not write fill-in-the-blank exercises that remove meaningful implementation decisions.
- Do provide clear behavioral contracts: inputs, outputs, error states, constraints, acceptance criteria.
- Hints may be included in a collapsible section or a separate `hints/` note. Hints must be conceptual, not code-revealing.
- A complete reference implementation may only be included if the chapter explicitly designates a reference section and the curriculum approves it.

### Introduce theory incrementally

- Teach only what is needed for the current milestone.
- Do not front-load theory for future milestones.
- Introduce each new concept immediately before the milestone that requires it.

### Use capability-first naming

- Chapter titles: `[Memorable Capability]: Build [Concrete Tool]`
- Subchapter titles: outcome-oriented, specific to the milestone gained
- Do not use generic academic titles.

### Embed diagrams in Markdown

- All Mermaid diagrams go directly in the chapter `.md` file.
- Do not create a `diagrams/` directory, a chapter-level diagram folder, or separate diagram files.
- Every diagram must explain a concept. Do not add diagrams for decoration.
- Explain the diagram's key takeaways in nearby text.

---

## When Modifying Existing Content

### Check prerequisites and downstream dependencies before changing a chapter

`CURRICULUM.md` documents which chapters depend on each chapter's tools and outcomes. Verify that changes do not silently invalidate downstream work.

### Preserve established tool contracts

- Do not change a tool's output format, error behavior, or state classification without explicit justification.
- Document intentional contract changes in the chapter's debrief section and in `CURRICULUM.md`.
- Add regression tests when modifying existing behavior.

### Update CURRICULUM.md when a change affects scope

If a chapter is split, merged, reordered, or its milestone plan materially changes, update the relevant entries in `CURRICULUM.md`. Do not let the curriculum drift out of sync with the actual chapters.

---

## Safety and Security Boundaries

- All exercises must target local test servers, synthetic traffic, intentionally vulnerable local applications, or explicitly authorized targets.
- Do not design exercises that depend on external public services.
- Where a tool can reach external systems, make the scope and authorization requirements explicit in the challenge specification.
- Safe defaults are mandatory: tools must use timeouts, respect resource limits, and handle cancellation.
- Do not teach users to disable certificate validation, suppress errors, or ignore security warnings as routine practice.

---

## Testing

- Do not claim that tests passed if none were run.
- Do not assert that a tool is correct based on reading the code alone.
- Include deterministic local test fixtures wherever the behavior can be verified without a live network.
- When the curriculum plan specifies a verification approach for a milestone, implement it.

---

## Repository Structure

The intended structure is minimal. Do not introduce new top-level directories without a strong curriculum justification.

**Allowed to create as implementation begins:**
- `chapters/NN-chapter-slug/` — chapter content
- `go.mod` — when the first Go implementation begins
- Tool directories as implementation milestones are reached

**Do not create prematurely:**
- `diagrams/`
- `scripts/`
- `cmd/`, `internal/`
- `lab/`
- `Makefile`, `.github/workflows/`, Docker configuration

These are introduced when actual implementation work justifies them.

---

## Red/Blue Balance

Maintain meaningful offensive and defensive coverage across the overall curriculum. When writing a chapter:

- Identify which Red Team activities and Blue Team activities the chapter covers.
- Do not treat Blue Team content as a short note appended to an offensive tutorial.
- Connect offensive findings to defensive actions explicitly.

---

## Honesty Constraints

- Do not claim unverified behavior.
- Do not invent curriculum details not present in `CURRICULUM.md`. If details are missing, flag the gap rather than inventing a resolution.
- Do not silently make major scope changes. Document decisions and their rationale.
- When the curriculum is ambiguous, note the ambiguity and propose a resolution for human review.
