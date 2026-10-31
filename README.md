# red-blue-lab

A progressive, story-driven, hands-on cybersecurity curriculum.

---

## What is this?

`red-blue-lab` is an executable learning journey through offensive and defensive security.

Each chapter asks you to build a real tool — a port scanner, an HTTP inspector, a packet parser, a crypto auditor — and use it to investigate, attack, and defend systems in a controlled lab environment. The tools evolve chapter by chapter, growing in capability and correctness as your knowledge grows.

This is not a collection of notes or a reading list. It is a curriculum designed around **doing**: reading specifications, writing implementations, running experiments, and verifying results.

---

## Who is this for?

Learners who want to:

- Understand how networks, protocols, and operating systems actually work.
- Build practical security tools from first principles.
- Think like both an attacker and a defender.
- Develop the habit of verifying claims with evidence rather than accepting them at face value.

Prior programming experience is assumed. Familiarity with Go is helpful but not required. No prior security background is needed.

---

## What will you build?

By the end of the curriculum, you will have built a personal toolkit of security tools, each capable of real investigative work:

| Tool | Capability |
|---|---|
| Byte Inspector | Inspect raw bytes, encodings, and representations |
| Network Diagnostic Tool | Diagnose local network configuration and connectivity |
| TCP Port Scanner | Identify open, closed, and uncertain ports with bounded concurrency |
| DNS Inspector | Query and compare DNS records across record types |
| Service Fingerprinter | Identify services by banner and protocol probe |
| HTTP Inspector | Examine requests, responses, headers, and redirects |
| HTTP Proxy | Intercept, log, and modify HTTP traffic |
| Web Security Header Scanner | Audit security headers and cookie attributes |
| Web Authorization Tester | Test authentication and authorization boundaries |
| Packet Inspector | Parse captured network packets and reconstruct streams |
| TLS Certificate Checker | Validate certificate chains, expiry, and configuration |
| System Diagnostics Tool | Inspect processes, file descriptors, and permissions |
| Fuzz Testing Tool | Generate malformed inputs and catch parser failures |
| Vulnerability Regression Harness | Reproduce bugs, verify fixes, and prevent regressions |
| Crypto Audit Tool | Detect cryptographic misuse and weak configurations |
| Security Event Detector | Parse logs, apply detection rules, and generate alerts |
| Incident Investigation Tool | Reconstruct timelines and produce structured incident reports |
| Red/Blue Assessment Toolkit | Integrate all tools in an authorized lab engagement |

All tools are implemented in **Go**, using the standard library wherever it teaches the mechanism directly.

---

## The Red/Blue Perspective

Every chapter is told through the work of two fictional engineers:

**Rayhan** is on the Red Team. He investigates services, discovers weaknesses, reproduces bugs in controlled environments, and maps attack paths.

**Samia** is on the Blue Team. She analyzes evidence, identifies suspicious behavior, builds detections, implements mitigations, and verifies that defenses hold.

Their work is not separate. Rayhan's findings motivate Samia's defenses. Samia's detections constrain what Rayhan can do unnoticed. The curriculum follows the full chain:

> Discover weakness → Reproduce it → Understand root cause → Implement defense → Test the defense → Verify the fix

---

## The Independent Challenge Model

Each chapter gives you:

- A technical explanation of the concepts you need.
- Diagrams, examples, and experiments that make the concepts concrete.
- A precise specification: inputs, outputs, behavior, constraints, edge cases, error handling, and acceptance criteria.

What it does **not** give you is the implementation.

You write the code. You verify it passes the acceptance criteria. You decide how to structure it.

When you need a nudge, hints are available. When you genuinely want to compare your approach, a reference implementation can be requested. But the primary path is independent: you read the spec, you build the tool, you verify the result.

---

## Incremental Tool Evolution

No chapter asks you to build a large, complete tool from nothing.

Each chapter begins where the last one left off. A scanner that opens one TCP connection in subchapter 1 gains range support in subchapter 2, proper timeout handling in subchapter 3, bounded concurrency in subchapter 4, and structured output in subchapter 5. Each milestone adds one meaningful capability, leaves you with a working and testable increment, and includes regression tests to ensure earlier behavior is preserved.

---

## Learning Philosophy

- **Just-in-time theory:** Concepts are introduced when you need them, not front-loaded.
- **Visual-first:** Diagrams, tables, and annotated examples take priority over prose.
- **Evidence over assumption:** You verify behavior with tests, not by reading that something should work.
- **Safety by default:** All exercises run against local test servers or authorized targets. The curriculum explains operational boundaries throughout.

---

## How to Navigate

Start at [**Chapter 00: Your First Security Lab**](chapters/00-your-first-security-lab/README.md). Each chapter lists its prerequisites explicitly. The curriculum is designed to be followed in order, but later chapters identify exactly which earlier tools and concepts they depend on.

**Curriculum overview:** [`docs/CURRICULUM.md`](docs/CURRICULUM.md)

**Content and authoring guidelines:** [`docs/CONTENT-GUIDELINES.md`](docs/CONTENT-GUIDELINES.md)

**Chapter content:** [`chapters/`](chapters/)

---

## License

Content and curriculum are for educational use. See `LICENSE` when added.
