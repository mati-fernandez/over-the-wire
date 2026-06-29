# What is Argument Injection?
**Argument Injection** is a vulnerability where user input is interpreted as additional **arguments** to a command-line program.
Unlike **[[Command Injection]]**, the attacker does **not** execute new commands. Instead, they change how the target program behaves by supplying unexpected options, filenames, or parameters.

---
# Typical vulnerable code
```php
$user = $_GET["input"];
passthru("grep -i $user dictionary.txt");
```
If the application concatenates user input directly into the command, the attacker may inject additional arguments.

---
# Example
Application executes:
```bash
grep -i <input> dictionary.txt
```
Attacker supplies:
```text
.* /etc/passwd
```
Result:
```bash
grep -i .* /etc/passwd dictionary.txt
```
`grep` now searches both files, potentially exposing sensitive information.

---
# Common targets
- `grep`
- `tar`
- `zip`
- `find`
- `curl`
- `ssh`
- `git`
- ImageMagick (`convert`)
Any CLI tool that accepts options and filenames may be vulnerable if arguments are not escaped.

---
# Prevention
- Escape every user-controlled argument (e.g. `escapeshellarg()` in PHP).
- Avoid constructing shell commands with string concatenation.
- Prefer language APIs over external command-line tools.

---
# Related
- [[Command Injection]]
- [[grep]]