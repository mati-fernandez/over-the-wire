# What is a Polyglot File?
A **polyglot file** is a file that is valid under two or more different formats or interpretations.
Different programs may interpret the same file differently.

---
# Example
```php
GIF89a
<?php echo file_get_contents("/etc/passwd"); ?>
```
An image validator sees:
```text
GIF89a
```
and considers it a GIF.
The PHP interpreter ignores the plain text until:
```php
<?php
```
then executes the embedded PHP code.

---
# Why it works
Different software parses different parts of the file.
Example:
```text
Upload validator
        ↓
Checks first bytes
        ↓
Accepts GIF
PHP interpreter
        ↓
Finds <?php
        ↓
Executes PHP
```

---
# Security implications
Polyglot files are commonly used to bypass:
- upload restrictions
- magic-byte validation
- weak content validation
They are frequently encountered in CTFs and real-world upload vulnerabilities.

---
# Important
A polyglot file is **not** necessarily valid according to every file format specification.
It only needs to be interpreted successfully by the relevant applications involved in the attack.

---
# Related
- [[Magic Bytes]]
- [[Arbitrary File Upload]]