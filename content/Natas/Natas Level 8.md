#### Concept
**Reversible Encoding.**
This level demonstrates that encoding (Base64, Hex) is not a security measure. Unlike encryption, encoding is a two-way transformation designed to represent data in different formats. If the encoding algorithm is known, the original data can be easily recovered through "Reverse Engineering".
#### Key Commands
- **`xxd -r -p`**: Converts plain hexadecimal strings back into binary/string format.
- **`rev`**: Reverses the character order of a string.
- **`base64 -d`**: Decodes a Base64 encoded string.
#### Walkthrough / Resolution
`echo -n "3d3d516343746d4d6d6c315669563362" | xxd -r -p | rev | base64 -d`
- Analyzed the provided PHP source code to understand the `encodeSecret` function: `bin2hex(strrev(base64_encode($secret)))`.
- Identified the stored `$encodedSecret` value: `3d3d516343746d4d6d6c315669563362`.
- Executed a reverse pipeline in the terminal to decode the secret step-by-step:
    - Converted the Hex string to binary.
    - Reversed the resulting string.
    - Decoded the Base64 result.
- The final output was the original secret: `oubWYf2kBq`.
- Submitted the secret to the form to retrieve the password for `natas9`.
#### Key Takeaways / Lessons Learned
- **Encoding is not Encryption:** Never store secrets using reversible encoding methods.
- **Pipeline Logic:** Complex transformations can be broken down and reversed by applying inverse functions in the exact opposite order.
#### Pass 9
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
