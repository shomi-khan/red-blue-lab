# red-blue-lab Curriculum Blueprint

This document is the canonical source of truth for the `red-blue-lab` curriculum. Future chapter authors must read the relevant entries here before writing or modifying content.

**Last updated:** Foundation pass  
**Total chapters:** 19 (Chapter 00 through Chapter 18)  
**Language:** Go (standard library preferred; external dependencies introduced only when they provide clear educational or practical benefit)

---

## Table of Contents

- [Curriculum Overview](#curriculum-overview)
- [Phase 1: Understand the Building Blocks](#phase-1-understand-the-building-blocks)
  - [Chapter 00 — Your First Security Lab](#chapter-00--your-first-security-lab-set-up-the-learning-environment)
  - [Chapter 01 — Decode the Bytes](#chapter-01--decode-the-bytes-build-a-byte-inspector)
  - [Chapter 02 — See Your Network](#chapter-02--see-your-network-build-a-network-diagnostic-tool)
- [Phase 2: Discover What's Running on a Network](#phase-2-discover-whats-running-on-a-network)
  - [Chapter 03 — Who's Listening?](#chapter-03--whos-listening-build-a-tcp-port-scanner)
  - [Chapter 04 — Turn Names into Addresses](#chapter-04--turn-names-into-addresses-build-a-dns-inspector)
  - [Chapter 05 — Identify the Service](#chapter-05--identify-the-service-build-a-service-fingerprinter)
- [Phase 3: Understand and Inspect Web Traffic](#phase-3-understand-and-inspect-web-traffic)
  - [Chapter 06 — Read the Web's Conversation](#chapter-06--read-the-webs-conversation-build-an-http-inspector)
  - [Chapter 07 — See Through the Middle](#chapter-07--see-through-the-middle-build-an-http-proxy)
  - [Chapter 08 — Audit the Web Surface](#chapter-08--audit-the-web-surface-build-a-web-security-header-scanner)
  - [Chapter 09 — Test the Trust Boundary](#chapter-09--test-the-trust-boundary-build-a-web-authorization-tester)
- [Phase 4: Look Beneath the Surface](#phase-4-look-beneath-the-surface)
  - [Chapter 10 — Follow the Packets](#chapter-10--follow-the-packets-build-a-packet-inspector)
  - [Chapter 11 — Catch the Trust Failure](#chapter-11--catch-the-trust-failure-build-a-tls-certificate-checker)
  - [Chapter 12 — See Inside the Process](#chapter-12--see-inside-the-process-build-a-system-diagnostics-tool)
- [Phase 5: Find and Fix Weaknesses](#phase-5-find-and-fix-weaknesses)
  - [Chapter 13 — Break Your Own Parser](#chapter-13--break-your-own-parser-build-a-fuzz-testing-tool)
  - [Chapter 14 — Reproduce the Bug](#chapter-14--reproduce-the-bug-build-a-vulnerability-regression-harness)
  - [Chapter 15 — Spot the Cryptographic Mistake](#chapter-15--spot-the-cryptographic-mistake-build-a-crypto-audit-tool)
- [Phase 6: Detect, Investigate, Respond](#phase-6-detect-investigate-respond)
  - [Chapter 16 — Spot the Suspicious Pattern](#chapter-16--spot-the-suspicious-pattern-build-a-security-event-detector)
  - [Chapter 17 — Reconstruct the Incident](#chapter-17--reconstruct-the-incident-build-an-incident-investigation-tool)
- [Phase 7: Bring Everything Together](#phase-7-bring-everything-together)
  - [Chapter 18 — Run the Final Engagement](#chapter-18--run-the-final-engagement-build-a-redblue-security-assessment-toolkit)
- [Curriculum-Level Decisions](#curriculum-level-decisions)
- [Dependency Map](#dependency-map)

---

## Curriculum Overview

### Phase and Chapter Index

| Phase | Ch | Title | Primary Tool | Level |
|---|---|---|---|---|
| 1 | 00 | Your First Security Lab | Lab environment | — |
| 1 | 01 | Decode the Bytes | Byte Inspector | L2 |
| 1 | 02 | See Your Network | Network Diagnostic Tool | L1 |
| 2 | 03 | Who's Listening? | TCP Port Scanner | L2 |
| 2 | 04 | Turn Names into Addresses | DNS Inspector | L2 |
| 2 | 05 | Identify the Service | Service Fingerprinter | L2 |
| 3 | 06 | Read the Web's Conversation | HTTP Inspector | L2 |
| 3 | 07 | See Through the Middle | HTTP Proxy | L2 |
| 3 | 08 | Audit the Web Surface | Web Security Header Scanner | L2 |
| 3 | 09 | Test the Trust Boundary | Web Authorization Tester | L2 |
| 4 | 10 | Follow the Packets | Packet Inspector | L2 |
| 4 | 11 | Catch the Trust Failure | TLS Certificate Checker | L2 |
| 4 | 12 | See Inside the Process | System Diagnostics Tool | L2 |
| 5 | 13 | Break Your Own Parser | Fuzz Testing Tool | L2 |
| 5 | 14 | Reproduce the Bug | Vulnerability Regression Harness | L2 |
| 5 | 15 | Spot the Cryptographic Mistake | Crypto Audit Tool | L2 |
| 6 | 16 | Spot the Suspicious Pattern | Security Event Detector | L3 |
| 6 | 17 | Reconstruct the Incident | Incident Investigation Tool | L2 |
| 7 | 18 | Run the Final Engagement | Red/Blue Assessment Toolkit | L3 |

### Maturity Levels

| Level | Meaning |
|---|---|
| **L1: Learning tool** | Implements the core behavior with basic tests. Known limitations are documented but not required to be fixed. |
| **L2: Reliable tool** | Handles relevant failures, timeouts, malformed input, cancellation, and resource limits. Output is stable enough to rely on in later chapters. |
| **L3: Hardened tool** | Adds safe defaults, configuration validation, stable structured output, regression coverage, and CI verification. |

Passing tests alone does not prove production readiness at any level.

---

## Phase 1: Understand the Building Blocks

---

### Chapter 00 — Your First Security Lab: Set Up the Learning Environment

#### 8.1 Chapter Identity

- **Phase:** 1 — Understand the Building Blocks
- **Primary capability:** The learner can set up and verify a reproducible local security lab, understand how challenges are structured, and complete the workflow from reading a spec to verifying a result.
- **Primary deliverable:** A working Go environment with a minimal local test server the learner wrote themselves.
- **Intended level:** Absolute beginner in security; programming experience assumed.
- **Real-world relevance:** Security professionals work in controlled lab environments before touching production. Understanding the challenge-verify loop is fundamental to safe security testing.

#### 8.2 Learning Outcomes

By completing Chapter 00, the learner can:

1. Install and verify a working Go toolchain.
2. Create, compile, and run a Go program.
3. Write a minimal TCP listener and connect to it with a second program.
4. Explain what an authorized test environment means and why it matters.
5. Read a challenge specification and identify: objective, inputs, outputs, constraints, and acceptance criteria.
6. Describe the Red/Blue perspective and the role of Rayhan and Samia.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** None.
- **Required knowledge:** Basic familiarity with a terminal and a text editor.
- **Must not assume:** Any Go knowledge, any security background.
- **Downstream consumers:** Every subsequent chapter depends on a working Go environment and the challenge-verification habit established here.

#### 8.4 Subchapter Milestone Plan

**00.1 — Meet Rayhan and Samia: Understand the Lab and Its Rules**

- *Capability gained:* Understand the curriculum structure, the fictional framing, the Red/Blue model, and the independent challenge approach.
- *New theory:* Authorized vs. unauthorized testing. Controlled environment definition. Challenge spec anatomy.
- *Visualizations:* Diagram showing the learning cycle (Story → Visualize → Learn → Challenge → Verify → Debrief → Reuse).
- *Tool evolution:* No tool yet.
- *Challenge:* Read and annotate a sample challenge specification identifying each section.
- *Constraints:* No external network access during this exercise.
- *Acceptance criteria:* Learner can correctly label all sections of a sample spec.
- *Verification:* Self-check against provided labels.
- *Enables:* The discipline of reading specs before coding, which every later milestone requires.

**00.2 — First Lines: Install Go and Run Your First Program**

- *Capability gained:* Compile and run a Go program from the command line.
- *New theory:* Go workspace, `go run` vs `go build`, `fmt.Println`.
- *Visualizations:* Annotated terminal session showing `go version`, `go run main.go`, expected output.
- *Tool evolution:* Minimal `main.go` that prints a greeting.
- *Challenge:* Write a program that prints a structured greeting including the current time using `time.Now()`.
- *Constraints:* Must use only the standard library. Must compile without warnings.
- *Acceptance criteria:* Program compiles and runs; output includes a formatted timestamp.
- *Verification:* Run the binary, observe output.
- *Enables:* All subsequent Go implementation work.

**00.3 — Listen Up: Write a Minimal TCP Server**

- *Capability gained:* Write a program that accepts TCP connections and responds with a fixed message.
- *New theory:* `net.Listen`, `net.Accept`, `net.Conn`, goroutines for concurrency, deferred close.
- *Visualizations:* Sequence diagram: client connects → server accepts → server writes → client reads → connection closes.
- *Tool evolution:* TCP server that accepts one connection, writes a greeting line, and exits.
- *Challenge:* Extend the server to handle multiple sequential connections without restarting; print each client's remote address.
- *Constraints:* Listen only on loopback (`127.0.0.1`). Must close the connection cleanly.
- *Acceptance criteria:* Connecting twice with `telnet` or `nc` produces two separate greetings in the server log.
- *Verification:* Use `nc 127.0.0.1 <port>` to verify. Observe printed remote addresses.
- *Enables:* Local test server fixture pattern reused in Chapter 03, 06, and beyond.

**00.4 — Verify the Setup: Your First Connectivity Check**

- *Capability gained:* Write a TCP client that connects to the local server and reads the greeting.
- *New theory:* `net.Dial`, reading from a `net.Conn`, EOF handling.
- *Visualizations:* Same sequence diagram as 00.3 annotated with which code runs on which side.
- *Tool evolution:* Companion client program.
- *Challenge:* Client connects, reads until EOF, prints the received message and the round-trip wall-clock time.
- *Constraints:* Target must be `127.0.0.1` only. Must not hard-code a port — accept it as an argument.
- *Acceptance criteria:* Output shows the greeting and a duration in milliseconds.
- *Verification:* Run server, run client, observe matching output.
- *Enables:* The local test fixture pattern becomes the standard for every chapter that needs a controlled TCP server.

#### 8.5 Tool Lifecycle

- **Chapter 00 deliverables:** A minimal TCP server and client, each a standalone `main.go`.
- **Initial capability:** Accept connections on loopback, exchange a fixed message.
- **Planned evolution:** These specific programs are not extended. They establish the pattern.
- **Expected final scope:** Illustrative examples only. Not reused directly but the pattern (local listener → test client) recurs throughout.
- **Important error states:** Port already in use; connection refused; client read error.
- **Security invariants:** Listener bound only to loopback.
- **Testing expectations:** Manual verification by running both programs.
- **Maturity:** L1.

#### 8.6 Testing and Acceptance

- Manual verification is sufficient for Chapter 00.
- Automated tests are introduced progressively beginning in Chapter 01.
- The learner should verify connectivity manually: server logs a connection, client prints the received message.

#### 8.7 Red/Blue Learning

- Chapter 00 is primarily setup. The Red/Blue framing is introduced narratively.
- Rayhan and Samia are introduced: their roles, the kind of work they do, and why both perspectives are necessary.
- The concept of authorization and the safety of controlled environments is introduced from the Blue Team angle.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Learning cycle diagram | How each chapter is structured | 00.1 |
| TCP server sequence diagram | Client-server interaction model | 00.3 |
| Annotated terminal session | What a working Go environment looks like | 00.2 |

---

### Chapter 01 — Decode the Bytes: Build a Byte Inspector

#### 8.1 Chapter Identity

- **Phase:** 1 — Understand the Building Blocks
- **Primary capability:** The learner can read raw bytes from a file or stdin, display them in multiple representations, and reason about encoding, offset, and length.
- **Primary tool:** **Byte Inspector** — a command-line tool that takes input (file path or stdin) and displays bytes as hex, decimal, binary, and ASCII interpretations.
- **Intended level:** Beginner.
- **Real-world relevance:** Security engineers inspect raw bytes constantly — packet captures, binary protocols, file format exploits, shellcode analysis. Understanding bytes at this level is foundational to everything else in the curriculum.

#### 8.2 Learning Outcomes

By completing Chapter 01, the learner can:

1. Convert between binary, decimal, and hexadecimal representations correctly.
2. Explain what a byte slice (`[]byte`) is in Go and how to index, slice, and iterate it.
3. Describe the difference between raw bytes and a text interpretation.
4. Explain why the same byte sequence means different things under different encodings.
5. Read a file as raw bytes and display subsets at specified offsets.
6. Recognize valid UTF-8 sequences and explain what makes a byte sequence invalid UTF-8.
7. Accept input from a file argument or stdin interchangeably.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 00 (Go environment, basic I/O).
- **Required knowledge:** Basic Go syntax, `os.Open`, `fmt.Printf`.
- **Must not assume:** Any knowledge of network protocols or security.
- **Concepts that must be established before this chapter:** None beyond Chapter 00.
- **Downstream consumers:** Every subsequent chapter benefits from byte-level intuition. Chapter 10 (Packet Inspector) relies on byte-level header parsing. Chapter 14 (Fuzz Testing) manipulates byte sequences directly.

#### 8.4 Subchapter Milestone Plan

**01.1 — Read and Display: Bytes Are Just Numbers**

- *Capability gained:* Read a file as `[]byte`, print each byte as a decimal number.
- *New theory:* Bits and bytes. The byte as the fundamental unit. `os.ReadFile`. Byte literals and integer types in Go. The `%d` and `%08b` verbs.
- *Visualizations:* Table mapping a byte value to its binary, decimal, and hex form for values 0x00–0x0F. Figure showing a file as a sequence of numbered cells.
- *Tool evolution:* Accept a filename argument, read the file, print one byte per line with its decimal value and index.
- *Challenge:* Print each byte with its zero-based index, decimal value, and 8-bit binary representation.
- *Constraints:* Handle the case where the file does not exist (print an error, exit non-zero). Maximum file size for this milestone: 1 MiB.
- *Acceptance criteria:* For a known test file, the printed values match hand-computed expectations. Empty file produces no output lines (zero bytes read).
- *Verification:* Create a small binary test file using Go's `os.WriteFile`. Verify output matches known byte values.
- *Enables:* 01.2.

**01.2 — Hexdump: The Classic View**

- *Capability gained:* Display bytes in the familiar hex dump layout: offset | hex columns | ASCII column.
- *New theory:* Hexadecimal notation and its convenience. Why security tools use hex. Printable vs. non-printable ASCII characters. The `%02x` format verb.
- *Visualizations:* Annotated hex dump showing each column's meaning. Table of ASCII characters 0x20–0x7E.
- *Tool evolution:* Add `--hex` flag; output groups bytes in rows of 16 with offset, two-digit hex values, and a printable-ASCII sidebar.
- *Challenge:* Format the output so rows align correctly regardless of file size. Represent non-printable bytes as `.` in the ASCII column.
- *Constraints:* 16 bytes per row. Offset column is 8 hex digits wide, zero-padded. Output must be readable in a fixed-width terminal.
- *Acceptance criteria:* Output matches the format of `xxd` or `hexdump -C` for a known file (verified manually).
- *Verification:* Compare output against `xxd` on a small test file if available on the platform; otherwise verify against hand-computed expected output.
- *Enables:* 01.3.

**01.3 — Navigate: Inspect Ranges by Offset and Length**

- *Capability gained:* Accept `--offset` and `--length` flags to display a specific byte range.
- *New theory:* Slicing byte arrays. Zero-based indexing. Out-of-bounds handling. Why ranges matter for protocol inspection (headers start at a known offset).
- *Visualizations:* Figure annotating a byte array with an offset pointer and a length span, showing what the slice expression captures.
- *Tool evolution:* Add `--offset N` and `--length N` flags. Validate that offset < file length and that offset+length does not exceed file length.
- *Challenge:* Display only the specified range in the selected format. If offset is beyond the file, print a clear error and exit non-zero.
- *Constraints:* Offset and length must be non-negative integers. Length=0 must display zero bytes (no output lines), not an error.
- *Acceptance criteria:* For a known file, `--offset 4 --length 8` displays exactly the correct 8 bytes starting at byte index 4.
- *Verification:* Test with a file of known content. Add a Go test that writes a deterministic file and verifies the slice output.
- *Enables:* 01.4, and later Chapter 10 (Packet Inspector uses offset-based parsing).

**01.4 — Interpret: Decode as Text Encodings**

- *Capability gained:* Attempt to decode a byte range as ASCII and UTF-8, and report which bytes are invalid under each encoding.
- *New theory:* ASCII as 7-bit encoding. UTF-8 as variable-length encoding of Unicode code points. The `utf8` package in Go. What makes a byte sequence invalid UTF-8. The difference between a byte and a character.
- *Visualizations:* Figure showing a multi-byte UTF-8 sequence with bit-level annotation. Table: byte value range → UTF-8 role (leading byte, continuation byte, invalid).
- *Tool evolution:* Add `--decode ascii` and `--decode utf8` flags. For each byte or sequence, label it as valid, non-printable, or invalid under the chosen encoding.
- *Challenge:* For `--decode utf8`, identify and mark each invalid byte with a `[invalid]` annotation. For `--decode ascii`, mark bytes > 0x7F as `[non-ASCII]`.
- *Constraints:* Do not attempt to "fix" or skip invalid bytes — display them alongside the annotation. The learner must not use any third-party encoding library.
- *Acceptance criteria:* A file containing a valid UTF-8 emoji followed by a lone continuation byte produces correct annotations for each sequence.
- *Verification:* Write a Go test that embeds the test byte sequence and checks annotations.
- *Enables:* 01.5. Also informs Chapter 13 (Fuzz Testing) where malformed byte sequences are intentionally generated.

**01.5 — Compose: Accept Stdin and Multiple Formats**

- *Capability gained:* The Byte Inspector accepts input from a file path argument or from stdin (via pipe), and supports multiple output formats selectable by flag.
- *New theory:* `os.Stdin` as an `io.Reader`. `io.ReadAll`. Flag parsing with `flag` package. Output format selection.
- *Tool evolution:* Unify input: if no filename argument, read stdin. Add `--format` flag accepting `hex`, `decimal`, `binary`, `utf8`, `ascii`.
- *Challenge:* Support all input sources and all output formats in a single binary. Print usage if called incorrectly.
- *Constraints:* When reading stdin, size is unknown in advance; do not require full buffer before starting output for large inputs. Cap at 10 MiB before producing an error.
- *Acceptance criteria:* `echo "hello" | byteinspect --format hex` produces the correct hex dump. `byteinspect --format binary myfile.bin` works identically to direct invocation.
- *Verification:* Go test that forks the binary (or calls the core logic as a function) with both input modes.
- *Enables:* The complete Byte Inspector. Later chapters use byte inspection concepts; the binary itself is useful as a debugging aid throughout.

#### 8.5 Tool Lifecycle

- **Tool name:** `byteinspect`
- **Initial capability (01.1):** Read a file, print bytes as decimal with index.
- **Final scope:** Read file or stdin; display bytes in hex, decimal, binary; support offset/length ranges; decode as ASCII or UTF-8 with invalid-byte annotation; selectable output format.
- **Core behavior:** Deterministic byte-for-byte display. No external I/O side effects.
- **Important error states:** File not found; offset out of bounds; length exceeds remaining bytes; stdin read error; file exceeds size cap; unsupported format flag.
- **Security invariants:** Does not write to any file. Does not execute or interpret content.
- **Testing expectations:** Unit tests for each format and edge case; integration test against known binary files; test for invalid UTF-8 annotation.
- **Downstream consumers:** Used as a debugging aid throughout the curriculum. Chapter 10 (Packet Inspector) develops similar byte-parsing patterns. Chapter 13 (Fuzz Testing) generates byte sequences that `byteinspect` can display.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Each milestone introduces at least one Go test using deterministic input.
- Tests must cover: empty input, single byte, exactly 16 bytes (one hex row), 17 bytes (two rows, second incomplete), invalid UTF-8, non-printable ASCII, valid multi-byte UTF-8.
- Regression tests from earlier milestones must remain green as new flags are added.
- No network access required. All tests use in-process byte slices or temporary files.

#### 8.7 Red/Blue Learning

- **Red Team:** Byte-level inspection is the foundation of binary protocol analysis, shellcode reading, and understanding how parsers handle unexpected input.
- **Blue Team:** Understanding byte representations is required for log analysis, forensic artifact inspection, and recognizing encoded payloads in security events.
- **Connection:** Chapter 10 (Packet Inspector) will return to byte-level parsing at the packet layer. Chapter 13 (Fuzz Testing) will use byte mutation. Chapter 15 (Crypto Audit) will inspect raw key material.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Byte representation table (binary/decimal/hex) | Base conversion | 01.1 |
| Hex dump anatomy figure | What each column means | 01.2 |
| Byte-slice offset/length figure | Range navigation | 01.3 |
| UTF-8 bit-level sequence figure | Why encoding matters | 01.4 |

---

### Chapter 02 — See Your Network: Build a Network Diagnostic Tool

#### 8.1 Chapter Identity

- **Phase:** 1 — Understand the Building Blocks
- **Primary capability:** The learner can inspect local network configuration, interpret IP addresses, and test TCP connectivity.
- **Primary tool:** **netdiag** — a command-line diagnostic tool reporting interface addresses, IP address classifications, and basic connectivity results.
- **Intended level:** Beginner to intermediate.
- **Real-world relevance:** Network diagnostic skills are the first thing a security engineer uses when a connection fails or behaves unexpectedly. Knowing what is reachable and from where is a prerequisite for all scanning and inspection work.

#### 8.2 Learning Outcomes

By completing Chapter 02, the learner can:

1. Explain IPv4 and IPv6 address notation and what each part represents.
2. Explain subnets and CIDR notation (e.g., `192.168.1.0/24`).
3. List the network interfaces on the local machine using Go.
4. Distinguish loopback, private, and public address ranges.
5. Explain what a port is and why the combination of address and port identifies a specific service.
6. Distinguish TCP from UDP at a conceptual level.
7. Attempt a TCP connection to a specified host:port and report whether it succeeded, was refused, or timed out.
8. Explain why a timeout and a refused connection are different kinds of evidence about a port's state.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 00 (Go environment), Chapter 01 (byte representation; helps with IP address bytes).
- **Required knowledge:** Chapter 00 Go basics.
- **Downstream consumers:** Chapter 03 (Port Scanner) directly extends the TCP connectivity test developed here. Chapter 04 (DNS) builds on IP address understanding. All network tool chapters assume this foundation.

#### 8.4 Subchapter Milestone Plan

**02.1 — Local Map: List Network Interfaces and Addresses**

- *Capability gained:* List all network interfaces on the local machine with their addresses.
- *New theory:* `net.Interfaces()`. Interface flags (up, loopback, multicast). IPv4 vs. IPv6. Loopback (`127.0.0.1`, `::1`). Link-local addresses. Private address ranges (RFC 1918).
- *Visualizations:* Table of address ranges: loopback, link-local, RFC 1918 private, public. Diagram of a machine with multiple interfaces (loopback + Ethernet + Wi-Fi).
- *Tool evolution:* Print each interface: name, flags, and all assigned addresses with their CIDR prefix.
- *Challenge:* For each address, label it as loopback, link-local, private, or public. Suppress interfaces with no assigned addresses unless `--all` flag is given.
- *Constraints:* IPv4 and IPv6 addresses both supported. No external network calls.
- *Acceptance criteria:* Loopback interface appears with correct address labels. At least one non-loopback interface appears on a typical workstation.
- *Verification:* Compare against `ip addr` or `ifconfig` output manually.
- *Enables:* 02.2.

**02.2 — The Address Decoded: Parse and Explain IP Addresses**

- *Capability gained:* Accept an IP address argument and explain its components and classification.
- *New theory:* `net.ParseIP`. Network address vs. host address within a CIDR block. Broadcast address (IPv4). Why IPv6 uses slash notation differently. Subnet mask arithmetic (conceptual, not required for implementation).
- *Visualizations:* Figure annotating an IPv4 address: four octets, CIDR prefix, network portion vs. host portion. Table comparing IPv4 and IPv6 address lengths.
- *Tool evolution:* Add `netdiag explain <address>` subcommand.
- *Challenge:* Given an IP address (with or without prefix), print: version (IPv4/IPv6), classification, network address (if CIDR given), and number of host addresses in the range (if CIDR given, IPv4 only).
- *Constraints:* Invalid addresses must produce a clear error. Do not assume `/32` if no prefix is given — report that no network range was specified.
- *Acceptance criteria:* `netdiag explain 10.0.1.5/24` outputs IPv4, private, network `10.0.1.0`, 254 usable host addresses.
- *Verification:* Go test with a set of known inputs and expected outputs.
- *Enables:* 02.3.

**02.3 — Connect or Not?: Test TCP Connectivity**

- *Capability gained:* Attempt a TCP connection to a given host:port and report the outcome: connected, refused, or timed out.
- *New theory:* `net.DialTimeout`. TCP three-way handshake (conceptual). `RST` as a refused signal. The difference between a timeout and a refusal as evidence. Operating system connection queues.
- *Visualizations:* Sequence diagram: successful connect (SYN → SYN-ACK → ACK). Refused connect (SYN → RST). Timed-out connect (SYN → silence → timeout). Table: outcome → what it likely means about the port/host state.
- *Tool evolution:* Add `netdiag connect <host:port>` subcommand with a configurable `--timeout` flag (default 3s).
- *Challenge:* Report `connected`, `refused`, or `timeout` as distinct outcomes. If the operating system explicitly reports that the network or route is unreachable, report that separately rather than mislabeling it as a timeout. Print the round-trip time for a successful connection. On success, close the connection cleanly.
- *Constraints:* Must close the connection after reporting. Do not leave connections open. Timeout must be enforced — a 3-second timeout must not block for 30 seconds.
- *Acceptance criteria:* Connecting to a local listener returns `connected`; connecting to a closed loopback port returns `refused`; and a controlled dialer that returns a timeout error is classified as `timeout`. An explicit network-unreachable error must remain distinct from a timeout. Tests must not depend on a non-routable address, external network access, or the host machine's routing configuration.
- *Verification:* Use the Chapter 00 local-server pattern to test `connected` and `refused`. Make the dial operation injectable through a small function or interface so a unit test can deterministically supply a timeout error and verify `timeout` classification. Add a separate test for an explicit network-unreachable error. Keep integration tests loopback-only.
- *Enables:* Chapter 03 (Port Scanner) directly extends this single-connection test to a range of ports.

**02.4 — The Diagnostic Report: Assemble All Findings**

- *Capability gained:* The tool produces a structured human-readable diagnostic report combining interface info, address analysis, and connectivity test results.
- *New theory:* Organizing multi-section CLI output. Exit codes and their conventions. When to write to stderr vs. stdout.
- *Tool evolution:* Add `netdiag report <host:port>` subcommand. Run 02.1 (interfaces), 02.2 (classify the target address), and 02.3 (connectivity test) and format results as a coherent report.
- *Challenge:* The report must be structured in clearly labeled sections. Connectivity failure must not prevent the report from completing — report what succeeded, explain what failed, exit non-zero only if a fatal error occurred.
- *Constraints:* No interactive prompts. Accept all options as flags. Timeout configurable.
- *Acceptance criteria:* `netdiag report 127.0.0.1:8080` produces a report with at least three sections: local interfaces, target address classification, and connectivity result.
- *Verification:* Integration test that runs the binary with a local server and verifies the report structure.
- *Enables:* The diagnostic report pattern recurs in Chapter 05 (Service Fingerprinter), Chapter 08 (Web Security Header Scanner), and Chapter 11 (TLS Certificate Checker).

#### 8.5 Tool Lifecycle

- **Tool name:** `netdiag`
- **Initial capability (02.1):** List local interfaces and addresses.
- **Final scope:** List interfaces; explain IP addresses and CIDR ranges; test TCP connectivity with outcome classification; produce a structured diagnostic report.
- **Core behavior:** Read-only. Does not modify system configuration.
- **Important error states:** Invalid IP address; invalid host:port; timeout; DNS resolution failure (when hostname is given); permission errors on interface enumeration.
- **Security invariants:** No persistent connections. Closes all connections after reporting. Loopback-only testing in automated tests.
- **Testing expectations:** Unit tests for address classification and CIDR math; integration tests using local listeners.
- **Downstream consumers:** Chapter 03 extends the TCP connectivity check. Chapter 05 uses the address-classification logic.
- **Maturity target:** L1 (reliable enough for learning; full hardening not required).

#### 8.6 Testing and Acceptance

- At minimum: unit tests for address classification (loopback, private, public, link-local) and deterministic outcome classification using a controlled dialer. Integration tests must use local listeners for connected/refused cases. Verify timeout enforcement with a controlled delay or injected dialer, not a non-routable address or external network.
- The "refused" test is platform-sensitive: ensure the listener is closed before attempting the connection. Network-unreachable errors vary by operating system, so test the classification with a controlled error rather than relying on the host network.

#### 8.7 Red/Blue Learning

- **Red Team:** Network diagnostic skills are the foundation of reconnaissance. Understanding what is reachable and from where helps map attack surfaces before active scanning.
- **Blue Team:** The same tools that show connectivity to a legitimate service also reveal unexpected open ports or reachable endpoints. Samia uses network diagnostics to verify that a service is only reachable from expected networks.
- **Connection:** The distinction between `timeout` and `refused` learned here becomes critical in Chapter 03 (Port Scanner), where Rayhan must report scan results honestly.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| IPv4 address anatomy figure | Octets, network vs. host portion | 02.2 |
| RFC 1918 address table | Private/loopback/public ranges | 02.1 |
| TCP connection outcome sequence diagrams (×3) | Connected, refused, timed out | 02.3 |
| Interface and addressing topology diagram | Local machine networking model | 02.1 |

---

## Phase 2: Discover What's Running on a Network

---

### Chapter 03 — Who's Listening?: Build a TCP Port Scanner

#### 8.1 Chapter Identity

- **Phase:** 2 — Discover What's Running on a Network
- **Primary capability:** The learner can scan a range of TCP ports on a target host, correctly distinguish open, closed, and uncertain results, and control scan resource usage.
- **Primary tool:** **portscan** — a TCP port scanner with bounded concurrency, timeouts, and honest result classification.
- **Intended level:** Beginner to intermediate.
- **Real-world relevance:** Port scanning is one of the most fundamental reconnaissance activities. Understanding what services are exposed on a network, and what the absence of a response means, is the starting point for any security assessment.

#### 8.2 Learning Outcomes

By completing Chapter 03, the learner can:

1. Explain the TCP three-way handshake at a packet-level conceptual model.
2. Explain why a refused connection (RST) and a timed-out connection are different kinds of evidence about a port.
3. Implement a TCP port scanner that correctly classifies results as `open`, `closed`, or `unknown`.
4. Apply bounded concurrency using a worker pool pattern in Go.
5. Enforce per-connection timeouts and explain why they are mandatory.
6. Use context cancellation to stop an in-progress scan.
7. Test port scanner behavior against deterministic local listeners.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 00 (TCP listener pattern), Chapter 02 (TCP connectivity, outcome classification).
- **Required knowledge:** `net.DialTimeout`, goroutines, channels.
- **Downstream consumers:** Chapter 05 (Service Fingerprinter) takes port scanner output as a starting point. Chapter 18 (Final Engagement) reuses the port scanner as part of the reconnaissance workflow.
- **Hard prerequisite check:** The distinction between `timeout` and `refused` must be established in Chapter 02 before this chapter is authored.

#### 8.4 Subchapter Milestone Plan

**03.1 — One at a Time: Scan a Single Port**

- *Capability gained:* Scan a single TCP port on a given host, report `open`, `closed`, or `unknown`.
- *New theory:* TCP handshake steps. RST as an explicit refusal. Timeout as ambiguous (firewall drop, host unreachable, or slow). Why "not open" is not the same as "closed."
- *Visualizations:* Three sequence diagrams: open port (SYN→SYN-ACK→ACK→close), closed port (SYN→RST), filtered port (SYN→silence). Table: observed outcome → classification → what it means.
- *Tool evolution:* `portscan <host> <port>` prints the classification and exits.
- *Challenge:* Classify based on error type: nil error = open; connection refused = closed; deadline exceeded or other network error = unknown.
- *Constraints:* Default timeout: 2 seconds. Must close open connections after classification.
- *Acceptance criteria:* Against a local listener: port reports `open`. After listener closes: port reports `closed`. Against a non-routable address with short timeout: reports `unknown`.
- *Verification:* Go test using local TCP listener for all three cases.
- *Enables:* 03.2.

**03.2 — More Ports: Scan a Range Sequentially**

- *Capability gained:* Accept a port range (e.g., `1-1024`) and scan all ports sequentially, printing results as they complete.
- *New theory:* Iterating over port ranges. How port numbers are assigned (well-known ports 0–1023, registered 1024–49151, dynamic/ephemeral).
- *Visualizations:* Table: well-known port ranges and their purpose. Diagram showing sequential scan timeline.
- *Tool evolution:* Add `--ports 1-1024` flag. Iterate and print each result.
- *Challenge:* Print results in a consistent format: `<port> <state>`. Support single port, range, and comma-separated list.
- *Constraints:* No concurrency yet. Maximum range: 65535 ports. Invalid ranges (e.g., `70000`, `100-50`) must produce a clear error.
- *Acceptance criteria:* Scanning ports 8080-8082 with two local listeners on 8080 and 8082 produces correct classifications for all three ports.
- *Verification:* Go test spinning up two listeners on known ports.
- *Enables:* 03.3.

**03.3 — Not Every Silence Is a No: Handle Timeouts Properly**

- *Capability gained:* Correctly distinguish timeout from other errors in all cases; make the timeout configurable.
- *New theory:* How to inspect `net.Error` and `os.IsTimeout`. Context deadline exceeded vs. connection refused at the syscall level. Why timeout classification requires care.
- *Visualizations:* Flowchart: "How to classify a dial error" — nil → open; OpError with refused syscall → closed; timeout/deadline → unknown; other → unknown with error note.
- *Tool evolution:* Add `--timeout` flag. Improve error classification using `net.Error` inspection.
- *Challenge:* Write a function `classify(err error) PortState` that correctly handles all three cases plus unexpected errors. The function must be independently testable.
- *Constraints:* The classify function must not call the network. It must be unit-testable with mock errors.
- *Acceptance criteria:* Unit tests verify each error type maps to the correct classification.
- *Verification:* Unit tests. Integration test with a firewall-simulated drop is acceptable using a port that deliberately drops connections (if available in the lab) or by timing.
- *Enables:* 03.4.

**03.4 — Speed Up Safely: Bounded Concurrency**

- *Capability gained:* Scan multiple ports concurrently using a worker pool; control the degree of concurrency with `--workers N`.
- *New theory:* Goroutines and channels. Worker pool pattern: N workers reading from a work channel, writing to a results channel. Why unbounded concurrency is dangerous (file descriptor exhaustion, network flooding). Default safe values.
- *Visualizations:* Diagram: work channel → N workers → results channel → collector. Timeline comparison: sequential vs. concurrent scan duration.
- *Tool evolution:* Replace sequential loop with a worker pool. Default to 100 concurrent workers.
- *Challenge:* Implement a worker pool that: fans out ports to workers, collects results in order, shuts down cleanly when all ports are scanned.
- *Constraints:* Workers: default 100, max 1000. Resource cleanup: all goroutines must exit before the program returns. No goroutine leaks.
- *Acceptance criteria:* Scanning 1000 ports with 100 workers is significantly faster than sequential. All results are present and no goroutines remain active after scan completes (verifiable with `-race`).
- *Verification:* Benchmark test. `-race` flag during test run.
- *Enables:* 03.5.

**03.5 — Cancel Cleanly: Context and Cancellation**

- *Capability gained:* Support scan cancellation via OS signal (Ctrl-C) using `context.WithCancel`; workers stop and resources are released.
- *New theory:* `context.Context`. `signal.NotifyContext`. Passing context to `net.DialContext`. Cooperative cancellation.
- *Visualizations:* Diagram: signal → cancel context → workers observe Done → workers exit → channel closes → collector exits.
- *Tool evolution:* Thread context through the worker pool. Handle `SIGINT` for clean shutdown.
- *Challenge:* When Ctrl-C is received mid-scan, the tool prints a "scan interrupted" message, reports partial results, and exits cleanly without panicking or leaving connections open.
- *Constraints:* Must not panic on cancellation. Must print partial results.
- *Acceptance criteria:* In a test, cancelling the context mid-scan results in partial results and no goroutine leaks.
- *Verification:* Go test that cancels the context after a fixed number of results.
- *Enables:* 03.6.

**03.6 — Trust the Results: Structured Output and Tests**

- *Capability gained:* The scanner produces structured output (JSON and human-readable) and has a comprehensive test suite including regression tests.
- *New theory:* `encoding/json`. Output design: what information belongs in a scan result. Regression testing as a discipline.
- *Tool evolution:* Add `--output json` flag. Define a `ScanResult` struct with host, port, state, duration, and timestamp.
- *Challenge:* Print one JSON object per line (NDJSON) when `--output json` is selected. Human-readable mode groups results by state.
- *Constraints:* Output format must not change between calls given the same input. JSON must be valid (verifiable with `jq`).
- *Acceptance criteria:* `--output json | jq .state` produces only `"open"`, `"closed"`, or `"unknown"` values.
- *Verification:* Full regression test suite. All previously passing tests must still pass.
- *Enables:* Chapter 05 (Service Fingerprinter) takes `portscan` output as input to identify services on open ports.

#### 8.5 Tool Lifecycle

- **Tool name:** `portscan`
- **Initial capability:** Scan one port, classify the result.
- **Final scope:** Scan a range of ports with bounded concurrency, timeouts, context cancellation, and structured (JSON or human-readable) output.
- **Core behavior:** Attempt TCP connections; classify results honestly; close all connections; exit cleanly.
- **Important error states:** Invalid host; DNS resolution failure; all ports timeout (possible network issue or firewall); port range validation errors.
- **Security invariants:** Default timeout enforced. Default worker count safe for loopback. Users must explicitly set high worker counts. Tool must not be used against hosts without authorization (documented in the chapter).
- **Output contract:** Each result has exactly one of three states: `open`, `closed`, `unknown`. The `unknown` state is never omitted in favor of a boolean.
- **Testing expectations:** Unit test for error classification. Integration test with local listeners. Goroutine leak test with `-race`. Partial cancellation test.
- **Downstream consumers:** Chapter 05 (Service Fingerprinter) takes open port list as input. Chapter 18 (Final Engagement) reuses as reconnaissance step.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Unit: `classify(err)` for all error types.
- Integration: three listener scenarios (open/closed/timeout).
- Concurrency: goroutine leak check using `-race` and a test that waits for all goroutines.
- Cancellation: mid-scan context cancel.
- Regression: all tests from 03.1–03.5 must still pass after 03.6.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses the port scanner to identify exposed services on a target host in the lab. Interprets `unknown` results as potentially filtered ports worth investigating further. Documents findings for the service fingerprinter.
- **Blue Team (Samia):** Reviews the port scanner output as the kind of evidence an attacker would gather. Verifies that only expected ports are open. Builds a detection rule (in Chapter 16) for port scan patterns in firewall logs.
- **Connection:** Open port findings from `portscan` feed directly into `svcfinger` (Chapter 05) and `httpinspect` (Chapter 06). Samia's work in Chapter 16 includes detecting port-scan signatures.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Three TCP outcome sequence diagrams | open/closed/unknown states | 03.1 |
| Error classification flowchart | How to inspect a dial error | 03.3 |
| Worker pool diagram | Bounded concurrency pattern | 03.4 |
| Cancellation signal flow diagram | Context propagation | 03.5 |
| Port number range table | Well-known vs. registered vs. dynamic | 03.2 |

---

### Chapter 04 — Turn Names into Addresses: Build a DNS Inspector

#### 8.1 Chapter Identity

- **Phase:** 2 — Discover What's Running on a Network
- **Primary capability:** The learner can query DNS records of multiple types, interpret responses, and compare results across resolvers.
- **Primary tool:** **dnsinspect** — a DNS inspector that queries A, AAAA, MX, TXT, CNAME, and NS records, displays TTL values, and can compare responses between resolvers.
- **Intended level:** Beginner to intermediate.
- **Real-world relevance:** DNS is the naming infrastructure of the internet. Security engineers use DNS inspection to map infrastructure, discover shadow IT, identify cloud provider exposures, find email security misconfigurations, and detect DNS hijacking.

#### 8.2 Learning Outcomes

By completing Chapter 04, the learner can:

1. Explain the DNS resolution chain: stub resolver → recursive resolver → authoritative server.
2. Look up A, AAAA, MX, TXT, CNAME, and NS records using Go's `net` package.
3. Explain what TTL means and why it matters for caching and security.
4. Distinguish NXDOMAIN from SERVFAIL and explain what each indicates.
5. Compare responses from two different resolvers and identify discrepancies.
6. Explain why DNS results can vary by resolver and what that implies for security.
7. Handle DNS resolution failures and timeouts gracefully.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 00, Chapter 02 (IP addresses and network model).
- **Downstream consumers:** Chapter 06 (HTTP Inspector) uses hostnames; DNS context helps explain why `http.Get("https://example.com")` works. Chapter 08 (Web Security Header Scanner) may query DNS for SPF/DKIM TXT records. Chapter 18 (Final Engagement) includes DNS reconnaissance.

#### 8.4 Subchapter Milestone Plan

**04.1 — What's the Address?: Resolve a Hostname to IP**

- *Capability gained:* Resolve a hostname to its IP address(es) using Go's standard library.
- *New theory:* How stub resolvers work. `net.LookupHost` and `net.LookupIP`. The A record (IPv4) and AAAA record (IPv6). Multiple results for a single hostname (load balancing, anycast).
- *Visualizations:* Sequence diagram: application → stub resolver → recursive resolver → authoritative server → response. Table: record type → what it returns.
- *Tool evolution:* `dnsinspect <hostname>` prints all resolved IP addresses.
- *Challenge:* Print each resolved address with its record type (A or AAAA). Sort results by record type, then address.
- *Constraints:* Must handle hostnames that resolve to no addresses without panicking. Timeout: 5 seconds.
- *Acceptance criteria:* `dnsinspect localhost` returns `127.0.0.1` (and `::1` on dual-stack systems). A non-existent hostname returns a clear error.
- *Verification:* Test using a local resolver mock or known stable hostname (e.g., `localhost`).
- *Enables:* 04.2.

**04.2 — More Than Just Addresses: Query Specific Record Types**

- *Capability gained:* Query MX, TXT, CNAME, and NS records by type.
- *New theory:* `net.LookupMX`, `net.LookupTXT`, `net.LookupCNAME`, `net.LookupNS`. MX records and mail routing. TXT records and their security uses (SPF, DKIM, DMARC). CNAME chains and their implications.
- *Visualizations:* Table: record type → purpose → security relevance. Example SPF TXT record annotated.
- *Tool evolution:* Add `--type` flag accepting `A`, `AAAA`, `MX`, `TXT`, `CNAME`, `NS`, `all`.
- *Challenge:* Query the specified record type and display each record's value. For MX, include preference (priority). For TXT, display the full string. For CNAME, show the canonical target.
- *Constraints:* Unsupported record type must produce a helpful error listing supported types.
- *Acceptance criteria:* Querying TXT records for a domain with a known SPF record produces the correct string.
- *Verification:* Using a local `hosts` file or test DNS server (e.g., `github.com/miekg/dns` test server) for deterministic tests. Acceptable to note that live DNS tests are non-deterministic.
- *Enables:* 04.3.

**04.3 — How Long Is It Cached?: Inspect TTL Values**

- *Capability gained:* Display TTL values alongside records; explain what low and high TTL values mean for security.
- *New theory:* TTL as a caching directive. Low TTL → frequent updates, faster failover, possible evasion. High TTL → long caching, difficult to change quickly. Go's standard `net` package does not expose TTL directly — introduce `net.Resolver` and the use of a raw DNS library for TTL access.
- *Visualizations:* Timeline diagram: record change → TTL expiry across caching resolvers. Table: TTL range → typical use → security implication.
- *Tool evolution:* Add TTL display. Introduce dependency on `github.com/miekg/dns` for raw DNS access (first external dependency in the curriculum — explain the decision).
- *Challenge:* Display TTL alongside each record. Warn when TTL is less than 60 seconds (possible evasion or attack preparation indicator).
- *Constraints:* Go standard library does not expose TTL from `net.LookupX`. The chapter must explain why an external library is introduced for this specific purpose and what it provides.
- *Acceptance criteria:* TTL is printed for each record. Short-TTL warning appears when appropriate.
- *Verification:* Test using a local DNS server that returns controlled TTL values.
- *Enables:* 04.4.

**04.4 — Does Everyone Agree?: Compare Resolver Responses**

- *Capability gained:* Query two different resolvers for the same record and report differences.
- *New theory:* Recursive vs. authoritative resolvers. Why responses can differ (split-horizon DNS, cache poisoning, anycast differences). How resolver comparison can reveal infrastructure anomalies.
- *Visualizations:* Diagram: same query sent to two resolvers, different response paths, possible divergent results. Table: divergence types → possible explanations.
- *Tool evolution:* Add `--resolver <ip:port>` flag. When two resolvers are specified, display responses side by side and flag differences.
- *Challenge:* Compare A and AAAA records from two resolvers. Report: records only in resolver 1, records only in resolver 2, TTL differences. Exit with a non-zero code if any difference is found.
- *Constraints:* Default resolver is the system resolver. Custom resolver specified by IP:port (e.g., `8.8.8.8:53`).
- *Acceptance criteria:* Querying the same record against a local test DNS server that returns a different IP than the system resolver correctly reports the discrepancy.
- *Verification:* Two local DNS test servers returning different answers.
- *Enables:* 04.5.

**04.5 — Handle the Failures: NXDOMAIN, SERVFAIL, and Timeouts**

- *Capability gained:* Classify DNS errors correctly: NXDOMAIN, SERVFAIL, timeout, and network error.
- *New theory:* DNS response codes (RCODE): NOERROR, NXDOMAIN, SERVFAIL, REFUSED. What each indicates about the DNS infrastructure. Retry behavior and when it is appropriate. Exponential backoff (conceptual).
- *Visualizations:* Table: RCODE → meaning → appropriate response in the tool. Flowchart for error classification.
- *Tool evolution:* Improve error classification. For each DNS error, print a human-readable explanation of what the error likely indicates.
- *Challenge:* Correctly classify all four error types. For SERVFAIL, suggest that the learner try a different resolver. For NXDOMAIN, confirm the domain does not exist (not just unreachable).
- *Constraints:* Must not retry indefinitely. One retry on SERVFAIL is acceptable; NXDOMAIN is definitive.
- *Acceptance criteria:* A query against a local DNS test server that returns NXDOMAIN produces the correct classification and explanation. Same for SERVFAIL.
- *Verification:* Local test DNS server returning controlled response codes.
- *Enables:* Chapter 06 (HTTP Inspector) benefits from DNS understanding when inspecting redirect chains that involve hostname changes.

#### 8.5 Tool Lifecycle

- **Tool name:** `dnsinspect`
- **Initial capability:** Resolve hostname to IP.
- **Final scope:** Query multiple record types; display TTL; compare two resolvers; classify DNS errors with explanations.
- **Important error states:** NXDOMAIN, SERVFAIL, REFUSED, network timeout, invalid hostname.
- **Security invariants:** Queries only the specified target; does not modify DNS records; does not follow infinite CNAME chains (cap at 10 hops).
- **External dependency:** `github.com/miekg/dns` — introduced for TTL access (milestone 04.3); document the reason.
- **Testing expectations:** Tests for each record type; error classification tests using a local DNS test server; resolver comparison test.
- **Downstream consumers:** Chapter 08 uses TXT records for SPF/DMARC inspection. Chapter 18 includes DNS reconnaissance.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Unit: hostname parsing, error classification.
- Integration: local DNS server (e.g., `miekg/dns` test server) for deterministic record responses.
- Resolver comparison: two local servers returning different answers.
- CNAME chain test: verify cycle detection and hop limit.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses DNS inspection to map infrastructure — find all IP addresses behind a domain, discover mail servers, read TXT records for cloud provider verification tokens.
- **Blue Team (Samia):** Verifies that DNS records are correct. Checks SPF/DMARC TXT records for email security. Compares resolver responses to detect possible DNS hijacking or split-horizon misconfigurations.
- **Connection:** DNS findings inform the HTTP Inspector (which services to visit) and the TLS Checker (which hostnames to verify).

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| DNS resolution sequence diagram | Full resolution chain | 04.1 |
| Record type reference table | A, AAAA, MX, TXT, CNAME, NS | 04.2 |
| TTL caching timeline diagram | Why TTL matters | 04.3 |
| Resolver comparison diagram | Divergent responses | 04.4 |
| DNS error classification table | RCODE meanings | 04.5 |

---

### Chapter 05 — Identify the Service: Build a Service Fingerprinter

#### 8.1 Chapter Identity

- **Phase:** 2 — Discover What's Running on a Network
- **Primary capability:** The learner can identify which service is running behind an open TCP port by inspecting banners and protocol responses, and can represent confidence levels in findings.
- **Primary tool:** **svcfinger** — a service fingerprinter that connects to open ports, reads initial data, matches against known patterns, and reports findings with explicit confidence levels.
- **Intended level:** Intermediate.
- **Real-world relevance:** Port numbers are hints, not proof. Services are often misconfigured, moved to non-standard ports, or impersonated. Fingerprinting using actual protocol responses is more reliable than port number lookup.

#### 8.2 Learning Outcomes

By completing Chapter 05, the learner can:

1. Explain the difference between a port number and the service actually running behind it.
2. Connect to an open TCP port, read the initial response (banner), and match it against known patterns.
3. Issue simple protocol-specific probes (HTTP HEAD, SMTP EHLO) and interpret responses.
4. Represent confidence in findings: identified, probable, or unknown.
5. Explain what false positives mean in the context of service fingerprinting.
6. Integrate with `portscan` output to fingerprint all discovered open ports.
7. Handle non-responsive ports and protocols that do not send a banner without blocking indefinitely.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 02 (TCP connectivity), Chapter 03 (port scanning, TCP connection lifecycle).
- **Downstream consumers:** Chapter 06 (HTTP Inspector) takes over where fingerprinting identifies an HTTP service. Chapter 18 (Final Engagement) uses fingerprinting as part of reconnaissance.

#### 8.4 Subchapter Milestone Plan

**05.1 — First Bytes: Read the Banner**

- *Capability gained:* Connect to a port, read the first response bytes (banner), and display them.
- *New theory:* Banner as a service's greeting. Read timeout for non-banner services. How much to read (cap at 1 KiB). Non-printable byte handling in output.
- *Visualizations:* Diagram showing client connecting, server immediately sending a banner line, client reading. Examples: SSH banner, SMTP greeting, FTP welcome.
- *Tool evolution:* `svcfinger <host:port>` connects, reads up to 1 KiB with a read timeout, and prints the raw banner.
- *Challenge:* Display banner as both raw hex and printable text (reusing Byte Inspector concepts). Note when a service sends no banner.
- *Constraints:* Read timeout: 3 seconds. Do not wait indefinitely for a service that does not send a banner.
- *Acceptance criteria:* Connecting to a local SMTP server returns the SMTP greeting. A local HTTP server that sends no banner on connect returns "no banner received."
- *Verification:* Local test servers for each case.
- *Enables:* 05.2.

**05.2 — Match the Pattern: Identify Services by Banner**

- *Capability gained:* Match banners against a known-pattern table and return an identified service name.
- *New theory:* Pattern matching strategies (prefix match, regex, case-insensitive substring). False positives: why a match does not prove the service. Confidence levels.
- *Visualizations:* Table: banner pattern → service → confidence. Flowchart: banner → try patterns → match found → report identified; no match → report unknown.
- *Tool evolution:* Add a pattern table for SSH, SMTP, FTP, HTTP (response to probe), and Redis. Match incoming banners.
- *Challenge:* For each match, report: service name, matched pattern, confidence level (`identified` / `probable` / `unknown`). Never report `identified` on a partial or ambiguous match.
- *Constraints:* Pattern table is embedded in code (no external file). Maximum 30 patterns initially. Must not claim certainty from a weak match.
- *Acceptance criteria:* SSH banner `SSH-2.0-OpenSSH_8.9` matches with confidence `identified`. Random binary data matches with confidence `unknown`.
- *Verification:* Unit tests for pattern matching logic using inline test banners.
- *Enables:* 05.3.

**05.3 — Ask the Question: Protocol-Specific Probes**

- *Capability gained:* For services that don't send a banner, send a minimal probe and inspect the response.
- *New theory:* Active probing vs. passive banner reading. HTTP HEAD request. HTTP/1.0 minimal request. Why probing can reveal what a passive read cannot.
- *Visualizations:* Sequence diagram: client connects → no banner → client sends `HEAD / HTTP/1.0\r\n\r\n` → server responds → client parses status line.
- *Tool evolution:* Add probe logic: if no banner received, attempt HTTP probe. If HTTP response returned, classify as HTTP with `identified` or `probable` confidence. Try probe only for ports in common HTTP range (80, 443, 8080, 8443) unless `--probe` flag is given.
- *Challenge:* Implement the HTTP probe and response parser. The parser must extract at minimum the HTTP version and status code. Invalid HTTP responses must not panic the prober.
- *Constraints:* Probe timeout: 3 seconds. Only probe services on a whitelist of ports unless `--probe-all` flag is explicitly given.
- *Acceptance criteria:* A local HTTP server on port 8080 that sends no initial banner is correctly identified after an HTTP HEAD probe.
- *Verification:* Local `net/http` test server.
- *Enables:* 05.4.

**05.4 — Be Honest: Represent Confidence Explicitly**

- *Capability gained:* The output includes explicit confidence levels, the evidence that led to the classification, and notes for ambiguous results.
- *New theory:* Evidence quality in security findings. Why a "probable" finding is not a confirmed finding. The difference between "this looks like SSH" and "this is SSH." How false positives affect downstream decisions.
- *Visualizations:* Table: confidence level → meaning → action recommended.
- *Tool evolution:* Improve the output structure: include `confidence`, `evidence` (the matched pattern or probe response), and `notes` for ambiguous results. Add `--output json`.
- *Challenge:* For a port returning HTTP-like data on port 22, report `probable` with a note that the port number is inconsistent with the observed protocol.
- *Constraints:* The word "identified" may only appear in output when a definitive pattern match or valid protocol response is found.
- *Acceptance criteria:* JSON output includes `confidence`, `evidence`, and `service` fields. A port with a valid HTTP response but on port 22 gets `probable`, not `identified`.
- *Verification:* Test cases that distinguish `identified` from `probable`.
- *Enables:* 05.5.

**05.5 — Scale Up: Fingerprint All Open Ports**

- *Capability gained:* Accept a list of host:port pairs (e.g., from `portscan --output json`) and fingerprint each one, producing a combined report.
- *New theory:* Composing tools with pipes. JSON as interchange format. Why fingerprinting all open ports in a scan is the natural next step after discovery.
- *Tool evolution:* Add `--input` flag accepting a file of `host:port` entries or piped JSON from `portscan`. Add `--workers` for concurrency.
- *Challenge:* Read open port results, fingerprint each with configurable concurrency, produce a JSON report with one entry per port.
- *Constraints:* Workers: default 10, max 100. Must not fingerprint ports marked `closed` or `unknown`.
- *Acceptance criteria:* Piping `portscan --output json` to `svcfinger --input -` fingerprints all open ports.
- *Verification:* Integration test: spin up multiple local servers on different ports, scan, fingerprint, verify each is correctly identified.
- *Enables:* Chapter 06 (HTTP Inspector) takes over when an HTTP service is identified. The `portscan → svcfinger` pipeline becomes the standard reconnaissance chain.

#### 8.5 Tool Lifecycle

- **Tool name:** `svcfinger`
- **Initial capability:** Read banner from a single port.
- **Final scope:** Read banners, apply pattern matching, issue probes, report confidence levels, accept input lists, support concurrency.
- **Output contract:** Each result has: `host`, `port`, `service` (or `unknown`), `confidence` (`identified`/`probable`/`unknown`), `evidence` (the matching string), `notes` (optional).
- **Important error states:** Connection refused (port closed after scan), no banner and probe failed, read timeout, probe timeout.
- **Security invariants:** Default probe-only mode limits probing to expected HTTP ports. `--probe-all` requires explicit consent. Must not leave connections open.
- **Testing expectations:** Unit tests for pattern matching. Integration tests with local servers. Composability test with `portscan` output.
- **Downstream consumers:** Chapter 06 receives identified HTTP services. Chapter 18 reuses in reconnaissance.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Unit: banner pattern matching for all defined patterns.
- Integration: SSH banner, SMTP greeting, HTTP probe, unknown binary service.
- Confidence test: ambiguous service correctly marked `probable`.
- Pipeline test: `portscan` JSON → `svcfinger`.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses the fingerprinter to understand what is actually running on each discovered port, regardless of the expected port number assignment. Identifies unexpected services and version information.
- **Blue Team (Samia):** Uses fingerprinting results to verify that every exposed service is expected and authorized. Unexpectedly identified services are escalated for investigation. Version banners reveal patch levels.
- **Connection:** Fingerprinting findings inform HTTP inspection (Chapter 06), TLS checking (Chapter 11), and the final engagement (Chapter 18).

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Banner read sequence diagram | Client/server initial exchange | 05.1 |
| Pattern match flowchart | From banner to classification | 05.2 |
| HTTP probe sequence diagram | Active probing for silent services | 05.3 |
| Confidence level table | identified/probable/unknown semantics | 05.4 |

---

## Phase 3: Understand and Inspect Web Traffic

---

### Chapter 06 — Read the Web's Conversation: Build an HTTP Inspector

#### 8.1 Chapter Identity

- **Phase:** 3 — Understand and Inspect Web Traffic
- **Primary capability:** The learner can inspect the full HTTP conversation: request structure, response headers, status codes, body handling, redirects, and HTTPS connections.
- **Primary tool:** **httpinspect** — a command-line HTTP inspector that sends configurable requests and displays the complete conversation.
- **Intended level:** Intermediate.
- **Real-world relevance:** HTTP is the protocol of web applications, APIs, and most modern services. Security engineers read HTTP conversations constantly — for vulnerability assessment, incident response, traffic analysis, and API testing.

#### 8.2 Learning Outcomes

By completing Chapter 06, the learner can:

1. Explain HTTP request structure: method, path, HTTP version, headers, body.
2. Explain HTTP response structure: status code, reason phrase, headers, body.
3. Use Go's `net/http` client to send configurable requests and inspect responses.
4. Explain common status code categories and their security relevance.
5. Trace redirect chains and explain why redirects matter for security.
6. Distinguish HTTP/1.1 from HTTP/2 at a conceptual level.
7. Send HTTPS requests using Go's standard library without disabling certificate validation.
8. Format and display complete HTTP conversations in a readable, structured format.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 02 (networking model), Chapter 03 (TCP), Chapter 04 (DNS).
- **Must not assume:** TLS internals (Chapter 11 covers those). Chapter 06 uses HTTPS as a black box via Go's standard library.
- **Downstream consumers:** Chapter 07 (HTTP Proxy) builds on the client model. Chapter 08 (Web Security Header Scanner) reads response headers. Chapter 09 (Web Authorization Tester) sends authenticated requests. Chapter 11 (TLS Checker) digs into the TLS layer that Chapter 06 treats as opaque.

#### 8.4 Subchapter Milestone Plan

**06.1 — First Request: Send GET and Print Status**

- *Capability gained:* Send an HTTP GET request and print the response status code.
- *New theory:* HTTP request/response model. `http.Get`. Status code categories (1xx, 2xx, 3xx, 4xx, 5xx). Why status codes matter. The `net/http` client defaults.
- *Visualizations:* Request/response diagram. Status code category table with security relevance column.
- *Tool evolution:* `httpinspect <URL>` sends GET, prints status code and reason phrase.
- *Challenge:* Exit with status 0 on 2xx, 1 on 4xx/5xx, 2 on connection/network error.
- *Acceptance criteria:* `httpinspect http://localhost:8080/` against a local server returns the correct status.
- *Verification:* Local `net/http` test server.
- *Enables:* 06.2.

**06.2 — See Everything: Display Headers and Body**

- *Capability gained:* Display all request and response headers and the response body.
- *New theory:* HTTP headers: purpose, format, common security-relevant headers. Content-Type and body encoding. Reading a response body without exhausting it (`io.LimitReader`).
- *Visualizations:* Annotated HTTP request and response showing each component. Table of common security-relevant headers.
- *Tool evolution:* Print request headers sent, response headers received, and body. Add `--max-body N` flag (default: 10 KiB) to limit body display.
- *Challenge:* Format the conversation with clear section separators. Truncate body at limit but report the actual Content-Length or transfer-encoded size.
- *Constraints:* Must not buffer the full body into memory when the body exceeds the limit.
- *Acceptance criteria:* A server returning 20 KiB response body with `--max-body 1024` shows only the first 1 KiB with a truncation notice.
- *Verification:* Test server returning configurable response sizes.
- *Enables:* 06.3.

**06.3 — More Than GET: Support Multiple Methods and Custom Headers**

- *Capability gained:* Send POST, HEAD, PUT, DELETE, and custom-method requests with configurable headers and body.
- *New theory:* HTTP methods and their semantics. When to use HEAD (metadata without body). Request body and Content-Type. Custom headers.
- *Visualizations:* Table: HTTP method → typical use → security testing relevance.
- *Tool evolution:* Add `--method`, `--header`, `--body`, `--content-type` flags. For HEAD requests, do not attempt to print a body.
- *Challenge:* Build an `http.Request` from the flags rather than using `http.Get`. Validate that `--body` is not used with GET or HEAD.
- *Constraints:* Reject inconsistent flag combinations (body with GET/HEAD) with a clear error.
- *Acceptance criteria:* `httpinspect --method POST --body '{"test":1}' --content-type application/json http://localhost:8080/` sends a correct POST.
- *Verification:* Test server that echoes request method and body back.
- *Enables:* 06.4.

**06.4 — Follow the Chain: Trace Redirects**

- *Capability gained:* Trace and display each redirect in a redirect chain.
- *New theory:* HTTP redirects (301, 302, 303, 307, 308). `Location` header. Redirect loops. HTTP → HTTPS upgrade redirects. Why redirect chains matter for security (open redirects, protocol downgrades).
- *Visualizations:* Sequence diagram: client → server returns 301 → client follows → final server. Table: redirect codes and their semantics.
- *Tool evolution:* Implement custom `CheckRedirect` function. `--no-follow` flag to disable redirect following. Print each hop with its status and Location.
- *Challenge:* Detect redirect loops (same URL seen twice) and exit cleanly with an error. Default: follow up to 10 redirects.
- *Constraints:* Redirect limit must be enforced. Loop detection must prevent infinite loops even if the limit is raised.
- *Acceptance criteria:* A server returning a 301 chain of 3 hops shows all 3 hops and the final response. A loop chain produces a clear loop error.
- *Verification:* Local test server that implements configurable redirect chains and loops.
- *Enables:* 06.5.

**06.5 — Secure Connection: Handle HTTPS**

- *Capability gained:* Send HTTPS requests and display TLS information (certificate subject and expiry).
- *New theory:* TLS as a transport layer. How Go's `http.Client` negotiates TLS. `tls.ConnectionState`. Certificate subject and expiry. Why ignoring certificate errors is dangerous (and not a default here). The difference between a valid TLS connection and a secure application.
- *Visualizations:* Layer diagram: HTTP → TLS → TCP → IP. Brief certificate chain overview.
- *Tool evolution:* Accept `https://` URLs. After a successful HTTPS request, print a TLS summary: TLS version, cipher suite, certificate subject, expiry, and whether the chain verified.
- *Challenge:* TLS must use the system trust store. Certificate errors must cause a non-zero exit. The `--insecure` flag may be added but must print a prominent warning and must not be silently used.
- *Constraints:* `InsecureSkipVerify` must not be the default. If used, log a warning to stderr.
- *Acceptance criteria:* An `https://localhost` request with a self-signed certificate fails with a certificate error unless `--insecure` is explicitly passed.
- *Verification:* Local HTTPS test server with a self-signed certificate generated in the test setup.
- *Enables:* Chapter 07 (HTTP Proxy), Chapter 08 (Web Security Header Scanner), Chapter 11 (TLS Certificate Checker digs deeper into TLS).

**06.6 — Structured Output: JSON and Human-Readable Formats**

- *Capability gained:* Produce a complete structured JSON record of the HTTP conversation for downstream use.
- *New theory:* Designing a conversation record schema. Timestamps and durations. Structured vs. human-readable output for tool composability.
- *Tool evolution:* Add `--output json`. Define `HTTPConversation` struct. Include: request (method, URL, headers), response (status, headers, body excerpt, body size), TLS summary, redirect chain, timing.
- *Challenge:* All previous flags must work with `--output json`. Partial conversations (on connection error) must produce a JSON error record, not a panic.
- *Acceptance criteria:* `httpinspect --output json <url> | jq .response.status_code` returns an integer.
- *Verification:* Full regression test suite. All milestone tests must still pass.
- *Enables:* Chapter 08 reads httpinspect output or reuses its HTTP request logic. Chapter 09 extends it for authentication.

#### 8.5 Tool Lifecycle

- **Tool name:** `httpinspect`
- **Initial capability:** Send GET and print status.
- **Final scope:** Configurable method/headers/body; redirect tracing; HTTPS with TLS summary; structured JSON output; body size limiting.
- **Output contract:** `HTTPConversation` JSON schema is documented and stable from 06.6 onward.
- **Important error states:** Connection refused; TLS certificate error; redirect loop; timeout; response body read error.
- **Security invariants:** `InsecureSkipVerify` requires explicit `--insecure` flag and logs a warning. No certificate errors silently ignored.
- **Testing expectations:** Local test servers for all scenarios. No public internet access required.
- **Downstream consumers:** Chapter 08 (Web Security Header Scanner) reads response headers. Chapter 09 (Web Authorization Tester) sends authenticated requests. Chapter 11 (TLS Checker) inspects TLS in depth.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Each milestone has a local test server.
- Body size limit test.
- Redirect chain test (3 hops, loop).
- HTTPS with self-signed cert: certificate error test. With `--insecure`: succeeds with warning.
- Regression: all milestone tests pass after 06.6.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses `httpinspect` to explore web application endpoints, understand redirect behavior, and identify information disclosure in response headers and bodies.
- **Blue Team (Samia):** Examines HTTP conversations to verify that responses do not leak sensitive headers, that redirects enforce HTTPS, and that error responses don't reveal stack traces.
- **Connection:** Chapter 08 audits the headers visible in `httpinspect` output. Chapter 09 uses the HTTP client to test authorization boundaries.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| HTTP request/response diagram | Request and response anatomy | 06.1 |
| Status code category table | 1xx–5xx meanings and security relevance | 06.1 |
| Security-relevant headers table | Which headers matter and why | 06.2 |
| HTTP method semantics table | When each method is used | 06.3 |
| Redirect chain sequence diagram | Following hops | 06.4 |
| HTTP/TLS layer diagram | Where TLS fits in the stack | 06.5 |

---

### Chapter 07 — See Through the Middle: Build an HTTP Proxy

#### 8.1 Chapter Identity

- **Phase:** 3 — Understand and Inspect Web Traffic
- **Primary capability:** The learner can implement a local HTTP forward proxy that intercepts, logs, and optionally modifies HTTP traffic between a client and a server.
- **Primary tool:** **httpproxy** — a local HTTP forward proxy with request/response logging, header inspection, configurable body limits, and sensitive data redaction.
- **Intended level:** Intermediate.
- **Real-world relevance:** Proxy tools are fundamental to web security testing. Understanding how a proxy works — and what it can and cannot see — is essential for web application security assessment. MITM proxies are used by every web security professional.

#### 8.2 Learning Outcomes

By completing Chapter 07, the learner can:

1. Explain how an HTTP forward proxy differs from a reverse proxy.
2. Implement an HTTP proxy that receives client requests and forwards them to upstream servers.
3. Log requests and responses in a structured format.
4. Explain why proxying HTTPS traffic (CONNECT tunneling) differs from proxying plain HTTP.
5. Add, remove, and inspect HTTP headers during forwarding.
6. Enforce body size limits and connection timeouts.
7. Redact sensitive values from proxy logs.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 06 (HTTP client, request/response model, headers).
- **Must not assume:** TLS internals (Chapter 11). This chapter explains CONNECT tunneling for HTTPS proxying without inspecting the encrypted content.
- **Downstream consumers:** Chapter 09 (Web Authorization Tester) can use `httpproxy` to intercept and inspect authorization flows. Chapter 18 (Final Engagement) uses the proxy for traffic analysis.

#### 8.4 Subchapter Milestone Plan

**07.1 — Pass It Through: A Minimal Forward Proxy**

- *Capability gained:* A server that accepts HTTP requests and forwards them to upstream servers.
- *New theory:* Forward proxy model. How the client addresses a request to the proxy (full URL in request line). `http.RoundTripper`. Stripping hop-by-hop headers (`Connection`, `Proxy-Connection`, etc.).
- *Visualizations:* Architecture diagram: client → proxy → upstream server. Sequence diagram showing request forwarding.
- *Tool evolution:* `httpproxy --listen :8888` starts a proxy. Configure browser or `httpinspect` to use it.
- *Challenge:* Forward any HTTP request and stream the response back. Remove standard hop-by-hop headers before forwarding.
- *Constraints:* Listen on loopback only by default. Enforce a maximum upstream response size (configurable, default 10 MiB).
- *Acceptance criteria:* `curl --proxy http://localhost:8888 http://localhost:9090/` reaches the upstream server and receives the correct response.
- *Verification:* Local upstream test server.
- *Enables:* 07.2.

**07.2 — Write It Down: Request and Response Logging**

- *Capability gained:* Log each proxied request and response in a structured format.
- *New theory:* Structured logging with `log/slog` (Go 1.21+). What to log: method, URL, status, duration, request and response size. What not to log by default (bodies, authorization headers).
- *Visualizations:* Example log line annotated with field names.
- *Tool evolution:* Add structured logging per proxied request: timestamp, method, URL, upstream response status, duration in milliseconds, request body size, response body size.
- *Challenge:* Write one log entry per proxied request to stdout in JSON format. Do not log request or response bodies by default.
- *Constraints:* Log must not block request forwarding. Log errors (proxy errors, upstream failures) on stderr.
- *Acceptance criteria:* After proxying five requests, the log has exactly five JSON entries with correct fields.
- *Verification:* Test that parses log output and checks field presence.
- *Enables:* 07.3.

**07.3 — Touch the Headers: Inspect and Modify**

- *Capability gained:* Add, remove, or replace request headers before forwarding; log all headers in verbose mode.
- *New theory:* Why proxies modify headers (X-Forwarded-For, Via, custom auth injection). The risk of header injection. Security implications of adding or removing security headers at the proxy layer.
- *Visualizations:* Diagram showing header transformations at the proxy.
- *Tool evolution:* Add `--add-header "Key: Value"` and `--remove-header Key` flags. In `--verbose` mode, log all request and response headers.
- *Challenge:* Apply configured header additions and removals on every request. Reject header injection attempts (values containing newlines) with a clear error.
- *Constraints:* Newlines in header values must be rejected. Header modifications must not affect hop-by-hop headers.
- *Acceptance criteria:* `--add-header "X-Debug: 1"` causes every upstream request to include that header. `--remove-header Authorization` strips auth from every request.
- *Verification:* Upstream test server that echoes received headers.
- *Enables:* 07.4.

**07.4 — Don't Get Stuck: Resource Limits and Timeouts**

- *Capability gained:* Enforce timeouts for upstream connections and response reads; limit concurrent connections.
- *New theory:* `http.Transport` tuning: `DialContext`, `ResponseHeaderTimeout`, `IdleConnTimeout`. Why proxies need aggressive timeouts. Slow client attacks.
- *Tool evolution:* Add `--upstream-timeout` and `--connect-timeout` flags. Limit maximum concurrent proxy connections with a semaphore (`--max-connections`, default 100).
- *Challenge:* A slow upstream that never sends headers must be cancelled after `--upstream-timeout`. A slow client that never reads must be cancelled after a read timeout.
- *Constraints:* Goroutines must not leak when connections time out.
- *Acceptance criteria:* A test upstream that delays the response header causes the proxy to return 504 after the configured timeout.
- *Verification:* Local slow-server test helper.
- *Enables:* 07.5.

**07.5 — Keep Secrets: Redact Sensitive Data from Logs**

- *Capability gained:* Redact sensitive header values (Authorization, Cookie, Set-Cookie) from logs; support a configurable redaction list.
- *New theory:* Why logging credentials is dangerous. What constitutes sensitive data in HTTP headers. The difference between redacting and removing.
- *Tool evolution:* Redact values of `Authorization`, `Cookie`, and `Set-Cookie` headers in logs (replace with `[redacted]`). Add `--redact-header Key` for additional headers.
- *Challenge:* Apply redaction consistently in all log output paths. Verify that redaction does not affect forwarded headers — only logged values.
- *Constraints:* Redaction must not affect request forwarding. Redacted fields must appear as `[redacted]` in log output.
- *Acceptance criteria:* A request with `Authorization: Bearer secret-token` logs `Authorization: [redacted]` but the upstream server receives the real header.
- *Verification:* Test that checks log output for `[redacted]` and upstream server for the real value.
- *Enables:* Chapter 09 (Web Authorization Tester) uses the proxy to intercept auth flows. The proxy becomes a general-purpose local lab tool.

#### 8.5 Tool Lifecycle

- **Tool name:** `httpproxy`
- **Initial capability:** Forward HTTP requests.
- **Final scope:** Forward proxy with structured logging, header modification, resource limits, and sensitive data redaction.
- **Important error states:** Upstream connection failure; upstream timeout; response too large; client disconnect before response complete; invalid header injection attempt.
- **Security invariants:** Loopback only by default. Sensitive headers redacted from logs. Header injection rejected.
- **Testing expectations:** Local upstream test servers for all scenarios. Goroutine leak checks.
- **Downstream consumers:** Chapter 09 (intercepting auth flows). Chapter 18 (traffic analysis during engagement).
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Forward proxy happy path.
- Slow upstream timeout (504).
- Header injection rejection.
- Redaction: log has `[redacted]`, upstream sees real value.
- Goroutine leak check.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses the proxy to inspect all traffic between a test client and a web application, revealing cookies, tokens, and API call patterns.
- **Blue Team (Samia):** Understands how proxies can expose sensitive data. Reviews proxy logs for suspicious traffic patterns. Verifies that authorization headers are not logged in production systems.
- **Connection:** Chapter 09 (Web Authorization Tester) uses the proxy to inspect authentication flows without manually reconstructing request/response pairs.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Forward proxy architecture diagram | Client → proxy → upstream | 07.1 |
| Request forwarding sequence diagram | Hop-by-hop vs. end-to-end headers | 07.1 |
| Header transformation diagram | What the proxy adds/removes | 07.3 |

---

### Chapter 08 — Audit the Web Surface: Build a Web Security Header Scanner

#### 8.1 Chapter Identity

- **Phase:** 3 — Understand and Inspect Web Traffic
- **Primary capability:** The learner can audit a web application's response headers and cookie attributes for security misconfigurations, classify findings by severity, and verify mitigations.
- **Primary tool:** **webscan** — a web security header scanner that inspects HTTP responses for missing or misconfigured security headers and cookie attributes.
- **Intended level:** Intermediate.
- **Real-world relevance:** Security headers and cookie attributes are the first line of defense against a wide range of web attacks. Misconfigured headers are among the most common and most easily fixed findings in web security assessments.

> **Curriculum decision:** The original proposed Chapter 08 covered both surface auditing and authorization testing. These are sufficiently different in scope and tool design that they are split into Chapter 08 (surface/headers) and Chapter 09 (authorization/behavior). This allows each chapter to have a focused, achievable tool milestone plan.

#### 8.2 Learning Outcomes

By completing Chapter 08, the learner can:

1. Identify the security-relevant HTTP response headers and explain the protection each one provides.
2. Explain the security attributes of HTTP cookies (`Secure`, `HttpOnly`, `SameSite`).
3. Scan a web application and produce a severity-classified report of missing or weak security headers.
4. Distinguish a confirmed misconfiguration from a suspected one.
5. Verify that mitigations added to a server actually appear in subsequent scan results.
6. Explain why a passing scan does not guarantee a secure application.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 06 (HTTP Inspector — sends requests, reads response headers).
- **Downstream consumers:** Chapter 09 (Web Authorization Tester) builds on the audit infrastructure. Chapter 18 (Final Engagement) includes header scanning as part of reconnaissance.

#### 8.4 Subchapter Milestone Plan

**08.1 — The Header Inventory: What Headers Should Be There?**

- *Capability gained:* Send an HTTP/HTTPS request and list all security-relevant response headers.
- *New theory:* Security headers: `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`, `Strict-Transport-Security`, `Referrer-Policy`, `Permissions-Policy`. What each protects against.
- *Visualizations:* Table: header name → attack it mitigates → minimum secure value.
- *Tool evolution:* `webscan <URL>` sends a GET, prints each security header it finds and each it does not find (with "missing" label).
- *Challenge:* Identify which security headers are present, which are missing, and which are present but with a weak value. Define a minimal rule for each header.
- *Constraints:* Treat HTTPS as required for `HSTS` to be meaningful. Flag `HSTS` as not applicable on plain HTTP.
- *Acceptance criteria:* Against a local server with no security headers, all expected headers are listed as missing.
- *Verification:* Local test server with configurable response headers.
- *Enables:* 08.2.

**08.2 — The Cookie Jar: Audit Cookie Security Attributes**

- *Capability gained:* Parse `Set-Cookie` headers and audit each cookie's security attributes.
- *New theory:* `Secure` flag (HTTPS only), `HttpOnly` (no JavaScript access), `SameSite` (`Strict`/`Lax`/`None`). Cookie scope: `Domain`, `Path`. `Max-Age` and `Expires`. Why each attribute matters.
- *Visualizations:* Annotated `Set-Cookie` header with each attribute labeled.
- *Tool evolution:* Add cookie audit to `webscan`. For each `Set-Cookie`, report which security attributes are present and which are missing.
- *Challenge:* Parse `Set-Cookie` headers using `net/http`'s cookie parser. Classify each missing attribute by severity (e.g., missing `Secure` on a session cookie = high).
- *Constraints:* Multiple cookies handled independently. Must handle cookies with no attributes (only name=value).
- *Acceptance criteria:* A cookie without `HttpOnly` is flagged. A cookie with `SameSite=None` without `Secure` is flagged as a critical misconfiguration.
- *Verification:* Test server issuing cookies with various attribute combinations.
- *Enables:* 08.3.

**08.3 — HTTP vs. HTTPS: Detect Protocol Security Issues**

- *Capability gained:* Detect when a site is served over HTTP without a redirect to HTTPS, or when HSTS is misconfigured.
- *New theory:* HTTP → HTTPS redirect. HSTS `max-age`. `includeSubDomains`. The difference between serving over HTTPS and enforcing HTTPS.
- *Tool evolution:* If target is HTTP, check whether it redirects to HTTPS. If HTTPS, check for `Strict-Transport-Security` presence and `max-age` value.
- *Challenge:* Report: serves HTTP without redirect (high), serves HTTP with redirect (informational), serves HTTPS without HSTS (medium), HSTS present but max-age < 6 months (low), HSTS present with adequate max-age (pass).
- *Acceptance criteria:* Each scenario correctly classified against local test servers.
- *Verification:* Local HTTP and HTTPS test servers with configurable redirect and HSTS behavior.
- *Enables:* 08.4.

**08.4 — Score and Report: Classify Findings by Severity**

- *Capability gained:* Produce a structured audit report with severity levels (critical, high, medium, low, informational, pass) and a summary score.
- *New theory:* Severity classification frameworks. Why "pass" is not "secure" — a header can be present but configured for minimal protection. Evidence vs. inference in security findings.
- *Visualizations:* Example audit report structure. Severity color coding in terminal (optional, flag-controlled).
- *Tool evolution:* Aggregate all findings into a structured report. Add `--output json`. Exit non-zero if any critical or high finding is present.
- *Challenge:* For each finding: header or cookie name, finding type (missing/weak/present), severity, recommendation. Summary: counts by severity.
- *Constraints:* JSON output must be valid. Exit code: 0 = no critical/high findings; 1 = critical/high found; 2 = tool error.
- *Acceptance criteria:* `webscan <url> --output json | jq '.findings[] | select(.severity == "high")'` returns correct findings for a known misconfigured server.
- *Verification:* Parameterized test with controlled local server configurations.
- *Enables:* 08.5.

**08.5 — Did It Work?: Verify Mitigations**

- *Capability gained:* Re-scan after a mitigation is applied and compare results, confirming which findings are resolved.
- *New theory:* Verification as a separate activity from scanning. Why a second scan (rather than assuming the fix worked) is essential. Diff-based reporting.
- *Tool evolution:* Add `--baseline <previous-scan.json>` flag. Compare current scan to baseline, report: resolved findings, new findings, unchanged findings.
- *Challenge:* Produce a diff report. Exit 0 only if all previously-critical/high findings are resolved.
- *Acceptance criteria:* A server initially missing `X-Frame-Options` receives the header; `--baseline` scan shows the finding as resolved.
- *Verification:* Two sequential scans of a local server, the second with the header added.
- *Enables:* This verification pattern is reused in Chapter 09 (Web Authorization Tester), Chapter 13 (Fuzz Testing regression), and Chapter 14 (Vulnerability Regression Harness).

#### 8.5 Tool Lifecycle

- **Tool name:** `webscan`
- **Initial capability:** List present/missing security headers.
- **Final scope:** Security header audit, cookie attribute audit, HTTPS enforcement check, severity classification, JSON output, baseline comparison.
- **Output contract:** JSON `AuditReport` with findings array; each finding has name, type, severity, recommendation.
- **Important error states:** Connection failure; TLS error; redirect loop; body read error.
- **Security invariants:** `--insecure` flag required to bypass TLS errors (with warning). No cookies or credentials stored.
- **Testing expectations:** Parameterized local server tests for each header/cookie scenario.
- **Downstream consumers:** Chapter 09. Chapter 18 reconnaissance.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Each header: present/missing/weak scenarios.
- Each cookie attribute: present/missing.
- HTTPS enforcement: all three scenarios.
- Baseline comparison: resolved and new findings.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses `webscan` to identify missing security headers that indicate exploitable attack surfaces (XSS enabled by missing CSP, clickjacking possible without X-Frame-Options).
- **Blue Team (Samia):** Uses `webscan` to audit deployed applications. Verifies that security headers are correctly configured after each deployment. Uses baseline comparison to detect regressions.
- **Connection:** Findings from `webscan` feed into Chapter 09 (Web Authorization Tester) which tests the behavioral security that headers cannot protect.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Security headers reference table | Each header and its protection | 08.1 |
| Annotated Set-Cookie header | Attribute meanings | 08.2 |
| HTTPS enforcement decision flowchart | HTTP → HTTPS states | 08.3 |
| Severity classification table | Critical → informational scale | 08.4 |

---

### Chapter 09 — Test the Trust Boundary: Build a Web Authorization Tester

#### 8.1 Chapter Identity

- **Phase:** 3 — Understand and Inspect Web Traffic
- **Primary capability:** The learner can systematically test authentication and authorization boundaries on a local web application, distinguishing confirmed failures from suspected ones, and verifying that mitigations hold.
- **Primary tool:** **authtest** — a web authorization tester that sends requests with controlled credential sets and reports authorization boundary failures.
- **Intended level:** Intermediate to advanced.
- **Real-world relevance:** Authorization failures — accessing resources you shouldn't — are one of the most common and most damaging web application vulnerabilities. Testing them requires systematic, evidence-based methodology, not guesswork.

> **All exercises in this chapter must target the local lab application only. The chapter specifies a local intentionally-vulnerable application as the test target.**

#### 8.2 Learning Outcomes

By completing Chapter 09, the learner can:

1. Explain the difference between authentication (who you are) and authorization (what you are allowed to do).
2. Test whether endpoints require authentication by sending unauthenticated requests.
3. Test whether role boundaries are enforced by sending requests with different credential levels.
4. Inspect and decode session tokens (JWT, cookie-based).
5. Design and execute a controlled path traversal test against a local server.
6. Classify findings as confirmed, probable, or suspected based on observable evidence.
7. Apply a mitigation and re-test to confirm the fix.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 06 (HTTP Inspector — authenticated requests), Chapter 07 (HTTP Proxy — intercepting flows), Chapter 08 (webscan — audit methodology).
- **Lab requirement:** A local intentionally-vulnerable web application. The chapter specifies one (e.g., a purpose-built Go server provided in the chapter's lab setup section).
- **Downstream consumers:** Chapter 14 (Vulnerability Regression Harness) extends the regression verification approach. Chapter 18 (Final Engagement) includes authorization testing as a phase.

#### 8.4 Subchapter Milestone Plan

**09.1 — Who Are You?: Understand Auth vs. Authz**

- *Capability gained:* Distinguish authentication from authorization with concrete examples. Explain common auth mechanisms in HTTP.
- *New theory:* Authentication: verifying identity (cookie session, JWT, HTTP Basic, API key). Authorization: verifying permission after identity is established. RBAC basics. Why authenticated ≠ authorized.
- *Visualizations:* Flowchart: request arrives → is identity known? (authentication) → is action permitted? (authorization). Table: auth mechanism → how it works → where it appears in HTTP.
- *Tool evolution:* No new tool yet. Lab exercise: send requests with and without credentials to the local lab server and observe the difference in responses.
- *Challenge:* Manually (using `httpinspect` or `curl`) identify three endpoints: one that requires no auth, one that requires auth, and one that requires a specific role.
- *Acceptance criteria:* The learner documents the evidence for each classification.
- *Enables:* 09.2.

**09.2 — The Open Door: Test Unauthenticated Access**

- *Capability gained:* Systematically test a list of endpoints without credentials and identify which respond as expected.
- *New theory:* HTTP status codes in auth context: 200 (open), 401 (unauthenticated), 403 (forbidden but identity known), 302 (redirect to login). Why 302 and 200 are both potentially concerning for endpoints that should be protected.
- *Tool evolution:* `authtest --urls urls.txt` sends unauthenticated GET to each URL and reports status code, redirect target (if any), and classification.
- *Challenge:* Classify each response: open (200), auth-redirected (3xx to login), denied (401/403), or unexpected. Flag 200 responses to non-public endpoints as potential unauthorized access.
- *Constraints:* URL list from file. Must use the local lab server. Target URL must be `127.0.0.1` or `localhost` in automated tests.
- *Acceptance criteria:* A lab server returning 200 for an endpoint that should require auth is flagged as a finding.
- *Verification:* Local lab server with configurable auth requirements.
- *Enables:* 09.3.

**09.3 — Role Boundaries: Test Authorization Differences**

- *Capability gained:* Test whether a lower-privilege credential can access resources that should require higher privilege.
- *New theory:* RBAC in HTTP: role embedded in JWT claim, role from session, role from header. How to send requests with different credential sets. IDOR (Insecure Direct Object Reference) basics.
- *Tool evolution:* Add `--credentials-file` accepting a file with named credential sets (e.g., `admin: Bearer token1`, `user: Bearer token2`). For each URL, test with each credential set. Report which credential can access which resource.
- *Challenge:* For each URL × credential combination, record the response status and body size. Flag combinations where a lower-privilege credential produces the same response as a higher-privilege one.
- *Constraints:* Credential file must not be logged. Lab server only.
- *Acceptance criteria:* A lab server with a misconfigured endpoint that allows `user` credentials to access `admin` data is correctly flagged.
- *Verification:* Lab server with intentional authorization bypass.
- *Enables:* 09.4.

**09.4 — What's in the Token?: Inspect Session Tokens**

- *Capability gained:* Decode JWT tokens and identify their claims. Detect common JWT misconfigurations.
- *New theory:* JWT structure: header.payload.signature. Base64URL encoding. Common claims (`sub`, `role`, `exp`, `iat`). JWT alg:none vulnerability (conceptual). Weak signature algorithms. Token expiry.
- *Visualizations:* Annotated JWT: three parts, each decoded. Table: common JWT claims and their security significance.
- *Tool evolution:* Add `authtest decode-token <jwt>` subcommand. Decode and display header and payload. Flag: expired token, `alg:none`, `alg:HS256` with weak secret indicators, missing `exp`.
- *Challenge:* Decode the JWT without a library (base64URL decode + JSON parse). Flag security concerns without verifying the signature (signature verification requires the server's key).
- *Constraints:* Do not attempt to forge tokens. Do not use a JWT library — implement the decoding yourself.
- *Acceptance criteria:* A sample expired JWT is correctly identified as expired. An `alg:none` JWT is flagged.
- *Verification:* Unit tests with known JWTs.
- *Enables:* 09.5.

**09.5 — Poke the Paths: Controlled Path Traversal Test**

- *Capability gained:* Test a local server's file-serving endpoint for path traversal by sending controlled, safe path inputs.
- *New theory:* Path traversal: `../` sequences in URLs and file paths. URL encoding. Why path normalization is important. The difference between a test input that confirms a vulnerability and one that doesn't.
- *Visualizations:* Diagram: URL → URL-decode → path normalize → file lookup → what happens at each step without/with protection.
- *Tool evolution:* Add `authtest path-test --base-url <url> --paths paths.txt`. Send each path, observe response code and body. Flag when a traversal path produces a 200 with file-like content.
- *Challenge:* Test a controlled list of traversal paths. The list must include valid paths (should return content), invalid paths (should return 404), and traversal attempts (should return 400 or 404, never file content).
- *Constraints:* Target must be the local lab server. Traversal test paths must be provided in a config file, not hard-coded. Do not attempt traversal beyond the server's web root in the test design.
- *Acceptance criteria:* A lab server without path normalization returns 200 with content for a traversal path — correctly flagged. A fixed server returns 400/404 — correctly reported as resolved.
- *Verification:* Two local lab servers: one vulnerable, one fixed.
- *Enables:* 09.6.

**09.6 — Evidence Quality: Distinguish Confirmed from Suspected**

- *Capability gained:* Apply a structured evidence classification to each finding: confirmed, probable, or suspected.
- *New theory:* Evidence quality rubric: confirmed (reproduced with observable evidence), probable (strongly suggested by indirect evidence), suspected (hypothesis without direct evidence). Why this matters for security reporting.
- *Tool evolution:* Add `--evidence-level` classification to each `authtest` finding. The classification is determined by the test design, not inferred automatically.
- *Challenge:* For each finding type (unauthenticated access, authorization bypass, path traversal), define what evidence is required to call it `confirmed` vs. `probable`. Document the classification decision in the output.
- *Acceptance criteria:* A finding that was reproduced and observed receives `confirmed`. A finding suggested only by a 200 status without inspecting the body receives `probable`.
- *Enables:* 09.7.

**09.7 — Did the Fix Hold?: Verify Mitigations**

- *Capability gained:* Re-run the authorization test suite after a fix is applied and confirm which findings are resolved.
- *New theory:* Regression verification methodology. Why a fix must be tested, not assumed. How to design a test that would catch a regression.
- *Tool evolution:* Add `--baseline` flag (same pattern as Chapter 08 `webscan`). Compare new results to baseline. Report resolved, new, and unchanged findings.
- *Challenge:* Apply a mitigation to the lab server (provided in the chapter's lab setup). Re-run `authtest`. Verify all previously `confirmed` findings are resolved.
- *Acceptance criteria:* After fixing the authorization bypass, the finding transitions from `confirmed` to `resolved` in the diff report.
- *Verification:* Before/after comparison using two lab server configurations.
- *Enables:* This verification methodology is extended in Chapter 14 (Vulnerability Regression Harness).

#### 8.5 Tool Lifecycle

- **Tool name:** `authtest`
- **Initial capability:** Test endpoints for unauthenticated access.
- **Final scope:** Unauthenticated access testing, role boundary testing, JWT decoding, path traversal testing, evidence classification, baseline comparison.
- **Output contract:** JSON `AuthReport` with findings; each finding has URL, credential set, finding type, evidence level, HTTP evidence, and notes.
- **Important error states:** Connection failure; invalid credential file; malformed JWT; redirect loop.
- **Security invariants:** Credential values never logged. Lab server targets only (enforced by documentation; the tool itself accepts any URL but the chapter makes authorization requirements explicit).
- **Testing expectations:** Local lab server with intentional vulnerabilities. Unit tests for JWT decoding and evidence classification.
- **Downstream consumers:** Chapter 14 (Vulnerability Regression Harness) extends the regression approach. Chapter 18 (Final Engagement).
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Unauthenticated access: expected open vs. protected endpoint.
- Role boundary: lower-privilege access to higher-privilege resource.
- JWT: expired, alg:none, missing exp.
- Path traversal: vulnerable and fixed lab server.
- Baseline comparison: resolved finding.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Methodically tests authorization boundaries in the lab application. Documents each confirmed finding with evidence.
- **Blue Team (Samia):** Reviews Rayhan's findings. Implements and verifies mitigations. Designs regression tests that would catch the same vulnerability in future deployments.
- **Connection:** Chapter 14 (Vulnerability Regression Harness) formalizes the reproduction and fix-verification workflow that `authtest` exercises informally.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Auth vs. authz flowchart | Authentication then authorization | 09.1 |
| HTTP auth mechanism table | Cookie/JWT/Basic/API key | 09.1 |
| JWT anatomy diagram | Header.payload.signature | 09.4 |
| Path traversal normalization diagram | How paths are resolved | 09.5 |
| Evidence quality classification table | Confirmed/probable/suspected | 09.6 |

---

## Phase 4: Look Beneath the Surface

---

### Chapter 10 — Follow the Packets: Build a Packet Inspector

#### 8.1 Chapter Identity

- **Phase:** 4 — Look Beneath the Surface
- **Primary capability:** The learner can parse network packet captures, inspect IP and TCP/UDP headers, filter by protocol, and identify anomalies in captured traffic.
- **Primary tool:** **pktinspect** — a packet inspector that reads PCAP files, parses headers, filters by protocol, and reports anomalies.
- **Intended level:** Intermediate to advanced.
- **Real-world relevance:** Packet capture analysis is essential for incident response, protocol debugging, and understanding what is really on the wire. Security engineers regularly analyze pcap files from network sensors and firewalls.

> **Implementation note:** This chapter uses pcap file parsing rather than live capture to avoid requiring elevated privileges in development. The chapter explains how live capture differs and what privileges it requires on various platforms. An external library for pcap reading is introduced because reimplementing a pcap parser from scratch does not teach packet analysis — it teaches file format parsing.

#### 8.2 Learning Outcomes

By completing Chapter 10, the learner can:

1. Explain the Ethernet frame structure and the IP packet structure.
2. Describe the TCP segment structure including flags and the connection state machine.
3. Parse IP and TCP/UDP headers from a byte slice.
4. Filter captured packets by protocol, address, and port.
5. Reconstruct which TCP segments belong to the same connection (4-tuple).
6. Identify anomalous or malformed packets.
7. Explain the difference between what is observable in a packet capture and what can be inferred.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 01 (byte inspection), Chapter 02 (networking model), Chapter 03 (TCP fundamentals).
- **External dependency:** `github.com/google/gopacket` or equivalent — introduced to handle pcap file reading and packet decoding. The chapter explains why the standard library does not cover this use case.
- **Downstream consumers:** Chapter 11 (TLS Certificate Checker) inspects TLS at the connection level. Chapter 16 (Security Event Detector) may process packet-derived events.

#### 8.4 Subchapter Milestone Plan

**10.1 — The Frame Within a Frame: Understand Packet Structure**

- *Capability gained:* Explain the layered structure of a network packet at the Ethernet/IP/TCP level.
- *New theory:* Ethernet frame: destination MAC, source MAC, EtherType. IP packet: version, IHL, protocol, source IP, destination IP. TCP segment: source port, destination port, sequence number, flags. UDP datagram: source port, destination port, length.
- *Visualizations:* Byte-layout figures for Ethernet header, IPv4 header, TCP header — each annotated with field names, offsets, and sizes. Encapsulation diagram: TCP inside IP inside Ethernet.
- *Tool evolution:* No implementation yet. Theory milestone with figures and an experiment using a pre-provided pcap file and `hexdump`.
- *Challenge:* Using the Byte Inspector from Chapter 01, inspect the first 54 bytes of a provided test pcap's first packet and identify each header field by hand.
- *Acceptance criteria:* Correct identification of source IP, destination IP, source port, destination port, and TCP flags for the first packet.
- *Enables:* 10.2.

**10.2 — Open the File: Read a PCAP and List Packets**

- *Capability gained:* Open a pcap file and print a summary of each packet: timestamp, length, source/destination addresses and ports, protocol.
- *New theory:* PCAP file format (global header + packet records). Why gopacket is introduced (platform-specific pcap reading, raw socket access). `pcapgo` package for file-only reading without libpcap dependency.
- *Tool evolution:* `pktinspect <file.pcap>` prints one line per packet: timestamp, protocol, src → dst, length.
- *Challenge:* Parse and display all packets from a provided test pcap file. For each packet, print: timestamp (RFC 3339), Ethernet/IP/TCP or UDP summary, total length.
- *Constraints:* Read-only on the pcap file. Handle truncated packets gracefully — print a warning, continue.
- *Acceptance criteria:* Reading a known test pcap with N packets produces exactly N output lines (or N - K lines with K warnings for truncated packets).
- *Verification:* Deterministic test pcap file included in the chapter's lab materials.
- *Enables:* 10.3.

**10.3 — Filter Down: Select by Protocol, Address, and Port**

- *Capability gained:* Filter displayed packets by protocol (TCP, UDP, ICMP), source/destination IP, and port.
- *New theory:* BPF filter concepts (not implementation). Why filtering matters for large captures. The 4-tuple as a connection identifier.
- *Tool evolution:* Add `--proto`, `--src`, `--dst`, `--port` flags. Flags may be combined.
- *Challenge:* Implement filter logic in Go (not using BPF). Display only matching packets. Show packet count before and after filtering.
- *Constraints:* Invalid filter values (non-existent protocol name, invalid IP) must produce a clear error before reading the file.
- *Acceptance criteria:* `--proto tcp --port 80` on a mixed pcap shows only TCP port 80 packets.
- *Verification:* Test pcap with known distribution of protocols and ports.
- *Enables:* 10.4.

**10.4 — Which Way Did It Flow?: Reconstruct TCP Connections**

- *Capability gained:* Group packets into TCP connections by their 4-tuple; display connection summaries.
- *New theory:* TCP 4-tuple: (src IP, src port, dst IP, dst port). Connection direction. SYN/SYN-ACK/ACK for handshake. FIN/RST for teardown. Sequence and acknowledgement numbers (conceptual).
- *Visualizations:* Diagram: packets grouped into connection flows. TCP state machine diagram: LISTEN → SYN_SENT → ESTABLISHED → FIN_WAIT → CLOSED.
- *Tool evolution:* Add `--connections` mode. Group packets by 4-tuple. For each connection, show: handshake (yes/no), packet count, byte count, final state (established/reset/incomplete).
- *Challenge:* Implement the grouping and basic state detection. Handle bidirectional flows (treat (A,B) and (B,A) as the same connection).
- *Constraints:* Do not attempt to reassemble application data. Do not claim to reconstruct application payload from packets.
- *Acceptance criteria:* A pcap with 3 distinct TCP connections groups correctly; a connection ending in RST is marked as reset.
- *Enables:* 10.5.

**10.5 — Something Looks Wrong: Detect Packet Anomalies**

- *Capability gained:* Identify and flag anomalous packets: malformed headers, unusual flag combinations, incomplete connections.
- *New theory:* Illegal TCP flag combinations (e.g., SYN+FIN, URG without data). IP header checksum (conceptual, not required to validate). Truncated packets. Retransmissions.
- *Tool evolution:* Add `--anomalies` flag. Report packets with: impossible flag combinations, IP/TCP length inconsistencies, connections with SYN but no SYN-ACK in the capture, RST without prior SYN.
- *Challenge:* Define 5 anomaly rules. Report each flagged packet with the rule name and reason.
- *Constraints:* Anomaly detection must produce a specific named rule per finding. Must not flag all retransmissions as anomalies.
- *Acceptance criteria:* A test pcap with deliberate anomalies (provided) produces the expected anomaly report.
- *Enables:* 10.6.

**10.6 — What Can We Actually Say?: Interpret Evidence Carefully**

- *Capability gained:* Understand and articulate the limitations of packet capture analysis — what can be proven vs. inferred.
- *New theory:* What a packet capture proves (these bytes were observed). What it cannot prove (what was sent before the capture started; application-level intent; whether data was modified in transit). Gaps in captures. Time synchronization issues.
- *Tool evolution:* Add a `--summary` output section that reports: capture file info (timestamp range, total packets, filtered packets, connections, anomalies), and a `notes` section listing what cannot be concluded.
- *Challenge:* Write the summary section. For a capture that shows incomplete connections (SYN but no SYN-ACK), note that the capture may have started after the handshake.
- *Acceptance criteria:* The `--summary` output includes a `limitations` field that lists at least two things that cannot be inferred from the current capture.
- *Verification:* Manual review. Check that the tool does not assert things beyond what the packets demonstrate.
- *Enables:* Chapter 11 (TLS Certificate Checker) and Chapter 16 (Security Event Detector) both require the discipline of evidence-based reporting established here.

#### 8.5 Tool Lifecycle

- **Tool name:** `pktinspect`
- **Initial capability:** List packets from a pcap file.
- **Final scope:** Packet listing with filters, TCP connection reconstruction, anomaly detection, evidence-aware summary.
- **External dependency:** `github.com/google/gopacket/pcapgo` for pcap file reading (no libpcap required for file-only reading).
- **Important error states:** Corrupted pcap file; truncated packet; unsupported link type; filter parse error.
- **Security invariants:** Read-only file access. Live capture not implemented (out of scope; chapter explains how).
- **Testing expectations:** Deterministic test pcap files bundled with the chapter lab materials.
- **Downstream consumers:** Chapter 16 (Security Event Detector) may ingest packet-derived events.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Packet listing: known pcap → expected packet count.
- Filter: each filter type (protocol, IP, port).
- Connection grouping: 3-connection pcap.
- Anomaly detection: crafted test pcap with known anomalies.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Inspects packet captures to understand traffic patterns, identify protocols in use, and detect protocol anomalies that suggest scanning or probing activity.
- **Blue Team (Samia):** Analyzes packet captures from network sensors to reconstruct attack timelines, confirm suspicious connections, and distinguish legitimate from malicious traffic.
- **Connection:** The evidence-based reporting approach (10.6) informs Chapter 16 (Security Event Detector) and Chapter 17 (Incident Investigation Tool).

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Ethernet/IP/TCP byte-layout figures | Header field positions and sizes | 10.1 |
| Encapsulation diagram | Layers inside layers | 10.1 |
| TCP state machine diagram | Connection lifecycle | 10.4 |
| Connection grouping diagram | 4-tuple flows | 10.4 |

---

### Chapter 11 — Catch the Trust Failure: Build a TLS Certificate Checker

#### 8.1 Chapter Identity

- **Phase:** 4 — Look Beneath the Surface
- **Primary capability:** The learner can inspect and validate TLS certificate chains, detect common TLS misconfigurations, and understand the difference between inspecting a certificate and proving a connection is secure.
- **Primary tool:** **tlscheck** — a TLS certificate checker that connects to servers, inspects certificate chains, validates hostname binding, checks expiry, and reports configuration findings.
- **Intended level:** Intermediate to advanced.
- **Real-world relevance:** TLS misconfiguration is one of the most common causes of security failures in deployed services. Certificate expiry, missing chain certificates, weak cipher suites, and hostname mismatch are routinely found in security assessments.

#### 8.2 Learning Outcomes

By completing Chapter 11, the learner can:

1. Explain the TLS handshake and what each side proves to the other.
2. Inspect a server's certificate chain: leaf, intermediate, and root.
3. Verify hostname binding using Subject Alternative Names.
4. Detect expired, not-yet-valid, and soon-to-expire certificates.
5. Identify common TLS configuration weaknesses (weak cipher suites, old protocol versions).
6. Explain the difference between inspecting a certificate and verifying the connection is secure.
7. Distinguish between trust-store validation and manual certificate inspection.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 02 (networking), Chapter 06 (HTTP Inspector used HTTPS as a black box — this chapter explains the layer).
- **Downstream consumers:** Chapter 18 (Final Engagement) includes TLS checking as part of the surface audit.

#### 8.4 Subchapter Milestone Plan

**11.1 — The Handshake: Understand What TLS Establishes**

- *Capability gained:* Explain the TLS handshake sequence and what is established at each step.
- *New theory:* TLS 1.2 vs. TLS 1.3 handshakes. ClientHello, ServerHello, Certificate, CertificateVerify, Finished. What the handshake proves. Symmetric key derivation (conceptual). Forward secrecy.
- *Visualizations:* TLS 1.3 handshake sequence diagram. Table: TLS 1.2 vs. TLS 1.3 differences relevant to security.
- *Tool evolution:* No implementation yet — theory milestone with a lab experiment using `openssl s_client` or Go TLS dial.
- *Challenge:* Using `tls.Dial` in a Go program, connect to a local TLS server and print the negotiated TLS version and cipher suite.
- *Enables:* 11.2.

**11.2 — The Certificate Chain: Leaf, Intermediate, Root**

- *Capability gained:* Inspect the full certificate chain presented by a server.
- *New theory:* Certificate chain structure. How a client verifies a chain. Trust anchors (root CAs). The role of intermediate CAs. Chain ordering. A missing intermediate causes validation failure even if the leaf is valid.
- *Visualizations:* Certificate chain diagram: leaf ← signed by intermediate ← signed by root (in trust store). Table: certificate fields → what they mean.
- *Tool evolution:* `tlscheck <host:port>` connects, retrieves the certificate chain, prints each certificate: subject, issuer, not before, not after, serial number, signature algorithm.
- *Challenge:* Display the chain in order (leaf first). Flag if the chain is incomplete (root not in chain, which is normal; but missing intermediate is a problem).
- *Constraints:* Use the system trust store. Must not skip verification. Must not use `InsecureSkipVerify`.
- *Acceptance criteria:* Against a local test TLS server with a self-signed cert (leaf only, no chain), a warning is shown that the chain cannot be verified by the system trust store.
- *Verification:* Local TLS server (using `crypto/tls` with a test certificate) generated in the chapter's lab setup.
- *Enables:* 11.3.

**11.3 — Does the Name Match?: Hostname Validation**

- *Capability gained:* Verify that the server's certificate matches the hostname requested, using Subject Alternative Names.
- *New theory:* SAN (Subject Alternative Name) vs. CN. Wildcard certificates. How hostname validation works. What a mismatch means for the client.
- *Visualizations:* Annotated certificate showing CN and SAN fields. Table: valid match scenarios vs. invalid match scenarios.
- *Tool evolution:* Add hostname validation report: which SANs are present, which matches the requested hostname, and a clear verdict.
- *Challenge:* Report: hostname matches (which SAN), partial match (wildcard covers hostname), or mismatch. Mismatch must produce a non-zero exit code.
- *Constraints:* Must use the actual server hostname, not the IP address, for SAN validation.
- *Acceptance criteria:* A certificate for `*.example.com` is correctly reported as matching `sub.example.com` but not `example.com` or `sub.sub.example.com`.
- *Verification:* Unit test with certificate templates.
- *Enables:* 11.4.

**11.4 — Is It Still Valid?: Expiry and Validity Window**

- *Capability gained:* Check certificate validity period and classify: valid, expired, not yet valid, or expiring soon.
- *New theory:* `NotBefore`, `NotAfter`. The risk of soon-to-expire certificates. Certificate rotation strategies (conceptual). Why expiry monitoring matters operationally.
- *Tool evolution:* Report: days until expiry (or days since expiry). Thresholds: <30 days = warning; expired = critical; >365 days = informational (possibly long-lived root).
- *Challenge:* Implement expiry classification using `time.Now()` relative to `NotAfter`. Report the expiry date in human-readable form alongside the classification.
- *Acceptance criteria:* An expired test certificate is classified as `critical`. A certificate with 15 days remaining is classified as `warning`.
- *Verification:* Test certificates with controlled `NotAfter` dates.
- *Enables:* 11.5.

**11.5 — What's It Using?: Detect TLS Configuration Weaknesses**

- *Capability gained:* Report the negotiated TLS version and cipher suite; flag deprecated configurations.
- *New theory:* TLS version deprecation: TLS 1.0 and 1.1 deprecated (RFC 8996). Weak cipher suites: RC4, DES, 3DES, export ciphers, CBC-mode without AEAD. Forward secrecy and ECDHE. Why cipher suite selection matters.
- *Visualizations:* Table: TLS version → security status → recommendation. Table: cipher suite properties → acceptable/deprecated.
- *Tool evolution:* Add negotiated TLS version and cipher suite to the report. Flag TLS 1.0, 1.1, and weak cipher suites as findings.
- *Challenge:* Report the negotiated protocol version (from `tls.ConnectionState`) and cipher suite. Flag any deprecated protocol or cipher.
- *Constraints:* Cannot force the server to negotiate a specific version for the report — report what is actually negotiated. Note that the client's supported versions affect what is negotiated.
- *Acceptance criteria:* A local TLS server configured to use TLS 1.2 with a strong cipher reports correctly. Explaining in the output what the tool can and cannot control about the negotiation.
- *Verification:* Local TLS servers with configurable versions and cipher suites.
- *Enables:* 11.6.

**11.6 — What Does This Actually Prove?: Interpret Results Carefully**

- *Capability gained:* Understand and articulate what TLS certificate validation proves and what it does not.
- *New theory:* What certificate validation proves: the server controls the private key for this certificate, and a trusted CA verified the domain. What it does not prove: the application behind the TLS layer is secure; the certificate authority is infallible; the negotiated cipher suite has no weaknesses.
- *Tool evolution:* Add a `--summary` section with a `limitations` field. Produce a structured JSON report.
- *Challenge:* Write the summary. Explicitly state: "Certificate chain valid" does not mean "application is secure." "Cipher suite accepted" does not mean "no known weaknesses."
- *Acceptance criteria:* The report includes both findings and a limitations section.
- *Enables:* Chapter 18 (Final Engagement) includes TLS checking as part of surface audit.

#### 8.5 Tool Lifecycle

- **Tool name:** `tlscheck`
- **Initial capability:** Connect and display certificate chain.
- **Final scope:** Chain inspection, hostname validation, expiry classification, TLS version/cipher suite report, evidence-aware summary.
- **Output contract:** JSON `TLSReport` with certificate chain array, hostname match verdict, expiry classification, protocol findings, limitations.
- **Security invariants:** Must not use `InsecureSkipVerify`. System trust store only. `--insecure` flag may be added for inspection of misconfigured servers but must print a prominent warning.
- **Testing expectations:** Deterministic test certificates generated in lab setup.
- **Downstream consumers:** Chapter 18 (Final Engagement).
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Chain: complete chain, incomplete chain.
- Hostname: match, wildcard match, mismatch.
- Expiry: expired, soon-to-expire, valid.
- TLS version: TLS 1.2 and TLS 1.3.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Identifies certificate misconfigurations that could be exploited (expired cert, hostname mismatch, weak cipher). Tests whether misconfiguration affects trust chain.
- **Blue Team (Samia):** Uses `tlscheck` to monitor certificate expiry across services. Verifies that TLS configuration meets organizational requirements. Detects unexpected certificate changes.
- **Connection:** Chapter 08 (`webscan`) checks HTTPS enforcement at the HTTP layer. Chapter 11 (`tlscheck`) inspects the TLS layer beneath it.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| TLS 1.3 handshake sequence diagram | What TLS establishes | 11.1 |
| Certificate chain diagram | Leaf → intermediate → root | 11.2 |
| SAN matching table | Valid vs. invalid hostname matches | 11.3 |
| TLS version and cipher suite table | Deprecated vs. recommended | 11.5 |

---

### Chapter 12 — See Inside the Process: Build a System Diagnostics Tool

#### 8.1 Chapter Identity

- **Phase:** 4 — Look Beneath the Surface
- **Primary capability:** The learner can inspect running processes, their open file descriptors, file permissions, environment variables, and resource limits using Go's OS interfaces.
- **Primary tool:** **sysdiag** — a system diagnostics tool that inspects process state, file permissions, and environment from a security perspective.
- **Intended level:** Intermediate to advanced.
- **Real-world relevance:** Process and file system inspection is central to host-based security: identifying credential exposure in environment variables, detecting world-writable sensitive files, finding processes with unexpected open sockets, and verifying privilege levels.

> **Platform note:** Some features are Linux-specific. The chapter clearly identifies platform-dependent behavior and provides alternatives or explanations for macOS and Windows where relevant.

#### 8.2 Learning Outcomes

By completing Chapter 12, the learner can:

1. List running processes and their attributes using Go's `os` and OS-specific interfaces.
2. List the open file descriptors of a process.
3. Inspect file permissions including setuid/setgid bits.
4. Read and classify environment variables from a security perspective.
5. Query process resource limits (`ulimit`-style).
6. Identify security-relevant anomalies in process and file state.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 02 (network concepts for socket inspection), Chapter 01 (byte representation for permission bit decoding).
- **Platform dependency:** Significant Linux-specific behavior in `/proc`. macOS uses different interfaces. The chapter specifies which subchapters are portable and which are Linux-focused.
- **Downstream consumers:** Chapter 16 (Security Event Detector) may analyze system events produced by sysdiag-style inspection.

#### 8.4 Subchapter Milestone Plan

**12.1 — Who's Running?: List Processes**

- *Capability gained:* List running processes with PID, PPID, user, and command name.
- *New theory:* Process as an OS abstraction. PID, PPID. `os.Getpid`, `/proc` filesystem (Linux). `ps`-equivalent using Go. Privilege and effective user ID.
- *Tool evolution:* `sysdiag ps` lists processes. Linux: read `/proc`. macOS: use `os/exec` to call `ps` and parse output (acceptable wrapper for this milestone).
- *Challenge:* Display PID, PPID, user, and command. Flag processes running as root (or UID 0) that have unexpected names.
- *Acceptance criteria:* The current process appears in the list with the correct PID.
- *Verification:* Start a known test process, verify it appears.
- *Enables:* 12.2.

**12.2 — What Files Does It Have Open?: Inspect File Descriptors**

- *Capability gained:* List open file descriptors for a given PID (Linux `/proc/PID/fd`).
- *New theory:* File descriptors: files, sockets, pipes. `/proc/PID/fd` symlinks. How open sockets appear as file descriptors. stdin/stdout/stderr (fd 0, 1, 2).
- *Tool evolution:* `sysdiag fds --pid <PID>` lists open file descriptors: fd number, type (file/socket/pipe), and target path or socket endpoint.
- *Challenge:* Categorize each fd as: regular file, socket, pipe, device, or other. For sockets, display the local address if readable from `/proc/net`.
- *Constraints:* Linux only for this subchapter. Clearly indicate when run on another platform.
- *Acceptance criteria:* Running against the current process shows at least fd 0, 1, 2 and any open files the test opens.
- *Enables:* 12.3.

**12.3 — Who Can Touch It?: Inspect File Permissions**

- *Capability gained:* Display file permissions including setuid, setgid, and sticky bits, and identify security-relevant findings.
- *New theory:* Unix permission model: user/group/other bits. setuid bit: executable runs as file owner. setgid bit: similar for group. Sticky bit on directories. Why setuid root binaries are a security concern.
- *Visualizations:* Permission bit table: `rwxrwxrwx` annotated with octal values and setuid position. Examples of security-relevant permission patterns.
- *Tool evolution:* `sysdiag perms <path>` displays permissions. `sysdiag perms --find-setuid /usr/bin` scans a directory tree for setuid binaries.
- *Challenge:* Decode the mode bits and display in symbolic (rwxr-xr-x) and octal formats. Flag setuid root binaries found in the directory scan.
- *Acceptance criteria:* A test file with `chmod 4755` (setuid) is correctly identified and flagged.
- *Verification:* Create test files with known permissions in a temp directory.
- *Enables:* 12.4.

**12.4 — Secrets in the Environment: Inspect Environment Variables**

- *Capability gained:* List environment variables from the current process and classify security-relevant ones.
- *New theory:* Environment variables as a credential store: why this is risky. Common sensitive variable names: `*_KEY`, `*_SECRET`, `*_TOKEN`, `*_PASSWORD`, `DATABASE_URL`. Inheritance of environment variables across process forks.
- *Tool evolution:* `sysdiag env` lists all environment variables. `--classify` flag categorizes: likely-credential (name matches known patterns), path-related, or general.
- *Challenge:* Classify each variable by name pattern. For likely-credential variables, show only the first 4 characters of the value followed by `[redacted]` in the classified output.
- *Constraints:* Do not show full values of likely-credential variables in default output.
- *Acceptance criteria:* `AWS_SECRET_ACCESS_KEY=abc123` is classified as `likely-credential` and its value is displayed as `abc1[redacted]`.
- *Enables:* 12.5.

**12.5 — How Many Resources?: Check Resource Limits**

- *Capability gained:* Query and display process resource limits (open files, memory, CPU time).
- *New theory:* `ulimit` system call equivalents in Go (`syscall.Getrlimit`). Soft vs. hard limits. Why open file limit matters for servers. Memory limits and OOM.
- *Tool evolution:* `sysdiag limits` displays current soft and hard limits for: open files, virtual memory, CPU time, max processes.
- *Challenge:* Display each limit with soft and hard values. Flag when soft limit is at the system default for a server process (e.g., 1024 open files is likely too low for a production service).
- *Constraints:* Linux/macOS only. Use `syscall.Getrlimit`.
- *Acceptance criteria:* Limits are displayed correctly. Comparison against `ulimit -a` output.
- *Enables:* 12.6.

**12.6 — Correlate the Findings: Security-Oriented Report**

- *Capability gained:* Produce a structured security-oriented system diagnostics report correlating process, permission, environment, and limit findings.
- *Tool evolution:* `sysdiag report` runs all subcommands and aggregates into a structured JSON report.
- *Challenge:* The report must: list security-relevant findings (setuid binaries, credential-like env vars, low open-file limits), separate findings by severity, and include a limitations section.
- *Acceptance criteria:* A report generated on a known system state matches expected findings for that state.
- *Enables:* Chapter 16 (Security Event Detector) can analyze system state events from sysdiag output.

#### 8.5 Tool Lifecycle

- **Tool name:** `sysdiag`
- **Initial capability:** List processes.
- **Final scope:** Process listing, file descriptor inspection, permission analysis, environment classification, resource limits, aggregated report.
- **Platform:** Linux primary; macOS partial. Document differences.
- **Security invariants:** Environment redaction of credential-like values in default output. Read-only operations.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Process listing: current process appears.
- File descriptors: test files opened in test.
- Permissions: known test files.
- Environment: controlled env in test.
- Resource limits: compare against system defaults.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Inspects process environment for credential exposure. Finds setuid binaries for privilege escalation research. Identifies processes with unexpected network sockets.
- **Blue Team (Samia):** Audits servers for setuid binaries, over-privileged processes, and credential exposure in environment variables. Verifies resource limits are appropriate for the service load.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Unix permission bit table | rwx bits, setuid, setgid, sticky | 12.3 |
| `/proc` filesystem structure diagram | What each directory contains | 12.1 |
| Environment variable sensitivity table | Patterns that suggest credentials | 12.4 |

---

## Phase 5: Find and Fix Weaknesses

---

### Chapter 13 — Break Your Own Parser: Build a Fuzz Testing Tool

#### 8.1 Chapter Identity

- **Phase:** 5 — Find and Fix Weaknesses
- **Primary capability:** The learner can build a fuzzing harness, generate and mutate inputs, detect crashes and panics in a target parser, and use Go's native fuzzing to drive discovery.
- **Primary tool:** **fuzzlab** — a fuzzing harness that generates mutated inputs against a controlled target parser, captures failures, and preserves reproducing cases.
- **Intended level:** Advanced.
- **Real-world relevance:** Parsing vulnerabilities are among the most common sources of security bugs. Fuzzing is the most effective automated technique for finding them. Every security engineer should understand how to fuzz a parser they have written.

#### 8.2 Learning Outcomes

By completing Chapter 13, the learner can:

1. Explain what fuzzing is and why it finds bugs that unit tests miss.
2. Implement a target parser with at least one known latent bug (for the lab).
3. Write a fuzzing harness that generates and mutates inputs.
4. Detect panics, unexpected errors, and crashes in the target.
5. Use `go test -fuzz` to leverage Go's native coverage-guided fuzzer.
6. Reproduce a finding with a minimal input.
7. Write a regression test that verifies the bug is fixed and does not recur.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 01 (byte manipulation), Chapter 03 (testing patterns and verification habits).
- **Downstream consumers:** Chapter 14 (Vulnerability Regression Harness) directly extends the regression approach established here.

#### 8.4 Subchapter Milestone Plan

**13.1 — The Target: Build a Parser to Break**

- *Capability gained:* Implement a simple structured-data parser (e.g., a minimal HTTP-like header parser or a custom binary format) that will serve as the fuzzing target.
- *New theory:* What makes a parser vulnerable: missing length checks, incorrect offset arithmetic, unchecked input assumptions. Why parsers are common attack surfaces.
- *Tool evolution:* Write the target parser as a Go package with a `Parse(input []byte) (Result, error)` interface.
- *Challenge:* Implement the parser according to a provided specification. The specification intentionally allows at least one boundary condition that will cause a panic.
- *Constraints:* The parser must be a real implementation — not a toy that trivially panics or trivially succeeds on all input. The flaw must be a realistic boundary condition.
- *Acceptance criteria:* The parser passes a suite of valid-input tests provided in the chapter. The panic flaw is not yet found — that is the fuzzer's job.
- *Enables:* 13.2.

**13.2 — Simple Mutations: Generate Bad Inputs**

- *Capability gained:* Write a mutation-based input generator that creates variations of valid input.
- *New theory:* Mutation strategies: bit flip, byte insertion, byte deletion, boundary values (0, 255, max length), random replacement. Why coverage-guided fuzzing is more effective than random mutation (conceptual).
- *Tool evolution:* `fuzzlab mutate --input <valid_input_file> --count 1000` generates 1000 mutations and saves them.
- *Challenge:* Implement at least 5 distinct mutation strategies. Each mutation must produce a syntactically plausible (not obviously garbage) input most of the time.
- *Enables:* 13.3.

**13.3 — Run and Watch: Execute Mutations Against the Target**

- *Capability gained:* Feed generated inputs to the parser, catch panics, record failures.
- *New theory:* `recover()` in Go to catch panics. What constitutes a failure: panic, unexpected error (not the specified error for invalid input), infinite loop (use timeout).
- *Tool evolution:* `fuzzlab run --target parser --corpus mutations/` runs each mutation through the parser, records failures with the input that triggered them.
- *Challenge:* Capture panics using `defer/recover`. Record the failing input to a file. Do not stop on first failure — report all distinct failures.
- *Constraints:* Each parser call runs in a goroutine with a timeout. A parser that hangs for more than 1 second is treated as a failure.
- *Acceptance criteria:* Running the mutation suite against the intentionally flawed parser discovers the panic. The failing input is saved.
- *Enables:* 13.4.

**13.4 — Let Go Help: Use Native Go Fuzzing**

- *Capability gained:* Write a `FuzzX` function and run `go test -fuzz` to use coverage-guided fuzzing.
- *New theory:* Go's native fuzzing (`go test -fuzz`): seed corpus, coverage guidance, corpus entries. How `go test -fuzz` differs from random mutation (it observes which inputs exercise new code paths). `testdata/fuzz/` corpus directory.
- *Tool evolution:* Write a `FuzzParseHeader(f *testing.F)` test function. Seed it with valid inputs. Run `go test -fuzz=FuzzParseHeader -fuzztime=30s`.
- *Challenge:* The native fuzzer must find a new failure (or confirm the one found in 13.3) within 60 seconds. The failing corpus entry must be committed to `testdata/fuzz/`.
- *Acceptance criteria:* `go test -fuzz=FuzzParseHeader` terminates with a found failure. The failure is reproducible with `go test -run=FuzzParseHeader/failing_case`.
- *Verification:* Run `go test -run=FuzzParseHeader/failing_case` to reproduce deterministically.
- *Enables:* 13.5.

**13.5 — Minimize and Understand: Isolate the Root Cause**

- *Capability gained:* Reduce a triggering input to its minimal form. Identify the root cause of the failure.
- *New theory:* Input minimization: why a 1-byte change is more useful than a 1000-byte triggering input. Root cause analysis: what assumption in the code is violated by the minimal input.
- *Tool evolution:* Add `fuzzlab minimize --input failing.bin --target parser` to progressively reduce the triggering input.
- *Challenge:* Manually or programmatically reduce the failing input to the smallest input that still triggers the panic. Describe the root cause in a written analysis.
- *Acceptance criteria:* The minimal input is no larger than 10 bytes for the chapter's parser. Root cause is correctly identified.
- *Enables:* 13.6.

**13.6 — Fix It and Lock It Down: Regression Testing**

- *Capability gained:* Fix the bug, verify the fix, and add the triggering input as a permanent regression test.
- *New theory:* What makes a good regression test. How the `testdata/fuzz/` corpus serves as regression inputs. Why the fix must address the root cause, not just the symptom.
- *Tool evolution:* Fix the parser. The minimal input must no longer trigger a panic. The fix must pass all previously passing tests.
- *Challenge:* Fix the parser and verify: the minimal input no longer panics; all valid-input tests still pass; `go test -fuzz` finds no new panics in 30 seconds (no guarantee, but a good signal).
- *Acceptance criteria:* `go test -run=FuzzParseHeader/failing_case` passes after the fix. All original valid-input tests pass. Root cause is documented in a code comment.
- *Enables:* Chapter 14 (Vulnerability Regression Harness) formalizes the reproduction and regression process.

#### 8.5 Tool Lifecycle

- **Tool name:** `fuzzlab`
- **Includes:** Target parser package, mutation generator, run harness, native fuzz test.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Valid-input test suite for the target parser.
- Mutation-based fuzzer finds a failure.
- Native Go fuzzer reproduces the failure.
- Fix: all tests pass; failing input no longer panics.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Uses fuzzing to discover parser vulnerabilities before an attacker does. Fuzzing is a proactive offense-informed defensive technique.
- **Blue Team (Samia):** Adds fuzz-found failures to the CI regression suite. Establishes a policy that parsers must pass a fuzz test before deployment.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Mutation strategy table | Types of mutations and their effects | 13.2 |
| Coverage-guided fuzzing diagram | How Go's fuzzer explores code paths | 13.4 |
| Input minimization flowchart | How to reduce a triggering input | 13.5 |

---

### Chapter 14 — Reproduce the Bug: Build a Vulnerability Regression Harness

#### 8.1 Chapter Identity

- **Phase:** 5 — Find and Fix Weaknesses
- **Primary capability:** The learner can reproduce a known vulnerability from a minimal description, isolate the preconditions, verify a fix, and design a regression test that prevents recurrence.
- **Primary tool:** **repro** — a structured reproduction and regression harness for controlled vulnerability verification.
- **Intended level:** Advanced.
- **Real-world relevance:** Reproducing reported vulnerabilities is a critical skill. A reproducible case is the foundation of root-cause analysis, patch verification, and regression prevention. Security teams that cannot reproduce reported bugs cannot know whether a fix is effective.

#### 8.2 Learning Outcomes

By completing Chapter 14, the learner can:

1. Reproduce a controlled vulnerability given a description and a vulnerable target.
2. Identify the minimum preconditions required to trigger the vulnerability.
3. Distinguish a proof of concept from proof of exploitability.
4. Apply a patch and verify that the reproduction test now fails (the bug is fixed).
5. Design a regression test that would catch the bug if it reappeared.
6. Write a structured vulnerability report with evidence.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 09 (authorization testing methodology), Chapter 13 (fuzzing, panic capture, and regression testing).
- **Lab requirement:** A controlled vulnerable Go server included in the chapter's lab setup. The vulnerability is specified; the learner must reproduce it.
- **Downstream consumers:** Chapter 18 (Final Engagement) includes proof-of-concept and regression verification.

#### 8.4 Subchapter Milestone Plan

**14.1 — What Does "Reproduce" Mean?: Define the Standard**

- *Capability gained:* Understand what a reproducible case requires: preconditions, steps, expected result, actual result.
- *New theory:* Minimal Reproducible Example (MRE). Preconditions vs. environmental assumptions. Why "it happens sometimes" is not a reproducible case.
- *Tool evolution:* Define a `Reproduction` struct: ID, title, preconditions, steps, expected behavior, observed behavior, evidence.
- *Challenge:* Given a provided vulnerability report, extract and document the preconditions, steps, and expected vs. observed behavior.
- *Enables:* 14.2.

**14.2 — Find the Trigger: Identify Preconditions**

- *Capability gained:* Systematically narrow the preconditions required to trigger the vulnerability.
- *New theory:* Precondition isolation: binary search across configuration space. One-variable-at-a-time testing. Why a large precondition set makes a bug harder to fix safely.
- *Tool evolution:* Add a `repro check --preconditions preconditions.yaml` command that verifies each precondition against the lab environment.
- *Challenge:* For the chapter's provided vulnerability, determine the minimum preconditions: server configuration, user role, request path, and input value.
- *Acceptance criteria:* The reproduction triggers reliably when all preconditions are met and does not trigger when any one precondition is absent.
- *Enables:* 14.3.

**14.3 — Make It Minimal: Write the Simplest Reproducer**

- *Capability gained:* Write the smallest program or test that reliably triggers the vulnerability.
- *New theory:* Minimal test case discipline: strip everything not required to trigger the bug. Why smaller is better for bug reports, fixing, and regression testing.
- *Tool evolution:* Write a Go test `TestReproduction_<ID>` that sets up preconditions, sends the triggering input, and asserts the expected-but-incorrect behavior.
- *Challenge:* The test must: set up the lab server in a known state; send the triggering request; assert that the response demonstrates the vulnerability (not just that a request failed).
- *Constraints:* Test must be deterministic. Must not depend on network timing or external services.
- *Acceptance criteria:* `go test -run TestReproduction_<ID>` passes (demonstrating the bug is present). After the fix is applied, the test must fail (demonstrating the fix is effective).
- *Enables:* 14.4.

**14.4 — Understand the Cause: Root-Cause Analysis**

- *Capability gained:* Identify the code-level root cause of the vulnerability.
- *New theory:* Root cause vs. symptom. Why fixing the symptom without addressing the root cause leads to recurrence. Trust boundary violations as a class of root causes.
- *Challenge:* Locate the specific code in the vulnerable server that is responsible for the behavior. Describe the root cause in one or two sentences. Distinguish the root cause from the consequences.
- *Acceptance criteria:* The root cause statement correctly identifies the code location and the violated assumption.
- *Enables:* 14.5.

**14.5 — Verify the Fix: Does It Hold?**

- *Capability gained:* Apply a patch to the vulnerable server and verify that the reproduction test now fails (correctly).
- *New theory:* A fix is verified when the reproduction test fails with the fixed server. The fix is insufficient if related tests now fail for a different reason. Partial fixes and their risks.
- *Tool evolution:* Add `repro verify --fix-description "..."` command that runs the reproduction test against the patched server and reports the result.
- *Challenge:* Apply the provided patch to the lab server. Run the reproduction test. Verify it fails (bug is fixed). Run all other tests — verify they still pass.
- *Acceptance criteria:* Reproduction test fails after patch. All previously passing tests pass.
- *Enables:* 14.6.

**14.6 — Prevent Recurrence: Design the Regression Test**

- *Capability gained:* Design a regression test that would automatically catch the bug if it reappeared in a future commit.
- *New theory:* Regression test design: test the fix, not the symptom. Testing at the layer of the root cause. Why a full reproduction test is better than a simple smoke test.
- *Tool evolution:* Promote the reproduction test to a permanent regression test in the test suite. Document why this test exists in a comment.
- *Challenge:* The regression test must: express the security invariant (what must be true), be independent of any specific implementation detail, and fail clearly if the invariant is violated.
- *Acceptance criteria:* The regression test is part of the test suite and will be run by `go test ./...`.
- *Enables:* 14.7.

**14.7 — Write the Report: Evidence-Based Findings**

- *Capability gained:* Produce a structured vulnerability report suitable for sharing with a development team.
- *New theory:* Vulnerability report structure: title, severity, affected component, preconditions, reproduction steps, evidence (screenshots/logs/test output), root cause, recommended fix, regression test reference.
- *Tool evolution:* `repro report --id <ID>` generates a structured Markdown report from the stored reproduction data.
- *Challenge:* Produce a report for the chapter's vulnerability. The report must clearly distinguish confirmed findings from inferences.
- *Acceptance criteria:* The report contains all required sections. Evidence is referenced as reproducible (pointing to the test).

#### 8.5 Tool Lifecycle

- **Tool name:** `repro`
- **Initial capability:** Structured reproduction case definition.
- **Final scope:** Precondition checking, minimal reproduction test, root-cause documentation, fix verification, regression test promotion, structured report generation.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Reproduction test: passes on vulnerable server, fails on patched server.
- Regression test: part of `go test ./...`.
- All previously passing tests pass after patch.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Produces the reproduction case and root-cause analysis.
- **Blue Team (Samia):** Reviews Rayhan's report, applies the patch, verifies the fix, and promotes the regression test to CI.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Precondition isolation diagram | Binary search across configuration space | 14.2 |
| Vulnerability report structure table | Required sections and their purpose | 14.7 |

---

### Chapter 15 — Spot the Cryptographic Mistake: Build a Crypto Audit Tool

#### 8.1 Chapter Identity

- **Phase:** 5 — Find and Fix Weaknesses
- **Primary capability:** The learner can identify cryptographic misuse — weak algorithms, improper random number generation, insecure password storage, and misconfigured TLS — by inspecting code and configuration.
- **Primary tool:** **cryptoaudit** — a tool that inspects Go source code and configuration files for known cryptographic misuse patterns.
- **Intended level:** Advanced.
- **Real-world relevance:** Cryptographic mistakes are silent failures: the code runs, tests pass, but the security property is absent. Recognizing and auditing cryptographic usage is a critical skill for security engineers reviewing code.

> **Important scope note:** The goal is to recognize, audit, and understand cryptographic mechanisms and their failure modes. The learner must not implement replacement cryptographic algorithms. Go's `crypto` standard library provides the correct implementations; this chapter teaches when and how to use them correctly.

#### 8.2 Learning Outcomes

By completing Chapter 15, the learner can:

1. Explain the difference between cryptographic hash functions, MACs, and digital signatures.
2. Identify when `math/rand` is used instead of `crypto/rand` and explain the security consequence.
3. Recognize insecure password storage (plain hash vs. adaptive hash with salt).
4. Identify weak or deprecated algorithms: MD5, SHA-1 for security purposes, ECB mode, static IV.
5. Explain what a timing side-channel is and recognize code patterns that introduce one.
6. Inspect TLS configuration in Go code for deprecated protocol versions and weak cipher suites.
7. Produce an evidence-based crypto audit report.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 01 (byte representation), Chapter 11 (TLS configuration).
- **Downstream consumers:** Chapter 18 (Final Engagement) includes a crypto audit as part of the assessment.

#### 8.4 Subchapter Milestone Plan

**15.1 — The Cryptographic Landscape: A Practitioner's Map**

- *Capability gained:* Explain the major categories of cryptographic primitive and when each is appropriate.
- *New theory:* Hash functions (one-way, deterministic). MACs (keyed, authentication). Symmetric encryption (confidentiality). Asymmetric encryption (key exchange, signatures). Password hashing (slow, salted). CSPRNG vs. PRNG.
- *Visualizations:* Decision flowchart: "Which primitive do I need?" Table: use case → correct primitive → Go package.
- *Challenge:* Given 10 use cases (store password, generate session token, sign a message, etc.), identify the correct primitive for each. Written exercise, no code.
- *Enables:* 15.2.

**15.2 — Weak Randomness: Detect `math/rand` in Security Contexts**

- *Capability gained:* Identify uses of `math/rand` in security-sensitive contexts and explain why `crypto/rand` is required.
- *New theory:* Pseudo-random vs. cryptographically secure. Why `math/rand` is predictable. Contexts requiring unpredictability: session tokens, API keys, nonces, IV/salt generation.
- *Tool evolution:* `cryptoaudit scan --dir <directory>` scans Go source files for `math/rand` usage. Reports each occurrence with file, line, and a description of the risk.
- *Challenge:* Use `go/ast` or `regexp`-based scanning to detect `math/rand` imports and usages. Classify each usage: definitely security-sensitive, possibly security-sensitive, or probably benign.
- *Constraints:* AST-based scanning preferred over regex for accuracy. Flag usages that seed with time-based values as high risk.
- *Acceptance criteria:* A provided test Go file with known `math/rand` usages in security contexts is correctly identified.
- *Verification:* Unit tests with known-good and known-bad Go source snippets.
- *Enables:* 15.3.

**15.3 — Dangerous Algorithms: Detect MD5, SHA-1, ECB, Static IV**

- *Capability gained:* Identify uses of deprecated or dangerous cryptographic algorithms in code.
- *New theory:* MD5 and SHA-1: collision vulnerabilities; acceptable for checksums, not for security signatures. ECB mode: deterministic encryption leaks plaintext patterns. Static IV in CBC/GCM: nonce reuse catastrophic for GCM. AES-CBC without authentication: padding oracle risk.
- *Visualizations:* ECB mode pattern preservation diagram (penguin image example — reference without including image). Nonce reuse impact in GCM.
- *Tool evolution:* Extend the scanner to detect `md5.New`, `sha1.New`, `aes.NewCBCEncrypter` with static IV, and `cipher.NewGCM` without fresh nonce per call.
- *Challenge:* Add detection rules for each dangerous pattern. Report with severity (high for ECB/static-IV, medium for MD5 in security context).
- *Acceptance criteria:* A test file using `crypto/md5` for a password hash is flagged. A correctly used `crypto/sha256` is not flagged.
- *Enables:* 15.4.

**15.4 — Storing Passwords: Identify Weak Password Hashing**

- *Capability gained:* Detect password storage that uses a plain hash instead of an adaptive, salted password hashing function.
- *New theory:* Password hashing requirements: slow, salted, one-way. bcrypt, argon2, scrypt vs. SHA-256. Why speed is the enemy of password hashing.
- *Tool evolution:* Add detection for patterns: `sha256.Sum256([]byte(password))`, `md5.Sum(...)` used as a password store, absence of salt concatenation. Recommend `golang.org/x/crypto/bcrypt` or `argon2`.
- *Challenge:* Correctly classify: bcrypt usage (safe), SHA-256 without salt (unsafe), SHA-256 with random salt (medium — better, but still not adaptive).
- *Acceptance criteria:* Test file with all three patterns produces correct classifications.
- *Enables:* 15.5.

**15.5 — Timing Side-Channels: Recognize Dangerous Comparisons**

- *Capability gained:* Identify byte-by-byte comparison of secrets (using `==` or loops) and explain the timing side-channel risk.
- *New theory:* Timing side-channels: how comparison time leaks information about how many bytes match. `subtle.ConstantTimeCompare`. When constant-time comparison is required (MAC verification, API key comparison).
- *Tool evolution:* Add detection for string/byte equality checks on values that appear to be tokens, MACs, or keys. Suggest `crypto/subtle.ConstantTimeCompare`.
- *Challenge:* Detect `hmac == receivedHmac` or `bytes.Equal(mac, received)` in contexts where the value appears to be a security token or MAC. `bytes.Equal` is not constant time.
- *Acceptance criteria:* A test file using `==` to compare an HMAC is flagged. A file using `subtle.ConstantTimeCompare` is not flagged.
- *Enables:* 15.6.

**15.6 — TLS Configuration: Audit Server and Client Config**

- *Capability gained:* Inspect `tls.Config` settings in Go code for deprecated protocols and weak defaults.
- *New theory:* `tls.Config`: `MinVersion`, `MaxVersion`, `CipherSuites`, `InsecureSkipVerify`. Why `InsecureSkipVerify: true` is almost always wrong. Default TLS behavior in Go versions ≥ 1.18 (reasonable defaults). When to specify `MinVersion` explicitly.
- *Tool evolution:* Add detection for: `InsecureSkipVerify: true`, `MinVersion` set below TLS 1.2, explicit weak cipher suites in `CipherSuites`.
- *Acceptance criteria:* Test file with `InsecureSkipVerify: true` is flagged as critical. File with `MinVersion: tls.VersionTLS12` is reported as acceptable.
- *Enables:* 15.7.

**15.7 — The Audit Report: Evidence-Based Findings**

- *Capability gained:* Produce a structured, severity-classified audit report for a codebase.
- *Tool evolution:* Aggregate all scanner findings into a JSON report with: file, line, rule, severity (critical/high/medium/low), finding description, recommendation.
- *Challenge:* Run `cryptoaudit scan --dir .` against a provided vulnerable sample project. Report must include all findings from rules 15.2–15.6.
- *Acceptance criteria:* JSON output passes schema validation. Each finding includes file, line, severity, and recommendation.

#### 8.5 Tool Lifecycle

- **Tool name:** `cryptoaudit`
- **Initial capability:** Scan for `math/rand`.
- **Final scope:** Scan for weak randomness, dangerous algorithms, weak password hashing, timing side-channels, TLS config weaknesses. Produce severity-classified JSON report.
- **External dependency:** `go/ast` from the standard library (no external library needed for AST parsing of Go code).
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Unit tests for each detection rule using inline Go source snippets.
- Integration test with a provided vulnerable sample project.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Identifies cryptographic weaknesses that could be exploited: weak tokens, predictable nonces, timing attacks.
- **Blue Team (Samia):** Runs `cryptoaudit` as part of code review. Integrates it into CI as a mandatory check for new code.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Cryptographic primitive decision flowchart | Which primitive for which use case | 15.1 |
| ECB mode pattern diagram (described) | Why ECB leaks plaintext patterns | 15.3 |
| Password hashing comparison table | SHA-256 vs. bcrypt vs. argon2 | 15.4 |

---

## Phase 6: Detect, Investigate, Respond

---

### Chapter 16 — Spot the Suspicious Pattern: Build a Security Event Detector

#### 8.1 Chapter Identity

- **Phase:** 6 — Detect, Investigate, Respond
- **Primary capability:** The learner can parse structured logs, normalize events, apply detection rules, correlate related events, and generate explainable alerts.
- **Primary tool:** **eventdetect** — a security event detector that reads structured log streams, evaluates detection rules, and produces labelled alerts with evidence.
- **Intended level:** Advanced.
- **Real-world relevance:** Detection is the Blue Team's primary defense. Without detection, defenders are blind. Building a detection engine from first principles — even a simple one — teaches how commercial SIEMs work and why alert quality matters.

#### 8.2 Learning Outcomes

By completing Chapter 16, the learner can:

1. Parse JSON-structured log events into a normalized schema.
2. Implement threshold-based, pattern-based, and sequence-based detection rules.
3. Correlate events by common identifiers (IP address, user, session).
4. Test detection rules with synthetic attack sequences.
5. Tune thresholds to reduce false positives without eliminating true positives.
6. Produce alerts with explicit evidence and a human-readable explanation.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 03 (port scanning — produces events that can trigger rules), Chapter 09 (authorization testing — produces events), Chapter 12 (system diagnostics — produces events).
- **Downstream consumers:** Chapter 17 (Incident Investigation Tool) processes alerts from `eventdetect`.

#### 8.4 Subchapter Milestone Plan

**16.1 — Read the Logs: Parse Structured Events**

- *Capability gained:* Read a stream of JSON log events and parse them into a normalized event struct.
- *New theory:* Structured logging format. Event normalization: timestamp, source, event type, actor, target, outcome. Why timestamps and event ordering matter.
- *Tool evolution:* `eventdetect --input events.ndjson` reads events, prints normalized summaries.
- *Challenge:* Define a normalized `Event` struct. Parse events from JSON; handle missing fields gracefully (use zero values, do not panic).
- *Constraints:* Handle events out of chronological order (sort by timestamp after reading). Handle events with unknown types (pass through with a warning).
- *Acceptance criteria:* A provided test event stream produces the correct normalized output.
- *Enables:* 16.2.

**16.2 — Simple Rules: Threshold and Pattern Detection**

- *Capability gained:* Implement threshold-based rules (5 failed logins in 60 seconds) and pattern-based rules (event type matches a string pattern).
- *New theory:* Rule types: threshold (count over time window), pattern (regex on event fields), sequence (A followed by B within N seconds). True positive vs. false positive vs. false negative.
- *Visualizations:* Diagram: event stream → rule engine → alert queue. Table: rule type → example → common failure modes.
- *Tool evolution:* Load rules from a YAML or JSON config file. Evaluate each event against all rules. Emit an alert when a rule triggers.
- *Challenge:* Implement threshold and pattern rule types. Each rule has: name, type, parameters, severity, description.
- *Acceptance criteria:* A test event stream with 6 failed logins from the same IP within 60 seconds triggers a threshold rule.
- *Enables:* 16.3.

**16.3 — Connect the Dots: Correlate Events**

- *Capability gained:* Correlate events sharing a common identifier (IP, user, session) to evaluate rules that span multiple events.
- *New theory:* Event correlation: grouping by key (IP address). Sliding window. Stateful detection. Why stateless rules miss multi-event patterns.
- *Tool evolution:* Implement a sliding window event store keyed by IP address and user ID. Evaluate rules against the window for each new event.
- *Challenge:* Implement the correlation engine. Windows must expire (events older than `window_size` are removed). Each rule specifies which field to correlate on.
- *Constraints:* Window size configurable per rule. Memory limit: maximum 10,000 events in memory.
- *Acceptance criteria:* A port scan (many connections from one IP in short time) triggers the port scan detection rule.
- *Enables:* 16.4.

**16.4 — Event Sequences: Detect Ordered Patterns**

- *Capability gained:* Implement sequence detection rules that trigger when event A is followed by event B within a time window.
- *New theory:* Sequence rules: common patterns (failed login → successful login from same IP, scan → connection → auth attempt). Why order matters.
- *Tool evolution:* Add sequence rule type. Each sequence rule has an ordered list of event patterns and a time window.
- *Challenge:* Implement sequence matching with ordering and time constraints. A partial sequence (A seen, B not yet seen) must not trigger prematurely.
- *Acceptance criteria:* A sequence of scan event → authentication attempt from the same IP within 5 minutes triggers the rule.
- *Enables:* 16.5.

**16.5 — Test the Detector: Synthetic Attack Sequences**

- *Capability gained:* Test the detection rules using synthetic event streams that simulate known attack patterns.
- *New theory:* How to test detection rules: positive tests (attack should trigger alert), negative tests (normal activity should not trigger), edge cases (boundary values for thresholds).
- *Tool evolution:* Add a test mode: `eventdetect --test-mode --attack-simulation port-scan` generates a synthetic attack event stream and verifies detection.
- *Challenge:* Write at least 3 synthetic attack simulations: port scan, brute-force login, successful auth after failed logins (credential stuffing pattern). Each must trigger the appropriate rules.
- *Acceptance criteria:* All 3 attack simulations trigger their respective rules. A normal activity stream triggers no rules.
- *Enables:* 16.6.

**16.6 — Tune It: Reduce False Positives**

- *Capability gained:* Adjust detection thresholds and add exclusion rules to reduce false positives while maintaining true positive detection.
- *New theory:* Base rate fallacy. Why a 1% false positive rate on low-rate events still produces mostly false alerts. Precision and recall trade-off in detection.
- *Tool evolution:* Add allowlist/exclusion entries to rules (e.g., exclude monitoring IPs from threshold rules). Adjust thresholds. Run against a mixed event stream (attack + normal).
- *Challenge:* A mixed stream (50% attack events, 50% normal traffic from a monitoring IP) should produce alerts only for the attack events. Tune rules to achieve this.
- *Acceptance criteria:* Monitoring IP events do not trigger false alerts. Attack events still trigger alerts.
- *Enables:* 16.7.

**16.7 — Explain the Alert: Produce Evidence-Rich Output**

- *Capability gained:* Produce alerts that include the triggering events, the rule that fired, and a human-readable explanation.
- *New theory:* Alert quality: explainability, actionability. Why an alert without evidence wastes a responder's time. Alert fatigue and its cost.
- *Tool evolution:* Alert output: rule name, severity, timestamp, triggering events (with evidence), human-readable description ("5 failed logins from 192.168.1.100 in the past 60 seconds — brute force attempt suspected.").
- *Challenge:* Each alert includes: rule_name, severity, first_seen, last_seen, evidence (array of triggering events), explanation (string).
- *Acceptance criteria:* Alert JSON is valid. Evidence array contains the actual events that triggered the rule.

#### 8.5 Tool Lifecycle

- **Tool name:** `eventdetect`
- **Initial capability:** Parse structured events.
- **Final scope:** Threshold, pattern, and sequence rules; event correlation; synthetic test mode; evidence-rich alerts.
- **Output contract:** NDJSON alerts with rule_name, severity, evidence, explanation.
- **Security invariants:** Read-only access to log files. No automatic response actions.
- **Testing expectations:** Synthetic attack simulations as automated tests.
- **Downstream consumers:** Chapter 17 (Incident Investigation Tool) processes `eventdetect` alerts.
- **Maturity target:** L3.

#### 8.6 Testing and Acceptance

- Each rule type: threshold, pattern, sequence.
- Positive and negative test cases for each rule.
- Mixed stream tuning test.
- Alert format validation.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Generates events by running scanning and authentication tests that the detector is expected to catch. Evaluates whether the detector can see his activity.
- **Blue Team (Samia):** Builds and tunes the detection rules. Uses Rayhan's test activity as ground truth. Iterates until all attack patterns are detected without excessive false positives.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Event normalization schema table | What fields are in a normalized event | 16.1 |
| Detection pipeline diagram | Events → rules → alerts | 16.2 |
| Sliding window diagram | How event correlation works | 16.3 |
| Precision-recall trade-off table | True/false positive/negative definitions | 16.6 |

---

### Chapter 17 — Reconstruct the Incident: Build an Incident Investigation Tool

#### 8.1 Chapter Identity

- **Phase:** 6 — Detect, Investigate, Respond
- **Primary capability:** The learner can correlate events across multiple log sources, reconstruct an incident timeline, triage findings by priority, and produce a structured incident report.
- **Primary tool:** **incidenttool** — an incident investigation tool that reads multiple event sources, builds a unified timeline, identifies key events, and generates a structured report.
- **Intended level:** Advanced.
- **Real-world relevance:** Incident investigation is the most demanding Blue Team activity. It requires structured thinking, evidence discipline, and the ability to reason under uncertainty. Building a tool that structures this process makes investigators more consistent and less likely to miss critical evidence.

#### 8.2 Learning Outcomes

By completing Chapter 17, the learner can:

1. Merge and deduplicate events from multiple log sources with time alignment.
2. Build a unified incident timeline from multi-source events.
3. Triage events by relevance to the suspected incident.
4. Identify gaps in evidence and note what cannot be concluded.
5. Describe containment actions and the evidence that motivates them.
6. Verify that a threat has been contained.
7. Produce a structured incident report with findings and uncertainty statements.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** Chapter 16 (Security Event Detector — produces the alerts that this tool investigates).
- **Downstream consumers:** Chapter 18 (Final Engagement) uses incident investigation as the Blue Team response phase.

#### 8.4 Subchapter Milestone Plan

**17.1 — All the Sources: Merge and Align Events**

- *Capability gained:* Read events from multiple NDJSON log files, merge and sort by timestamp.
- *New theory:* Multi-source log analysis. Clock skew between sources. Deduplication (same event in two log sources). The danger of treating correlation as causation.
- *Tool evolution:* `incidenttool --sources http.log,auth.log,firewall.log` reads all sources, merges and sorts events by timestamp, deduplicates by event ID where available.
- *Challenge:* Handle sources with different schemas by normalizing to the common event format. Flag events whose timestamps are more than 60 seconds ahead of the wall clock (possible clock skew).
- *Acceptance criteria:* A test with 3 sources, some events shared, produces a correctly merged and deduplicated timeline.
- *Enables:* 17.2.

**17.2 — The Timeline: Build a Unified View**

- *Capability gained:* Display the merged event stream as a readable chronological timeline.
- *New theory:* Incident timeline as an investigative artifact. How to represent uncertain times (approximately). What to highlight in a timeline.
- *Tool evolution:* Add `--timeline` output mode. Display events in chronological order with source label, timestamp, type, actor, and outcome. Highlight events that match known alert rules.
- *Challenge:* In the timeline, visually distinguish alert-triggered events from background events. Group events less than 5 seconds apart as a cluster.
- *Acceptance criteria:* A timeline from a synthetic incident scenario clearly shows attack events before, during, and after the alert.
- *Enables:* 17.3.

**17.3 — What Matters Most?: Triage**

- *Capability gained:* Score events by relevance to the suspected incident using triage criteria, and surface the most relevant events.
- *New theory:* Triage: prioritizing investigation effort. Scoring heuristics: events involving the suspected actor or target, events near alert time, events with high severity.
- *Tool evolution:* Add `--triage --incident-start <timestamp> --incident-actor <ip>` to score events by proximity to the incident. Produce a sorted "key events" list.
- *Challenge:* Implement a relevance score that factors in: time proximity (events within 30 minutes of the alert), actor match (same IP), and event type (auth failures > page loads).
- *Acceptance criteria:* The key events list for a synthetic incident ranks attack events higher than background events.
- *Enables:* 17.4.

**17.4 — What Don't We Know?: Document Evidence Gaps**

- *Capability gained:* Identify what evidence is missing and what cannot be concluded from the available data.
- *New theory:* Evidence gaps: missing log sources, time gaps in captures, incomplete events. The difference between "we have no evidence of X" and "X did not happen." Why stating uncertainty is essential to responsible incident reporting.
- *Tool evolution:* Add `--gaps` analysis: detect time periods with no events (possible log gap), sources that failed to produce any events, and common event types that are absent.
- *Challenge:* If there is a 30-minute gap in a log source, report it explicitly. If no authentication events appear for an otherwise active IP, note that auth logs may be incomplete.
- *Acceptance criteria:* A test with a deliberate 30-minute log gap produces a gap warning at the correct timestamp.
- *Enables:* 17.5.

**17.5 — Contain and Recover: Support Decisions**

- *Capability gained:* Present the evidence that supports specific containment decisions, without making the decisions automatically.
- *New theory:* Containment decisions: network isolation, account suspension, system shutdown. Why automation of containment is dangerous. The role of a tool in presenting evidence, not acting.
- *Tool evolution:* Add `--containment-recommendations` mode. For each detected attack actor (IP, account), list: evidence for malicious activity, risk of false positive, recommended containment action, and impact of that action.
- *Challenge:* The tool presents options and evidence. It does not execute containment. The output must include uncertainty statements.
- *Acceptance criteria:* For a synthetic incident, the recommendations include the correct actor, evidence, and at least one uncertainty statement.
- *Enables:* 17.6.

**17.6 — Was It Effective?: Verify Containment**

- *Capability gained:* After containment actions are taken, verify that the actor's activity has ceased.
- *New theory:* Containment verification: compare pre- and post-containment event streams. What constitutes "no further activity." Why absence of evidence is not proof of containment.
- *Tool evolution:* Add `--verify-containment --after <timestamp>` to check whether the suspected actor appears in events after the containment timestamp.
- *Challenge:* Report: actor seen after containment (containment ineffective or new actor), actor not seen (possible but not certain — note log coverage), new actors seen with similar patterns.
- *Acceptance criteria:* Post-containment events with the actor's IP correctly flagged as possible containment failure.
- *Enables:* 17.7.

**17.7 — The Report: Structured and Honest**

- *Capability gained:* Generate a structured incident report that includes timeline, findings, evidence gaps, containment actions, verification, and uncertainty statements.
- *Tool evolution:* `incidenttool report --output report.md` generates a Markdown report with sections: executive summary, timeline, key findings, evidence quality, containment actions, verification, next steps.
- *Challenge:* Every finding section must include both the evidence and a statement of what cannot be concluded. The report must not overstate certainty.
- *Acceptance criteria:* The report includes at least one uncertainty statement per major finding.

#### 8.5 Tool Lifecycle

- **Tool name:** `incidenttool`
- **Initial capability:** Merge multi-source events.
- **Final scope:** Multi-source merge, timeline, triage, gap analysis, containment recommendations, verification, structured report.
- **Maturity target:** L2.

#### 8.6 Testing and Acceptance

- Merge and deduplication: 3 overlapping sources.
- Timeline: synthetic incident scenario.
- Triage: attack events ranked higher than background.
- Gap detection: deliberate log gap.

#### 8.7 Red/Blue Learning

- **Red Team (Rayhan):** Provides the synthetic attack event stream. Reviews the incident report to verify that the Blue Team correctly characterized his activity.
- **Blue Team (Samia):** Uses `incidenttool` to investigate Rayhan's simulated attack. Produces the incident report with containment recommendations.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Multi-source merge diagram | How events from different sources align | 17.1 |
| Incident timeline example | What a timeline looks like | 17.2 |
| Evidence quality assessment table | Strong/weak/absent evidence states | 17.4 |

---

## Phase 7: Bring Everything Together

---

### Chapter 18 — Run the Final Engagement: Build a Red/Blue Security Assessment Toolkit

#### 8.1 Chapter Identity

- **Phase:** 7 — Bring Everything Together
- **Primary capability:** The learner conducts a complete, authorized red/blue security assessment of a lab target using all accumulated tools, produces a structured assessment report, and demonstrates that detections and mitigations work end-to-end.
- **Primary deliverable:** A completed assessment report and a composed toolkit entrypoint (`assess`) that orchestrates the existing tools for a structured engagement.
- **Intended level:** Advanced (all prior chapters).
- **Real-world relevance:** Real-world security assessments integrate reconnaissance, vulnerability identification, exploitation, detection, mitigation, and reporting into a disciplined, documented process. This chapter puts the learner through a complete cycle in a controlled environment.

> **New implementation:** The `assess` orchestration tool is modest — it calls existing tools, collects their structured output, and produces an integrated report. The value is in the integration, not in building large new capabilities.

#### 8.2 Learning Outcomes

By completing Chapter 18, the learner can:

1. Define an engagement scope with explicit authorization boundaries.
2. Execute a structured reconnaissance phase using the full discovery toolkit.
3. Form security hypotheses and test them using the appropriate tools.
4. Reproduce a confirmed finding in the lab environment.
5. Verify that the Blue Team's detection rules fire for Red Team activities.
6. Apply and verify mitigations for confirmed findings.
7. Produce a complete, evidence-based security assessment report.

#### 8.3 Prerequisites and Dependencies

- **Required prior chapters:** All chapters 00–17.
- **Required tools available:** portscan, dnsinspect, svcfinger, httpinspect, httpproxy, webscan, authtest, pktinspect, tlscheck, sysdiag, fuzzlab, repro, cryptoaudit, eventdetect, incidenttool.
- **Lab requirement:** A purpose-built lab application that combines multiple vulnerabilities from previous chapters. Specified in the chapter's lab setup.

#### 8.4 Subchapter Milestone Plan

**18.1 — Define the Engagement: Scope and Authorization**

- *Capability gained:* Define a formal engagement scope with targets, time window, and out-of-scope items.
- *New theory:* Rules of engagement. Scope creep and its risks. Authorization documentation. What to do when unexpected scope is discovered.
- *Tool evolution:* `assess init --target 127.0.0.1 --scope scope.yaml` creates an engagement record.
- *Challenge:* Complete a scope template specifying: allowed targets, prohibited actions, time window, escalation path, and what constitutes a stop condition.
- *Acceptance criteria:* Scope YAML is complete and reviewed.
- *Enables:* 18.2.

**18.2 — Red Team Phase 1: Reconnaissance**

- *Capability gained:* Execute discovery using the full reconnaissance toolkit and document findings.
- *Tool evolution:* `assess recon` runs portscan, dnsinspect, and svcfinger against the defined scope; aggregates results into a unified reconnaissance report.
- *Challenge:* Run the full discovery sequence. Document: open ports, services identified, DNS records found. Form at least 3 security hypotheses for investigation.
- *Acceptance criteria:* Reconnaissance report identifies all services running on the lab target.
- *Enables:* 18.3.

**18.3 — Red Team Phase 2: Investigate and Exploit**

- *Capability gained:* Test the security hypotheses from reconnaissance using web inspection, TLS checking, and authorization testing tools.
- *Tool evolution:* `assess investigate --hypothesis <file>` runs appropriate tools for each hypothesis and records findings.
- *Challenge:* For each hypothesis: select the appropriate tool(s); execute controlled tests against the lab target; classify findings as confirmed, probable, or suspected. Produce at least one confirmed finding with reproduction steps.
- *Acceptance criteria:* At least one finding is confirmed with a reproduction case.
- *Enables:* 18.4.

**18.4 — Blue Team Phase 1: Detect the Red Team**

- *Capability gained:* Verify that detection rules in `eventdetect` fire for the Red Team's activities.
- *Tool evolution:* `assess detect --events engagement.log` runs `eventdetect` on the events generated during the Red Team phase.
- *Challenge:* Verify that at least 2 detection rules fire for the Red Team's activities. Document: which rules fired, which did not, and whether any Red Team activities went undetected.
- *Acceptance criteria:* Detection report produced. Gaps in detection identified and documented.
- *Enables:* 18.5.

**18.5 — Blue Team Phase 2: Investigate and Contain**

- *Capability gained:* Use `incidenttool` to investigate the detected activity and produce a containment recommendation.
- *Tool evolution:* `assess investigate-incident --events engagement.log --alerts alerts.ndjson` runs `incidenttool`.
- *Challenge:* Produce an incident timeline. Document the actor's activity. Recommend containment action with evidence. Verify containment (in the lab: take the lab server offline, verify no further events).
- *Enables:* 18.6.

**18.6 — Mitigate and Verify: Close the Loop**

- *Capability gained:* Apply mitigations for all confirmed findings and verify that the reproduction cases no longer succeed.
- *Tool evolution:* `assess verify-mitigations --findings findings.json` reruns each finding's reproduction test against the patched lab target.
- *Challenge:* For each confirmed finding: apply the provided mitigation in the lab, rerun the reproduction test, verify the finding is resolved, rerun `eventdetect` to verify the detection still fires for the old attack (regression test for detection).
- *Acceptance criteria:* All confirmed findings verified as resolved. All previous detections still firing for legacy attack patterns.
- *Enables:* 18.7.

**18.7 — The Assessment Report: The Deliverable**

- *Capability gained:* Produce a complete security assessment report from all engagement phases.
- *Tool evolution:* `assess report --output assessment.md` generates the final report from all collected phase outputs.
- *Challenge:* The report must include: executive summary, scope and authorization, reconnaissance findings, vulnerability findings with evidence and classification, detection effectiveness, incident investigation summary, mitigation verification, and recommendations. Every claim must be supported by evidence.
- *Acceptance criteria:* The report is complete, evidence-based, and clearly distinguishes confirmed findings from suspected ones.

#### 8.5 Tool Lifecycle

- **Tool name:** `assess`
- **Scope:** Orchestration tool — calls existing tools, aggregates output, produces integrated reports.
- **New capability:** Engagement lifecycle management, phase orchestration, integrated reporting.
- **Important principle:** `assess` is a thin integration layer. It does not reimplement capabilities that existing tools already provide.
- **Maturity target:** L3.

#### 8.6 Testing and Acceptance

- Each phase produces expected output against the lab target.
- Detection rules fire for Red Team activities.
- Mitigations verified: all confirmed findings resolved.
- Assessment report complete with evidence for all claims.

#### 8.7 Red/Blue Learning

- This chapter is explicitly both Red and Blue. Rayhan conducts phases 18.2 and 18.3. Samia conducts phases 18.4, 18.5, and 18.6. Both collaborate on 18.7.
- The chapter demonstrates the complete offensive-to-defensive cycle in a single integrated engagement.

#### 8.8 Visual Learning Plan

| Visual | Concept | Placement |
|---|---|---|
| Engagement lifecycle diagram | All phases and their outputs | 18.1 |
| Tool dependency map | Which tools feed which phases | 18.2 |
| Finding classification progression | Suspected → probable → confirmed → resolved | 18.3 |

---

## Curriculum-Level Decisions

### Decision 1: Chapter 08 Split from Original Chapter 08

The original proposal contained a single "Catch the Broken Trust Boundary: Build a Web Security Auditor" chapter covering both header/cookie auditing and authorization/behavior testing. These were separated into:

- **Chapter 08 — Audit the Web Surface:** Security headers, cookie attributes, HTTPS enforcement. Tool: `webscan`.
- **Chapter 09 — Test the Trust Boundary:** Auth vs. authz, role testing, JWT inspection, path traversal, evidence classification. Tool: `authtest`.

**Rationale:** The combined scope was too large for a single cohesive milestone plan. The tools have fundamentally different designs (header inspection vs. authenticated request testing). Splitting allows each chapter to have a focused, achievable progression.

**Effect:** Chapters 09–17 (original) become Chapters 10–18. Total chapters: 19 (00–18).

### Decision 2: Packet Inspector Uses PCAP File Reading

Chapter 10 (Packet Inspector) uses pcap file reading rather than live capture.

**Rationale:** Live packet capture requires elevated OS privileges (`CAP_NET_RAW` or root on Linux, `/dev/bpf` access on macOS, administrator on Windows). Requiring elevated privileges for a development exercise creates unnecessary friction and teaches a poor default habit. PCAP file reading teaches the same parsing skills. The chapter explains how live capture differs and what it requires.

### Decision 3: External Dependencies Policy

Three external dependencies are introduced and justified in the curriculum:

| Chapter | Dependency | Justification |
|---|---|---|
| 04 | `github.com/miekg/dns` | Go's `net` package does not expose TTL values. TTL is essential for the DNS security analysis in this chapter. |
| 10 | `github.com/google/gopacket/pcapgo` | PCAP file format parsing and packet decoding is too large a scope for an educational exercise. The learning objective is packet analysis, not PCAP format parsing. |
| 15 | None (uses `go/ast`) | Go source code AST parsing is in the standard library. |

All other tools use only the Go standard library.

### Decision 4: Tool Naming Convention

All tools use short, memorable command names: `byteinspect`, `netdiag`, `portscan`, `dnsinspect`, `svcfinger`, `httpinspect`, `httpproxy`, `webscan`, `authtest`, `pktinspect`, `tlscheck`, `sysdiag`, `fuzzlab`, `repro`, `cryptoaudit`, `eventdetect`, `incidenttool`, `assess`.

Chapter authors must not rename tools without updating all downstream references in this document.

### Decision 5: `go.mod` Deferred

No `go.mod` is created during the foundation pass. It will be established when the first Go implementation begins (Chapter 01 milestone 01.1). The module path will be `github.com/red-blue-lab` or equivalent — to be decided when the module is initialized.

---

## Dependency Map

```
Ch 00 ──────────────────────────────────────────┐
         (Go environment, TCP client/server)     │
                                                 ▼
Ch 01 ── Byte Inspector ──────────────────► Ch 10, Ch 13
         (byte representation, I/O)
                                                 │
Ch 02 ── Network Diagnostic ──────────────────── ┤
         (IP, TCP connectivity, outcome          │
          classification)                        ▼
                                            Ch 03, Ch 04
Ch 03 ── Port Scanner ───────────────────► Ch 05, Ch 18
         (TCP, concurrency, state)

Ch 04 ── DNS Inspector ──────────────────► Ch 06, Ch 08
         (DNS, record types, TTL)

Ch 05 ── Service Fingerprinter ──────────► Ch 06, Ch 18
         (banner grab, protocol probe)

Ch 06 ── HTTP Inspector ─────────────────► Ch 07, Ch 08
         (HTTP client, headers, HTTPS)           │
                                                 │
Ch 07 ── HTTP Proxy ──────────────────────────── ┤
         (proxy, logging, redaction)             │
                                                 ▼
                                            Ch 09

Ch 08 ── Web Security Header Scanner ────► Ch 18
         (headers, cookies, HTTPS audit)

Ch 09 ── Web Authorization Tester ───────► Ch 14, Ch 18
         (auth/authz, JWT, path traversal)

Ch 10 ── Packet Inspector ───────────────► Ch 11, Ch 16
         (packet parsing, TCP flows)

Ch 11 ── TLS Certificate Checker ────────► Ch 18
         (TLS chain, hostname, expiry)

Ch 12 ── System Diagnostics Tool ────────► Ch 16
         (processes, files, env, limits)

Ch 13 ── Fuzz Testing Tool ──────────────► Ch 14
         (fuzzing, panic capture, regression)

Ch 14 ── Vulnerability Regression Harness ► Ch 18
         (repro, root cause, patch verify)

Ch 15 ── Crypto Audit Tool ──────────────► Ch 18
         (weak crypto, AST scanning)

Ch 16 ── Security Event Detector ────────► Ch 17, Ch 18
         (rules, correlation, alerts)

Ch 17 ── Incident Investigation Tool ────► Ch 18
         (timeline, triage, report)

Ch 18 ── Final Engagement (assess)
         (integrates all tools)
```
