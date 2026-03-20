#### Concept
Handling encoded data (Base64).
#### Key Commands
`base64 -d`
#### Walkthrough
The password is stored in `data.txt` as a Base64 encoded string. To retrieve the clear-text password, we use the `base64` utility with the `-d` (decode) flag.

```bash
base64 -d data.txt
```
#### Key Takeaways
- **Encoding vs. Encryption:** Base64 is NOT encryption; it is an encoding scheme used to represent binary data in an ASCII string format.
- **Flags matter:** Running `base64` without flags will **encode** the input instead of decoding it.
#### Pass 11
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr