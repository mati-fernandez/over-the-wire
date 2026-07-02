# What is HMAC?
**HMAC** (Hash-based Message Authentication Code) is a mechanism used to verify both:
- **Integrity** (data was not modified)
- **Authenticity** (data comes from someone who knows the secret key)
It is not encryption. It does **not hide data**.

---
# Core idea
HMAC combines:
- a **cryptographic hash function** (e.g. SHA-256)
- a **secret key**
Result:
```text
HMAC = Hash(message + secret_key)
```
But internally it is more secure than simple concatenation.

---
# Why not just use a hash?
If you do:
```text
Hash(message)
```
An attacker can modify the message and recompute the hash.
But with HMAC:
```text
HMAC(message, secret_key)
```
The attacker cannot forge a valid tag without the secret key.

---
# How it works (simplified)
```text
Message + Secret Key
        ↓
Hash Function (twice internally)
        ↓
HMAC Tag
```

---
# Example
Server stores:
```text
data = "showpassword=no"
tag  = HMAC(data, secret)
```
Client sends both:
```text
data + tag
```
Server verifies:
```text
HMAC(received_data, secret) == received_tag
```
If false → data was tampered.

---
# Key property
Any change in the message produces a completely different HMAC:
```text
"no"  → valid tag
"yes" → completely different tag
```
Even a single character breaks verification.

---
# Why HMAC exists
Standard hashes are not enough because:
- hashes are public
- attackers can recompute them
HMAC adds **secrecy to the verification process**.

---
# Where HMAC is used
- API authentication
- JWT signatures (HS256)
- Webhooks (Stripe, GitHub, etc.)
- Session cookies
- Secure token validation

---
# Security note
HMAC does **not encrypt data**.
It only answers:
> “Has this data been modified?”
It does NOT answer:
> “Is this data secret?”

---
# Relation to Natas 11
In [[Natas Level 11]]:
- cookie is **encrypted (XOR)**
- but there is **no integrity check**
So an attacker can:
- modify ciphertext
- recompute nothing
- still pass validation
With HMAC, this attack would fail.

---
# Takeaway
- HMAC = **tamper detection + authenticity**
- Not encryption
- Requires shared secret
- Prevents client-side modification attacks like cookie tampering