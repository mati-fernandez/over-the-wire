# What is Base64?
**Base64** is an encoding scheme that represents binary data using 64 printable ASCII characters.
It is **not encryption** and **not compression**. It simply converts bytes into text so they can be transmitted or stored safely in text-based systems.

---
# Why use Base64?
Many protocols and formats expect text rather than raw binary data.
Common examples include:
- HTTP cookies
- Email (MIME)
- JSON APIs
- Data URIs
- JWTs

---
# How it works
```text
Bytes
   │
   ▼
Base64 Encode
   │
   ▼
Printable ASCII text
```
Decoding performs the reverse operation.

---
# Example
Original text:
```text
Hello
```
Bytes (hex):
```text
48 65 6c 6c 6f
```
Base64:
```text
SGVsbG8=
```
Decoding `SGVsbG8=` returns the original bytes.

---
# Important
After decoding Base64, the result is **bytes**, not necessarily readable text.
Those bytes may represent:
- UTF-8 text
- An image
- A PDF
- Encrypted data
- Any binary format
The interpretation depends on the application.

---
# Common tools
## Bash
```bash
echo "SGVsbG8=" | base64 -d
```
## Node.js
```js
Buffer.from("SGVsbG8=", "base64");
```

---
# Notes
Base64 is reversible without a key.
Anyone can decode Base64 if they have the encoded data.
It provides **no confidentiality**.