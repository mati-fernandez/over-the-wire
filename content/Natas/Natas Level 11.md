#### Concept
**PHP Session Forgery via XOR Encryption Oracle.**
This level demonstrates how relying on client-side cookies for security is dangerous, especially when using a reversible cipher like XOR with a fixed key. If an attacker knows the original plaintext and the resulting ciphertext, they can recover the secret key and forge their own data.
#### Key Commands
- **`XOR (^)`**: A logical operation where $A \oplus B = C$. It is reversible: $A \oplus C = B$.
- **`JSON & Base64`**: The data format used to store the state in the cookie.
- **`atob() / btoa()`**: JavaScript functions to decode and encode Base64 strings.
#### Walkthrough / Resolution
- **Analyze the Source**: The PHP code reveals that the data is stored in a cookie called `data`. The process is: `JSON -> XOR (with secret key) -> Base64`.
- **Identify the Plaintext**: The default data is known: `{"showpassword":"no","bgcolor":"#ffffff"}`.
- **Recover the Key**: Since $Plaintext \oplus Ciphertext = Key$, I took the cookie value from the browser, decoded it from Base64, and performed an XOR operation against the known JSON string. This revealed the repeating key: `eDWo`.
- **Forge the Cookie**:
    - Created a new JSON string: `{"showpassword":"yes","bgcolor":"#ffffff"}`.
    - Encrypted it using XOR with the recovered key `eDWo`.
    - Encoded the result in Base64.
- **Injection**: Replaced the `data` cookie in the browser with the forged string and refreshed the page. The server decrypted the forged cookie, saw `"showpassword":"yes"`, and displayed the password.
#### Key Takeaways / Lessons Learned
- **Never trust client-side data**: Even if encrypted, if the algorithm is weak or the key is recoverable, the data can be tampered with.
- **XOR is not encryption**: Without a unique, random, and secret key for every single message (One-Time Pad), XOR is easily breakable if the attacker knows or can guess part of the plaintext.
- **Server-side state**: Sensitive flags like `showpassword` should always be stored on the server (e.g., in a secure database or server-side session), never sent to the user's browser.
#### Pass 12
yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
