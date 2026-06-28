# What is a Hex Dump?
A **hex dump** is a human-readable representation of binary data. It displays the contents of a file or memory as hexadecimal values, often alongside their ASCII representation.
Example:
```text
00000000: 4865 6c6c 6f0a                           Hello.
```
It is commonly used in reverse engineering, digital forensics, binary analysis, exploit development, and debugging.

---
# Anatomy of a Hex Dump
```text
00000000: 4865 6c6c 6f0a                           Hello.
```
This output consists of three parts:
## 1. Offset
```text
00000000
```
The **offset** indicates the position (in bytes) from the beginning of the file.
Examples:
```text
00000000  → byte 0
00000010  → byte 16
00000020  → byte 32
```
Offsets are displayed in **hexadecimal**.
The leading zeros are **padding** to keep all lines aligned. Eight hexadecimal digits can represent any 32-bit offset (`0x00000000` to `0xFFFFFFFF`).

---
## 2. Hexadecimal Bytes
```text
4865 6c6c 6f0a
```
Each **byte** is represented by **two hexadecimal digits**.
Example:

| Hex |   ASCII   |
| --- | --------- |
|  48 |     H     |
|  65 |     e     |
|  6C |     l     |
|  6C |     l     |
|  6F |     o     |
|  0A | LF (`\n`) |
Tools such as `xxd` group bytes for readability. The grouping has no special meaning.

---
## 3. ASCII Representation
`Hello.`
Whenever possible, printable bytes are shown as their ASCII characters.
Non-printable bytes are displayed as a dot (`.`).
For example `0A` represents a newline character (`LF`), so it appears as `.`

---
# Plain Hex vs. Hex Dump
- A **plain hexadecimal string** contains only hexadecimal digits: `48656c6c6f0a`
- A **hex dump** includes additional information such as offsets and an ASCII column:
```text
00000000: 4865 6c6c 6f0a                           Hello.
```
---
# Working with `xxd`
Generate a hex dump:
```bash
echo "Hello" | xxd
```
Output:
```text
00000000: 4865 6c6c 6f0a                           Hello.
```
Generate plain hexadecimal:
```bash
echo "Hello" | xxd -p
```
Output:
```text
48656c6c6f0a
```
Convert plain hexadecimal back to its original bytes:
```bash
echo "48656c6c6f0a" | xxd -r -p
```
## Common Flags
- `-r` (**reverse**): Converts hexadecimal data back into its original binary representation.
- `-p` (**plain**): Expects plain hexadecimal input instead of a formatted hex dump.
Together:
```bash
xxd -r -p
```
means:
> Reverse a plain hexadecimal string into its original binary data.
---
# Common Use Cases
- Inspect binary files.
- Identify file signatures (magic bytes).
- Analyze network captures.
- Reverse engineer executables.
- Understand exploit payloads.
- Convert between binary and hexadecimal representations.