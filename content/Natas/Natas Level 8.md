#### Summary
A secret was protected using reversible encoding instead of proper cryptography.
#### Target
The encoded secret embedded in the application's source code.
#### Exploit
1. View the application source code (`index-source.html`).
2. Identify the `encodeSecret()` function:
   ```php
   function encodeSecret($secret) {
       return bin2hex(strrev(base64_encode($secret)));
   }
   ```
3. Reverse each transformation in the opposite order to recover the original secret.
4. Submit the decoded secret to obtain the password for the next level.
#### Payloads / Commands
```bash
echo "3d3d516343746d4d6d6c315669563362" | xxd -r -p | rev | base64 -d
```
Command breakdown:
* `echo` prints the encoded secret to standard output.
* `|` pipes the output of one command into the next.
* `xxd`
	* `-r` (**reverse**) converts a [[hex dump]] back into binary.
	* `-p` (**plain**) expects a plain hexadecimal string without offsets or formatting.
* `rev` reverses the character order of each input line.
* `base64`
	* `-d` (**decode**) decodes Base64-encoded data.
Overall transformation:
```
bin2hex()        → xxd -r -p
strrev()         → rev
base64_encode()  → base64 -d
```
#### Why it works
The application protects the secret using reversible encoding functions rather than encryption. Because the algorithm is exposed and every transformation is reversible, the original secret can be reconstructed.
#### Takeaways
* Encoding is not encryption.
* Security should rely on secret keys, not secret algorithms.
* Understanding how data is transformed makes it possible to reverse the process.
#### Pass 9
UdxmI27dTaXmnd1rxKQTfws6jihTdcQ9
