# Chapter 01 — Decode the Bytes: Build a Byte Inspector

> **Phase:** 1 — Understand the Building Blocks  
> **Level:** L2 — Reliable tool  
> **Primary deliverable:** \`byteinspect\`, a command-line tool for examining raw file and stdin bytes  
> **Prerequisite:** [Chapter 00 — Your First Security Lab](../00-your-first-security-lab/README.md)

Rayhan has received a suspicious attachment from the local lab. Its filename ends in \`.txt\`, but opening it in a text editor produces strange symbols and a few empty squares. The editor is trying to interpret bytes as text. That interpretation may be useful, but it is not the data itself.

Samia wants a reliable way to inspect the evidence without changing it. Before either engineer can reason about a file format, a network packet, or an encoded payload, they need to answer a simpler question:

**What bytes are actually present?**

This chapter builds that answer, one capability at a time. You will create a small inspector, teach it to render bytes in familiar forms, navigate to a range, interpret text encodings without hiding invalid data, and finally accept input from either a file or a pipe.

---

## What you will build

By the end of this chapter, \`byteinspect\` will:

- Read a file or standard input without treating its contents as text by default.
- Display bytes as decimal, binary, hexadecimal, or a classic hexdump.
- Select a byte range using a zero-based offset and a length.
- Interpret bytes under ASCII or UTF-8 rules while preserving invalid bytes in the output.
- Handle empty input, malformed arguments, oversized input, and I/O errors predictably.

The tool is an inspector, not a decoder for arbitrary file formats. It does not execute, modify, repair, or upload the input.

## Learning outcomes

After completing all five milestones, you should be able to:

1. Convert a byte value between binary, decimal, and hexadecimal.
2. Explain how a Go \`[]byte\` represents an ordered sequence of byte values.
3. Distinguish raw bytes from a text interpretation of those bytes.
4. Explain why one byte sequence can produce different text under different encodings.
5. Read a file as bytes and inspect an exact range using zero-based indexing.
6. Recognize valid and invalid UTF-8 sequences without silently discarding malformed input.
7. Accept the same input from a file argument or stdin.
8. Write deterministic tests using embedded byte sequences and temporary files.

## Prerequisites

- Complete Chapter 00: Go toolchain, basic Go syntax, terminal use, and basic file I/O.
- Be comfortable running \`go run\`, \`go build\`, and \`go test\`.
- Know how to create and inspect a small file from the terminal.

No networking or prior security knowledge is required. This chapter uses only Go's standard library. The first implementation milestone is where the project initializes its Go module, as specified in the curriculum.

## The byte-level mental model

A computer stores information as bits. A bit has one of two values: 0 or 1. Eight bits form a byte. A byte can therefore represent 256 distinct values, from 0 through 255.

A byte is not inherently a letter, a number written by a human, or an instruction. It is a value. Meaning comes from the convention used to interpret it.

Consider the byte value 65:

| Representation | Value |
|---|---|
| Binary | \`01000001\` |
| Decimal | \`65\` |
| Hexadecimal | \`0x41\` |
| ASCII interpretation | \`A\` |

These are four views of the same eight bits. The ASCII interpretation is meaningful only because ASCII assigns the value 65 to the capital letter \`A\`.

### A file is an ordered sequence of bytes

For a tiny file containing the bytes \`41 42 00 7F\`, its contents can be pictured as:

\`\`\`text
Index:       0       1       2       3
         +-------+-------+-------+-------+
Byte:    | 0x41  | 0x42  | 0x00  | 0x7F  |
         +-------+-------+-------+-------+
Decimal:    65      66       0      127
Binary: 01000001 01000010 00000000 01111111
\`\`\`

The index is the byte's position, starting at zero. Index 2 is the third byte, not the second. This convention matters when inspecting file headers and protocol fields: an offset is a position measured from the beginning of the byte sequence.

In Go, a \`[]byte\` is a slice of byte values. It has a length, can be indexed, and can be iterated. It does not promise that the values form valid text.

### Binary, decimal, and hexadecimal

| Hex | Decimal | Binary | ASCII |
|---|---:|---|---|
| \`00\` | 0 | \`00000000\` | non-printable |
| \`01\` | 1 | \`00000001\` | non-printable |
| \`09\` | 9 | \`00001001\` | non-printable |
| \`0A\` | 10 | \`00001010\` | line feed |
| \`20\` | 32 | \`00100000\` | space |
| \`30\` | 48 | \`00110000\` | \`0\` |
| \`41\` | 65 | \`01000001\` | \`A\` |
| \`7E\` | 126 | \`01111110\` | \`~\` |
| \`7F\` | 127 | \`01111111\` | delete control |

Hexadecimal is convenient because one hex digit represents four bits. Two hex digits represent exactly one byte. A byte written as \`01000001\` is easier to scan as \`41\` when reading a long dump.

### Raw bytes are not the same thing as text

A text editor must choose an encoding to turn bytes into characters. If the bytes do not form valid sequences under that encoding, the editor may show replacement symbols, omit data, or make a guess.

That is a display decision. It does not change the original bytes.

For security work, preserve the distinction:

- **Raw value:** the byte that exists in the input.
- **Interpretation:** what a selected encoding says that byte or sequence means.
- **Display:** how the tool chooses to make the value visible to a person.

A trustworthy inspector keeps the raw value available even when an interpretation fails.

---

# 01.1 — Read and Display: Bytes Are Just Numbers

Rayhan first needs a factual inventory. Before looking for strings or file signatures, he wants the exact byte values and their positions. Samia asks for an output that can be checked by hand.

### What you will build

A first version of \`byteinspect\` that reads one file and prints each byte's zero-based index, decimal value, and eight-bit binary representation.

### Prerequisites

- Chapter 00.
- Basic use of \`os.ReadFile\`, \`fmt.Printf\`, and command-line arguments.

### Just-in-time theory

A byte has an unsigned value from 0 to 255. In Go, \`byte\` is an alias for \`uint8\`. A byte slice (\`[]byte\`) stores an ordered sequence of these values.

The format verbs used in this milestone are:

| Verb | Meaning | Example for value 10 |
|---|---|---|
| \`%d\` | Decimal integer | \`10\` |
| \`%08b\` | Binary, padded to 8 digits | \`00001010\` |

The width in \`%08b\` is important. Without it, the value 10 could be printed as \`1010\`, which is mathematically correct but visually less useful when every byte should occupy eight bit positions.

The index and value answer different questions. The index tells you *where* a byte is. The value tells you *what number* is stored there.

### Visual explanation

The table below maps the first sixteen byte values. It is a compact conversion reference, not a claim that these values are all printable characters.

| Hex | Decimal | Binary |
|---|---:|---|
| \`00\` | 0 | \`00000000\` |
| \`01\` | 1 | \`00000001\` |
| \`02\` | 2 | \`00000010\` |
| \`03\` | 3 | \`00000011\` |
| \`04\` | 4 | \`00000100\` |
| \`05\` | 5 | \`00000101\` |
| \`06\` | 6 | \`00000110\` |
| \`07\` | 7 | \`00000111\` |
| \`08\` | 8 | \`00001000\` |
| \`09\` | 9 | \`00001001\` |
| \`0A\` | 10 | \`00001010\` |
| \`0B\` | 11 | \`00001011\` |
| \`0C\` | 12 | \`00001100\` |
| \`0D\` | 13 | \`00001101\` |
| \`0E\` | 14 | \`00001110\` |
| \`0F\` | 15 | \`00001111\` |

### Challenge specification

🎯 **Problem statement**

Build the first increment of \`byteinspect\`. It accepts a path to one file and reports every byte with its index, decimal value, and eight-bit binary representation.

**Objective**

Produce a deterministic, human-readable inventory of the file's raw bytes.

**Inputs**

- Exactly one positional argument: a path to a regular file.
- The file may contain any byte values, including zero bytes and invalid text sequences.
- Maximum accepted file size: 1 MiB (1,048,576 bytes).

**Outputs**

For each byte, print one line to stdout in this logical form:

\`\`\`text
INDEX  DECIMAL  BINARY
0      65       01000001
1      66       01000010
2      0        00000000
3      127      01111111
\`\`\`

The exact spacing may be chosen by you, but columns must be unambiguous and stable. Empty input produces no data lines. Diagnostics go to stderr.

**Behavioral contract**

- Read the file as raw bytes. Do not convert the whole file to a string before inspecting it.
- Indexes start at zero and increase by one for each byte.
- Decimal values are in the inclusive range 0–255.
- Binary values contain exactly eight digits.
- Preserve byte order.
- Do not omit zero-valued or non-printable bytes.
- An empty file is valid and produces zero data lines.
- Do not print a fabricated row for an empty file.

**Constraints**

- Use only the Go standard library.
- Reject files larger than 1 MiB.
- Do not modify the input file.
- Do not execute or interpret file contents.

**Edge cases**

- Empty file.
- One-byte file containing \`0x00\`.
- One-byte file containing \`0xFF\`.
- File containing all values from \`0x00\` through \`0xFF\`.
- File containing invalid UTF-8. It must still be read as bytes.
- File exactly 1 MiB and file one byte larger than 1 MiB.

**Error behavior**

| Condition | Required behavior |
|---|---|
| Missing path argument | Print usage to stderr; exit non-zero |
| More than one path argument | Print usage to stderr; exit non-zero |
| File does not exist or cannot be read | Print a concise path-related error to stderr; exit non-zero |
| File exceeds 1 MiB | Print a size-limit error to stderr; exit non-zero |
| Successful read | Exit zero |

Do not print partial successful output when the file is rejected for exceeding the limit.

**Security considerations**

The file is untrusted input. Treat it as data only. Avoid logging file contents as text, and do not write to the source path. The size limit prevents an unexpectedly large file from consuming unbounded memory.

**Acceptance criteria**

- A known fixture containing \`41 42 00 7F\` produces four rows with indexes 0–3 and decimal values 65, 66, 0, and 127.
- Every binary field is exactly eight characters wide.
- Empty input produces no rows and exits successfully.
- A missing file and an oversized file produce stderr diagnostics and non-zero exit status.
- The input file remains byte-for-byte unchanged.

**Test expectations**

Write deterministic tests using temporary files created by the test itself. Include the known four-byte fixture, empty input, a one-byte boundary, the maximum permitted size, and one byte over the limit. Tests must not depend on files already present on the developer's machine.

**Definition of completion**

The tool can read an arbitrary file up to 1 MiB and report every byte exactly once, in order, with a correct zero-based index, decimal value, and eight-bit binary representation.

### Verification

Create the four-byte fixture from explicit byte values, not by typing characters into an editor that might apply an encoding. Independently calculate the expected values and compare them with the program's output. Run the tests more than once: deterministic tests should produce the same result every time.

### Debrief

The first important discovery is that a file extension does not determine its contents. A file named \`.txt\` can contain arbitrary bytes. The inspector now reports what is present rather than what a text editor guesses is present.

### What's next

In 01.2, the same bytes will be grouped into a hexdump so that patterns and offsets are easier to scan.

---

# 01.2 — Hexdump: The Classic View

Rayhan's first output is accurate but cumbersome. A file with thousands of bytes becomes thousands of lines. Samia wants a view that lets her spot repeated values, readable fragments, and suspicious gaps without losing the original offsets.

### What you will build

Extend \`byteinspect\` with a \`--hex\` mode that prints sixteen bytes per row, including an offset, hexadecimal values, and a printable-ASCII sidebar.

### Prerequisites

- Completed 01.1.
- Keep the previous decimal/binary behavior and its tests.

### Just-in-time theory

A hexadecimal digit represents four bits. One byte therefore needs exactly two hexadecimal digits, from \`00\` through \`ff\`. The \`%02x\` formatting verb gives a lower-case hexadecimal value padded to at least two digits.

A hexdump usually shows three aligned regions:

1. **Offset:** the position of the first byte in the row.
2. **Hex columns:** the byte values, two hex digits each.
3. **ASCII column:** a cautious text view of the same bytes.

For this chapter, a byte is shown literally in the ASCII column only when its value is in the printable ASCII range \`0x20\` through \`0x7E\`. All other values are represented by a period (\`.\`). This avoids control characters changing the terminal display.

### Visual explanation

A sample row for the bytes \`48 65 6c 6c 6f 00 57 6f 72 6c 64 0a\`:

\`\`\`text
00000000  48 65 6c 6c 6f 00 57 6f 72 6c 64 0a              |Hello.World.|
^^^^^^^^  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ^^^^^^^^^^^^^
offset    hex bytes (16 slots per row)                     ASCII view
\`\`\`

The final row may contain fewer than sixteen bytes. Missing slots are padding for alignment, not additional bytes. The ASCII column must represent only bytes that actually exist.

### Challenge specification

🎯 **Problem statement**

Add a hexdump output mode to the existing tool. Do not replace the earlier byte inventory capability.

**Objective**

Display input in stable rows of sixteen bytes with an eight-digit offset, two-digit hexadecimal values, and a printable-ASCII sidebar.

**Inputs**

- The file path accepted by 01.1.
- A \`--hex\` flag selecting hexdump output.
- File size remains limited to 1 MiB for this milestone.

**Outputs**

A row contains:

- An eight-character, zero-padded, lower-case hexadecimal offset.
- Up to sixteen two-digit hexadecimal byte values separated by one space.
- An ASCII sidebar between vertical delimiters.
- A period for every byte outside \`0x20\`–\`0x7E\`.

Illustrative output:

\`\`\`text
00000000  48 65 6c 6c 6f 00 57 6f 72 6c 64 0a              |Hello.World.|
00000010  41                                               |A|
\`\`\`

**Behavioral contract**

- Rows represent consecutive, non-overlapping chunks of at most sixteen bytes.
- The first row offset is zero. Each next row offset increases by sixteen.
- Hex values are lower-case and exactly two digits.
- The ASCII sidebar is derived from the same bytes as the hex columns.
- Printable ASCII bytes are shown as their corresponding characters.
- Bytes below \`0x20\` or above \`0x7E\` are shown as \`.\`.
- A short final row is padded visually in the hex area so the sidebar remains aligned. Padding must never appear as actual bytes in the sidebar.
- Empty input produces no rows.
- The original 01.1 output remains available and unchanged.

**Constraints**

- Exactly sixteen byte positions per row.
- Offset field is eight hexadecimal digits, zero-padded.
- Use no third-party hexdump package.
- The tool must not assume that a row always contains sixteen actual bytes.

**Edge cases**

- Empty input.
- Exactly one byte.
- Exactly fifteen bytes.
- Exactly sixteen bytes.
- Exactly seventeen bytes (one full row and one one-byte row).
- Non-printable values such as \`00\`, \`09\`, \`0A\`, and \`7F\`.
- Printable boundary values \`20\` and \`7E\`.

**Error behavior**

Argument and file errors retain the behavior defined in 01.1. An unsupported or malformed flag must produce a clear stderr diagnostic and a non-zero exit status. No panic or silent fallback to a different format is acceptable.

**Security considerations**

The ASCII sidebar is a display aid, not a decoding step. Never emit raw control bytes into the terminal. The original input remains untouched.

**Acceptance criteria**

- A 16-byte fixture produces exactly one row at offset \`00000000\`.
- A 17-byte fixture produces a second row at offset \`00000010\`.
- Every hex byte has two digits.
- The ASCII sidebar shows printable ASCII and periods for all other values.
- Short-row padding affects alignment only; it does not create phantom bytes.
- The 01.1 mode still passes its complete test suite.

**Test expectations**

Use embedded byte fixtures or temporary files. Assert offsets, row count, hex values, sidebar characters, and final-row behavior. Include exactly 16 and 17 bytes because the row boundary is where off-by-one errors tend to hide.

**Definition of completion**

The hexdump mode renders any accepted input in correctly aligned sixteen-byte rows, and all 01.1 behavior remains intact.

### Verification

Compare a small fixture against \`xxd\` or \`hexdump -C\` when either utility is available. The external utility is an optional manual cross-check, not a test dependency. Your deterministic Go tests remain the source of truth.

### Debrief

The hexdump reveals patterns that a line-per-byte display hides. But the ASCII column is still only an interpretation. A period does not mean the byte is absent; it means the byte is not printable under this particular display rule.

### What's next

In 01.3, you will navigate directly to a region instead of dumping the entire file.

---

# 01.3 — Navigate: Inspect Ranges by Offset and Length

A large binary file may contain a header near the beginning and a payload much later. Rayhan needs to isolate a region without manually counting rows. Samia also wants to know exactly which bytes were examined so that the finding can be reproduced.

### What you will build

Add \`--offset N\` and \`--length N\` options that select a precise byte range before formatting.

### Prerequisites

- Completed 01.1 and 01.2.
- Understand zero-based indexing and the existing output modes.

### Just-in-time theory

A range is described by a starting offset and a number of bytes:

\`\`\`text
Input:   10 11 12 13 14 15 16 17 18 19
Index:    0  1  2  3  4  5  6  7  8  9

offset = 3, length = 4

Selected:          13 14 15 16
Index:               3  4  5  6
\`\`\`

The range includes the byte at \`offset\` and contains exactly \`length\` bytes. In interval notation, it covers \`[offset, offset+length)\`: the start is included and the end is excluded.

This is the same convention used by Go slice expressions. It also explains why a length of zero is meaningful: it selects no bytes.

Care is needed when validating \`offset + length\`. Integer addition can overflow. A robust contract checks that the offset is within the input and that the requested length does not exceed the remaining bytes, rather than trusting an unchecked sum.

### Visual explanation

\`\`\`text
Byte indexes:  0   1   2   3   4   5   6   7   8   9
               +---+---+---+---+---+---+---+---+---+---+
Input:         | A | B | C | D | E | F | G | H | I | J |
               +---+---+---+---+---+---+---+---+---+---+
                           ^               ^
                         offset=3       end=7 (exclusive)
                         <---- length=4 ---->
Selected:                  D   E   F   G
\`\`\`

The key detail is that the end position is exclusive. A range beginning at 3 with length 4 selects indexes 3, 4, 5, and 6.

### Challenge specification

🎯 **Problem statement**

Extend \`byteinspect\` so a user can select a range of bytes and render only that range in the chosen output mode.

**Objective**

Select an exact byte interval without off-by-one errors or out-of-bounds access.

**Inputs**

- Existing file path and output mode.
- \`--offset N\`: non-negative base-10 integer, default 0.
- \`--length N\`: non-negative base-10 integer, optional.
- If length is omitted, inspect from the offset through the end of the input.

**Outputs**

The selected bytes are passed to the chosen formatter. In hexdump mode, the displayed offset is the absolute offset in the original input, not a new zero-based offset relative to the selected range. In the decimal inventory mode, indexes are also absolute indexes in the original input.

**Behavioral contract**

- Offset is zero-based.
- Length counts bytes, not characters.
- If length is omitted, select all bytes from offset to end.
- If length is zero, select no bytes and produce no data rows.
- Offset equal to input length is valid only when the selected length is zero or omitted (the omitted range is empty).
- Offset greater than input length is invalid.
- If the requested length exceeds the number of bytes remaining after the offset, reject the request.
- A selected range is always contiguous.
- Existing formatting behavior applies to the selected bytes; only the displayed offsets/indexes remain absolute.

**Constraints**

- Offset and length must be non-negative integers.
- Reject malformed numbers, signs that imply negative values, and values that cannot be represented safely.
- Do not allow integer overflow during range validation.
- Keep the existing 1 MiB file limit.
- Do not silently clamp a range to the end of the file.

**Edge cases**

- Offset 0 and length 0.
- Offset at the last byte with length 1.
- Offset equal to file length with length 0.
- Offset equal to file length with length 1.
- Offset greater than file length.
- Length exactly equal to the remaining bytes.
- Length one byte larger than the remaining bytes.
- Very large decimal arguments that exceed the supported integer range.
- Empty file with default options and with explicit zero length.

**Error behavior**

| Condition | Required behavior |
|---|---|
| Negative or malformed offset/length | stderr diagnostic; non-zero exit |
| Offset greater than input length | stderr diagnostic; non-zero exit |
| Length exceeds remaining bytes | stderr diagnostic; non-zero exit |
| Valid zero-length range | No data rows; exit zero |
| Valid range | Format exactly the selected bytes |

Do not silently shorten an invalid request. The user must be able to distinguish “the requested range exists” from “the tool displayed less data than requested.”

**Security considerations**

Input arguments are untrusted. Validate numeric conversion and range boundaries before indexing or slicing. Avoid unchecked arithmetic that can wrap around and turn an invalid range into an apparently valid one. Do not leak data outside the requested range.

**Acceptance criteria**

- For a known file, \`--offset 4 --length 8\` displays exactly eight bytes beginning at index 4.
- A range at the end of the file behaves according to the boundary rules above.
- Invalid ranges fail clearly and do not panic.
- A valid zero-length range exits successfully with no data rows.
- The hexdump offset and decimal indexes refer to the original input positions.
- All 01.1 and 01.2 tests continue to pass.

**Test expectations**

Write table-driven tests for valid and invalid ranges. Include empty input, last-byte selection, exact remaining length, one-byte overflow, and extremely large numeric arguments. Tests should verify both selected values and absolute offsets.

**Definition of completion**

For every accepted offset/length pair, the tool displays exactly the requested bytes and their original positions; every invalid range is rejected without panic or silent truncation.

### Verification

Use a deterministic input with distinct byte values at each position so that a wrong offset is immediately visible. For example, a fixture containing values 0 through 15 makes it easy to verify that offset 4 and length 8 selects values 4 through 11.

### Debrief

An offset is not a character position and a length is not a visual width. Both count bytes. This distinction becomes essential when a later tool parses packet headers or binary structures whose fields are defined at exact byte offsets.

### What's next

In 01.4, the inspector will interpret the selected bytes as ASCII or UTF-8 while retaining evidence of malformed sequences.

---

# 01.4 — Interpret: Decode as Text Encodings

Rayhan finds a byte sequence that looks almost like a readable message. One part displays correctly, but another part appears malformed. If he replaces invalid bytes with a question mark and moves on, he may erase the very evidence he is investigating.

Samia wants two explicit interpretations: ASCII and UTF-8. Neither is allowed to hide bytes that do not fit.

### What you will build

Add \`--decode ascii\` and \`--decode utf8\` modes. The tool reports printable text, non-printable or non-ASCII values, and invalid UTF-8 bytes without repairing or discarding them.

### Prerequisites

- Completed 01.1 through 01.3.
- Understand that byte values and characters are not interchangeable.

### Just-in-time theory

**ASCII** is a seven-bit character encoding. Its standard character assignments occupy values 0 through 127. Values above \`0x7F\` are not ASCII characters. Some values within the range are control characters rather than printable symbols.

**UTF-8** encodes Unicode code points using sequences of one to four bytes. ASCII characters use the same single-byte values in UTF-8, which is why ordinary English text often looks identical in both. Non-ASCII characters require multi-byte sequences.

A UTF-8 sequence has structure:

| Leading byte range | Meaning |
|---|---|
| \`00\`–\`7F\` | One-byte ASCII-compatible code point |
| \`C2\`–\`DF\` | Start of a two-byte sequence |
| \`E0\`–\`EF\` | Start of a three-byte sequence |
| \`F0\`–\`F4\` | Start of a four-byte sequence |
| \`80\`–\`BF\` | Continuation byte; not a valid leading byte |
| Other values | Invalid as UTF-8 leading bytes |

This table is a guide to the byte roles, not the complete validation algorithm. Some leading-byte and continuation-byte combinations are invalid because they would encode overlong values, surrogate code points, or values beyond the Unicode range. Use Go's standard \`unicode/utf8\` facilities to validate UTF-8 rather than attempting to infer validity from the first byte alone.

A Unicode character can occupy several bytes. Therefore, a byte offset may point into the middle of a multi-byte character. A selected range is still a valid byte range even if it begins or ends inside a UTF-8 sequence.

### Visual explanation

The character \`€\` is encoded in UTF-8 as three bytes:

\`\`\`text
Character:       €
Unicode code:    U+20AC
UTF-8 bytes:     E2 82 AC

E2 = 11100010   three-byte sequence begins
82 = 10000010   continuation byte
AC = 10101100   continuation byte
\`\`\`

All three bytes are needed for the complete character. If the final byte is missing, the remaining prefix is not a complete UTF-8 encoding of that character.

For a deliberately malformed sequence such as \`41 82 42\`, the ASCII-compatible bytes around the invalid value must remain visible. The byte \`82\` is a continuation byte with no valid leading byte before it.

### Challenge specification

🎯 **Problem statement**

Add explicit ASCII and UTF-8 interpretation modes to \`byteinspect\`. Report invalid or non-ASCII bytes without changing the underlying data.

**Objective**

Make text interpretation useful for investigation while preserving every raw byte and identifying invalid sequences accurately.

**Inputs**

- Existing input file and range options.
- \`--decode ascii\` or \`--decode utf8\`.
- The selected byte range is interpreted; if no range is supplied, the full input is selected.

**Outputs**

For ASCII mode:

- Values 0–127 are recognized as within the ASCII encoding.
- Printable ASCII values \`0x20\`–\`0x7E\` may be shown as characters.
- Control values are identified as non-printable/control values.
- Values above \`0x7F\` are annotated as \`[non-ASCII]\`.

For UTF-8 mode:

- Valid UTF-8 sequences are displayed as their decoded text.
- Invalid byte sequences are annotated with \`[invalid]\` and their raw byte value remains available in the output.
- The tool must identify invalid bytes or invalid sequence spans accurately enough that no malformed byte is silently dropped.
- The output must preserve the order of valid and invalid portions.

Illustrative logical output for bytes \`41 82 42\`:

\`\`\`text
offset 0: A
offset 1: 0x82 [invalid]
offset 2: B
\`\`\`

This is an illustration of the information that must be retained; the exact line layout is yours to define.

**Behavioral contract**

- ASCII and UTF-8 are explicit modes. Do not guess an encoding automatically.
- ASCII bytes above \`0x7F\` are annotated as non-ASCII, not silently converted.
- ASCII control values are not emitted raw to the terminal.
- UTF-8 validation must follow UTF-8 validity rules, not merely check whether a byte is in a continuation range.
- Valid multi-byte sequences are decoded as a unit.
- Invalid sequences remain represented in the output with their original byte values.
- Do not repair, normalize, skip, or replace invalid bytes without an explicit annotation that preserves the original value.
- A range beginning or ending inside a multi-byte sequence is handled as the selected bytes actually stand: an incomplete fragment is invalid within that selected input.
- Existing decimal, binary, and hexdump modes remain available and unchanged.

**Constraints**

- Use only the Go standard library; no third-party encoding library.
- Do not write decoded content to a file.
- Do not execute or interpret the decoded text.
- Do not allow terminal control bytes to alter terminal state.

**Edge cases**

- Empty input.
- Pure ASCII text.
- ASCII control characters such as NUL, tab, carriage return, and line feed.
- A valid two-byte UTF-8 sequence.
- A valid three-byte sequence such as the euro sign.
- A valid four-byte sequence such as a supplementary-plane emoji.
- A lone continuation byte.
- An incomplete multi-byte sequence at end of input.
- An invalid leading byte.
- Overlong encodings.
- UTF-8 encodings of surrogate code points.
- Code points above U+10FFFF.
- A selected range that starts or ends in the middle of a valid sequence.

**Error behavior**

- Unknown decode mode: stderr diagnostic and non-zero exit.
- Invalid input range: retain the range error behavior from 01.3.
- Invalid UTF-8 data is not a command error. It is input evidence and must be annotated while the command exits successfully.
- File and I/O errors retain earlier behavior.

**Security considerations**

Malformed text is a common source of parser disagreement and security bugs. Never silently normalize invalid sequences or assume that a displayed replacement character represents the original bytes. Escape or annotate control values so untrusted input cannot manipulate the terminal. The tool must remain read-only.

**Acceptance criteria**

- A valid UTF-8 emoji is recognized as one valid multi-byte sequence.
- A lone continuation byte is identified as invalid.
- An incomplete sequence at end of input is identified as invalid.
- ASCII values above \`0x7F\` are marked non-ASCII.
- Control bytes are not emitted raw.
- Invalid bytes remain identifiable by their original hexadecimal values.
- The selected range is respected, including ranges that split a multi-byte sequence.
- All earlier milestone tests remain green.

**Test expectations**

Embed byte sequences directly in tests. Cover valid one-, two-, three-, and four-byte UTF-8 sequences, lone continuation bytes, incomplete sequences, overlong encodings, surrogate encodings, and out-of-range code points. Assert that invalid bytes remain represented and that no test depends on the machine's locale or terminal encoding.

**Definition of completion**

The tool can distinguish valid text from invalid byte sequences under explicitly selected ASCII and UTF-8 rules, without losing or modifying any raw input byte.

### Verification

Use a fixture containing ordinary ASCII, a valid multi-byte character, and deliberately malformed bytes. Compare the raw hex view with the decode view. Every byte in the selected range must be accounted for by either a valid decoded sequence or an invalid/non-ASCII annotation.

### Debrief

A string is an interpretation of bytes under an encoding. It is not a replacement for the bytes themselves. Preserving that distinction helps prevent parser differentials: two systems may interpret malformed input differently, and an investigator must be able to see what was actually supplied.

### What's next

In 01.5, the tool will accept both named files and piped stdin, then expose its output representations through one consistent interface.

---

# 01.5 — Compose: Accept Stdin and Multiple Formats

Samia receives a byte sequence from a command pipeline rather than a file. Requiring her to save it first would add friction and create another artifact to manage. Rayhan wants the same inspector to work on either source, with a single format-selection interface.

### What you will build

Unify input handling so \`byteinspect\` reads a named file or stdin, and add a \`--format\` option for \`hex\`, \`decimal\`, \`binary\`, \`utf8\`, and \`ascii\`.

### Prerequisites

- Completed 01.1 through 01.4.
- Understand command-line flags, \`os.Stdin\`, and the \`io.Reader\` abstraction.

### Just-in-time theory

A command-line program can receive data through two common paths:

- A **file argument** identifies a named file that the program opens and reads.
- **Standard input (stdin)** is a stream supplied by the shell, another process, or an interactive terminal.

A pipe connects one program's stdout to another program's stdin:

\`\`\`text
producer stdout ───────► byteinspect stdin
\`\`\`

From the reader's perspective, stdin is an input stream. It does not need to know whether the bytes came from a file, a pipe, or another source.

A stream may not have a known total size in advance. This affects resource handling: the program must enforce its input limit while reading rather than assuming that stdin is always small. For this milestone, the total accepted input is capped at 10 MiB.

The output format is independent of the input source. A file and a pipe containing identical bytes must produce identical output when given the same format and range options.

### Visual explanation

\`\`\`mermaid
flowchart LR
    F[Named file] --> R[Input reader]
    P[Pipe / stdin] --> R
    R --> L{Within 10 MiB limit?}
    L -->|yes| S[Selected byte range]
    L -->|no| E[Error on stderr]
    S --> M{Requested format}
    M --> H[Hex dump]
    M --> D[Decimal]
    M --> B[Binary]
    M --> U[UTF-8 interpretation]
    M --> A[ASCII interpretation]
\`\`\`

The input path converges before formatting. This is the central design property: output behavior should not depend on whether the bytes came from a file or stdin.

### Challenge specification

🎯 **Problem statement**

Complete \`byteinspect\` by supporting file or stdin input and a unified output-format flag.

**Objective**

Provide one command-line interface that accepts either a named file or piped input, enforces a bounded input size, applies range selection, and renders the selected bytes in the requested format.

**Inputs**

- Optional positional file path.
- If no path is provided, read from stdin.
- \`--format\` accepts exactly one of:
  - \`hex\`
  - \`decimal\`
  - \`binary\`
  - \`utf8\`
  - \`ascii\`
- \`--offset N\` and \`--length N\` retain the behavior from 01.3.
- Default format: \`hex\`.
- Maximum total input size: 10 MiB (10,485,760 bytes).

**Outputs**

- The selected format is written to stdout.
- Diagnostics and usage errors are written to stderr.
- The same byte sequence with the same options must produce identical output regardless of whether it comes from a file or stdin.
- For \`hex\`, use the hexdump layout established in 01.2.
- For \`decimal\`, print zero-based absolute index and decimal value as established in 01.1.
- For \`binary\`, print zero-based absolute index and exactly eight binary digits.
- For \`utf8\` and \`ascii\`, use the interpretation and annotation rules established in 01.4.

**Behavioral contract**

- Exactly one input source is used.
- With one positional path, read that file.
- With no positional path, read stdin.
- More than one positional path is an error.
- The default format is \`hex\`.
- Unsupported format values are errors; do not silently fall back.
- Apply range validation consistently to file and stdin input.
- The input limit is 10 MiB. If the input exceeds the limit, fail with a clear error and do not produce a successful partial dump.
- A stream that ends at or below the limit is valid, including an empty stream.
- A read error is reported to stderr and produces a non-zero exit status.
- The program must not wait for additional input after EOF.
- Output for identical bytes and options is byte-for-byte identical across file and stdin input.
- Existing range semantics and absolute offsets/indexes remain unchanged.

**Constraints**

- Use only the Go standard library.
- Enforce the 10 MiB cap while reading stdin; do not read an unbounded stream into memory.
- Do not require the entire stream to be buffered before deciding whether it exceeds the limit.
- Do not write input data to disk.
- Do not make network requests.
- Do not execute or interpret input bytes.
- Preserve all earlier format and range behavior.

**Edge cases**

- Empty stdin.
- Empty named file.
- Pipe containing one byte.
- Pipe containing exactly 10 MiB.
- Pipe containing 10 MiB plus one byte.
- File and stdin containing identical binary bytes.
- No positional path with an interactive stdin source that reaches EOF.
- More than one positional path.
- Unsupported format.
- Valid zero-length range.
- Range outside the input.
- Invalid UTF-8 supplied through stdin.

**Error behavior**

| Condition | Required behavior |
|---|---|
| No path; stdin reaches EOF normally | Process input normally, including empty input |
| One path; file cannot be opened/read | stderr diagnostic; non-zero exit |
| More than one path | Usage diagnostic; non-zero exit |
| Unsupported format | stderr diagnostic; non-zero exit |
| Input exceeds 10 MiB | stderr size-limit diagnostic; non-zero exit; no successful partial output |
| Stdin read failure | stderr diagnostic; non-zero exit |
| Invalid range | Same clear range error as 01.3 |
| Invalid UTF-8 bytes | Annotate as data; do not treat as an I/O failure |

The 10 MiB limit applies to the complete input, not merely the selected range.

**Security considerations**

Stdin is untrusted input just like a file. A pipe can produce an arbitrarily long stream, so enforce the size cap during reading. Do not write input to temporary files, execute it, or emit raw control characters. Avoid partial output that could be mistaken for a complete inspection when the input was rejected for exceeding the cap.

**Acceptance criteria**

- \`echo "hello" | byteinspect --format hex\` produces the expected hexdump.
- \`byteinspect --format binary myfile.bin\` produces binary output with absolute indexes.
- A file and stdin containing identical bytes produce byte-for-byte identical output for every format.
- Empty file and empty stdin are valid.
- Input exactly at 10 MiB is accepted; one byte above the limit is rejected.
- Unsupported formats and malformed arguments fail clearly.
- Range behavior is identical for both input sources.
- All tests from 01.1 through 01.4 remain green.

**Test expectations**

Test the input-selection and formatting logic with deterministic byte slices. Add integration coverage that invokes the built binary or its command entrypoint with both a temporary file and controlled stdin. Include exact-limit and over-limit tests. Avoid tests that rely on shell-specific behavior; where a shell pipe is used as a manual experiment, keep automated tests portable.

**Definition of completion**

A single \`byteinspect\` binary can inspect a bounded file or stdin stream in any supported format, with consistent range semantics and deterministic output.

### Verification

Run the same fixture through both input paths and compare stdout byte-for-byte. Then test the size boundary: exactly 10 MiB must be accepted, while 10 MiB plus one byte must fail without presenting a partial result as complete.

### Debrief

The final tool has a clean separation between where bytes come from, which range is selected, and how that range is displayed. That separation is more than tidy command-line design: it makes the inspector predictable and testable.

---

## Tool lifecycle

| Property | Contract |
|---|---|
| Tool name | \`byteinspect\` |
| Initial capability | 01.1: file input, decimal and binary inventory |
| Final input | One file path or stdin |
| Final formats | \`hex\`, \`decimal\`, \`binary\`, \`utf8\`, \`ascii\` |
| Range support | Zero-based offset and byte length |
| File limit | 1 MiB through 01.4 |
| Final input limit | 10 MiB, including stdin |
| External dependencies | None; Go standard library only |
| Side effects | No file writes, execution, or network access |
| Maturity target | L2 — Reliable tool |

### Important error states

- Missing or unreadable file.
- Multiple file arguments.
- Unsupported output format.
- Invalid numeric offset or length.
- Offset beyond input.
- Length beyond remaining input.
- Input exceeding the applicable size limit.
- Stdin read failure.
- Invalid UTF-8 data (an annotated data condition, not a command failure).

### Security invariants

- Input is always treated as untrusted data.
- The tool never executes or interprets input.
- The tool never modifies the source.
- No raw terminal control bytes are emitted.
- Input size is bounded.
- Invalid encodings remain visible as evidence.
- No external I/O is performed.

## Testing strategy

Every milestone adds deterministic tests and retains earlier tests as regression coverage.

| Area | Required cases | What the tests demonstrate |
|---|---|---|
| Byte inventory | Empty, one byte, all 256 values | Correct values, order, and indexing |
| Binary formatting | 0, 1, 127, 128, 255 | Exactly eight bits per byte |
| Hexdump | 1, 15, 16, 17 bytes | Correct row boundaries and offsets |
| ASCII sidebar | 0x1F, 0x20, 0x7E, 0x7F | Printable boundary behavior |
| Range selection | First, middle, last, zero length | Correct zero-based byte selection |
| Range rejection | Beyond end, too long, huge numbers | Safe validation without panic |
| ASCII interpretation | Control values and >0x7F | Non-printable and non-ASCII annotation |
| UTF-8 interpretation | Valid 1–4 byte sequences and malformed sequences | Correct validation and preservation |
| Input sources | Same fixture from file and stdin | Source-independent output |
| Size limits | Exactly limit and limit + 1 | Bounded resource use |

Use embedded byte slices and temporary files. No test should depend on a public website, external DNS, machine locale, terminal encoding, or pre-existing local files.

Run the complete test suite after every milestone. A later milestone is not complete merely because its new tests pass; earlier behavior must remain intact.

## Red/Blue learning

🔴 **Rayhan — Red Team perspective**

Byte-level inspection is a foundation for understanding binary protocols, file signatures, parser behavior, and malformed input. In this chapter, Rayhan uses the inspector to establish what bytes a file actually contains. The exercise is analysis, not execution: no payload is run and no external target is contacted.

🔵 **Samia — Blue Team perspective**

The same skill supports forensic review and defensive analysis. Samia can preserve suspicious artifacts, compare raw bytes with their text interpretation, and avoid mistaking a rendering artifact for evidence. Invalid encoding annotations are especially useful when investigating inconsistent parsing behavior between components.

**Shared lesson:** A reliable security conclusion begins with preserving the input and separating observation from interpretation. Chapter 10 returns to this discipline when parsing packet data. Chapter 13 uses byte sequences as fuzzing inputs. Chapter 14 relies on precise reproduction of malformed inputs.

## Publication checklist

Before considering this chapter complete, verify:

- [ ] All five milestones are present and follow the curriculum order.
- [ ] Each milestone adds one focused, working capability.
- [ ] No implementation code or solution is included in the regular challenge body.
- [ ] Each challenge specifies inputs, outputs, behavior, constraints, edge cases, errors, security, acceptance, tests, and completion.
- [ ] Diagrams are embedded in this Markdown file and explained nearby.
- [ ] Tests use deterministic local data only.
- [ ] Invalid UTF-8 is preserved and annotated, not silently repaired.
- [ ] Earlier milestone tests remain regression coverage.
- [ ] Tool name, flags, limits, and milestone scope match \`docs/CURRICULUM.md\`.
- [ ] No tests are claimed to have passed unless they were actually run.

## What's next

Chapter 02 — **See Your Network: Build a Network Diagnostic Tool** — moves from bytes on disk to the network configuration of the local machine. The byte-level intuition developed here will help when IP addresses and packet fields are represented as bytes.
