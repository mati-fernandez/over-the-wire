#### Summary
The application stores user preferences inside a cookie protected with **repeating-key XOR** and Base64 encoding. Since part of the plaintext is known, the XOR key can be recovered (**Known Plaintext Attack**). The cookie can then be forged with `"showpassword":"yes"` to reveal the next password.
#### Target
- `data` cookie (user-controlled)
- `loadData()`
- `xor_encrypt()`
- `json_decode()`
#### Exploit
1. Capture the `data` cookie.
2. URL-decode and Base64-decode it.
3. Recover the repeating XOR key using the known JSON plaintext.
4. Forge a new cookie with `"showpassword":"yes"`.
5. Replace the original cookie and refresh the page.
#### Payloads / Commands
Recover the XOR key:
```
Key: kBSw
```
Scripts:
- [[exploit11#recover-key.js]]
- [[exploit11#forge-cookie.js]]
#### Why it works
The application encrypts a client-controlled cookie using **repeating-key XOR**, which is vulnerable to a **Known Plaintext Attack**. Since the cookie's JSON structure is predictable, the XOR key can be recovered by XORing the ciphertext with the known plaintext. The recovered key can then be used to forge arbitrary cookie contents.
#### Real-world Notes
- Repeating-key XOR provides no integrity and is vulnerable to known-plaintext attacks.
- Sensitive client-side data should be authenticated (e.g., [[HMAC]] or authenticated encryption), not simply encrypted.
- Modern applications typically store sensitive state server-side or use authenticated tokens.
#### Takeaways
- Repeating-key XOR is insecure for protecting client-controlled data.
- Base64 is only an encoding layer.
- Always analyze the complete data transformation pipeline (URL Encoding → Base64 → XOR → JSON).
- Predictable plaintext can completely break weak encryption schemes.
#### Pass 12
EAGkE8uzFTxeoTT2mMst9Xy7PX6guEng
