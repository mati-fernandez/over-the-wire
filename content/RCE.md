# What is RCE?
**Remote Code Execution (RCE)** is the ability for an attacker to execute arbitrary code or operating system commands on a target machine.
It is considered one of the most severe vulnerability impacts.

---
# Common paths to RCE
- [[Command Injection]]
- Deserialization vulnerabilities
- File upload vulnerabilities
- Template Injection
- Memory corruption (e.g. buffer overflows)

---
# Typical impact
- Read or modify files.
- Execute system commands.
- Install malware.
- Create new users.
- Steal credentials.
- Escalate privileges.
- Gain persistent access.

---
# Example
A vulnerable application executes:
```php
passthru($_GET["cmd"]);
```
An attacker sends:
```text
id
```
The operating system executes the command and returns its output.

---
# Notes
RCE is **not** a vulnerability by itself. It is usually the **impact** of another vulnerability.
For example:
- Command Injection → may lead to RCE.
- Deserialization → may lead to RCE.
- File upload → may lead to RCE.

---
# Related
- [[Command Injection]]
- [[Argument Injection]]