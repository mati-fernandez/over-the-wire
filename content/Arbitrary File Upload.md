# What is Arbitrary File Upload?
An **Arbitrary File Upload** vulnerability allows an attacker to upload files that should not be accepted by the application.
Depending on how the server handles uploaded files, this may lead to information disclosure, file overwrite, or [[RCE]].

---
# Common causes
- Trusting the client-provided filename or extension.
- Missing or weak server-side validation.
- Relying only on MIME types or magic bytes.
- Storing uploads inside a web-accessible directory.
- Allowing uploaded scripts to execute.

---
# Typical attack flow
```text
Attacker uploads file
        ↓
Server accepts it
        ↓
File stored on server
        ↓
Attacker accesses or executes it
```

---
# Common bypass techniques
- Changing the file extension (`.php`, `.jsp`, `.aspx`, etc.).
- Double extensions (`image.jpg.php`).
- Magic bytes / file signature bypasses.
- MIME-Type spoofing.
- [[Polyglot File|Polyglot Files]].

---
# Mitigations
- Validate file type server-side.
- Generate server-side filenames.
- Store uploads outside the web root.
- Disable script execution in upload directories.
- Apply strict allowlists for extensions and content types.

---
# Related
- [[Magic Bytes]]
- [[Polyglot File]]
- [[RCE]]