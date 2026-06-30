# What is a Buffer (Node.js)?
A **Buffer** is a Node.js object used to store and manipulate **raw binary data** (bytes).
Unlike JavaScript strings, which represent text, a `Buffer` represents the actual bytes stored in memory.

---
# Why use Buffers?
Many operations work on bytes rather than text, including:
- Cryptography (XOR, AES, RSA)
- Base64 encoding/decoding
- File I/O
- Network protocols
- Binary formats (images, PDFs, executables)

---
# Creating Buffers
## From a string
```js
const buf = Buffer.from("Hello");
```
Creates a buffer containing the UTF-8 bytes of `"Hello"`.

---
## From a Base64 string
```js
const buf = Buffer.from("SGVsbG8=", "base64");
```
The second argument specifies the **encoding of the input string**.
Node automatically decodes the Base64 text into its original bytes.

---
## Allocate empty memory
```js
const buf = Buffer.alloc(16);
```
Creates a buffer of 16 bytes initialized to `0x00`.
This is commonly used to store the output of an algorithm.

---
# Accessing bytes
Buffers behave like arrays of unsigned 8-bit integers.
```js
const buf = Buffer.from("ABC");
console.log(buf[0]); // 65
console.log(buf[1]); // 66
console.log(buf[2]); // 67
```
Each element is a single byte (`0`–`255`).

---
# Converting Buffers
## To UTF-8 text
```js
buf.toString();
```
## To Base64
```js
buf.toString("base64");
```
## To hexadecimal
```js
buf.toString("hex");
```

---
# XOR example
```js
const input = Buffer.from("ABC");
const output = Buffer.alloc(input.length);
const key = 0x42;
for (let i = 0; i < input.length; i++) {
    output[i] = input[i] ^ key;
}
```
Each byte is processed independently.

---
# Buffer vs. String
|String|Buffer|
|---|---|
|Stores text.|Stores raw bytes.|
|Human-readable.|May contain arbitrary binary data.|
|Encoded (UTF-8 by default).|No inherent encoding.|
|Used for text processing.|Used for binary processing.|

---
# Notes
A `Buffer` does **not** know whether its bytes represent text, an image, encrypted data, or anything else. Interpretation depends on how the data is encoded or processed.
For example:
- `Buffer.from("SGVsbG8=", "base64")` contains the bytes of `"Hello"`.
- `Buffer.from(ciphertext, "base64")` contains encrypted bytes, which are not expected to be human-readable.

---
# Related
- [[Base64]]
- [[XOR Cipher]]