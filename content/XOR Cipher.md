# What is XOR?
The **XOR (Exclusive OR)** operation compares two bits.
It returns:
- `0` if both bits are equal.
- `1` if the bits are different.
Truth table:

|A|B|A XOR B|
|:-:|:-:|:-:|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

---
# Why is XOR useful?
XOR has a unique property:
```text
(A XOR B) XOR B = A
```
The same operation both encrypts and decrypts data.

---
# Example
Plaintext byte:
```text
01000001
```
Key:
```text
01000010
```
Ciphertext:
```text
00000011
```
Decrypt:
```text
00000011
XOR
01000010
=
01000001
```
The original byte is recovered.

---
# Repeating-key XOR
A short key is repeated until it matches the plaintext length.
Example:
```text
Key:
ABCABCABCABC...
Plaintext:
HELLOWORLD...
Ciphertext:
Plaintext XOR Key
```
This is the scheme used in [[Natas Level 11]].

---
# Known Plaintext Attack
If an attacker knows both:
- the plaintext
- the ciphertext
they can recover the key:
```text
Key = Plaintext XOR Ciphertext
```
This is why repeating-key XOR is considered insecure.

---
# Example in Node.js
```js
const input = Buffer.from("ABC");
const output = Buffer.alloc(input.length);
const key = 0x42;
for (let i = 0; i < input.length; i++) {
    output[i] = input[i] ^ key;
}
```
The `^` operator performs a bitwise XOR on the numeric values of each byte.

---
# Notes
XOR is extremely common in:
- CTFs
- Malware analysis
- Reverse engineering
- Simple obfuscation schemes
Modern cryptography does **not** use repeating-key XOR for secure encryption.