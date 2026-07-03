# What are Magic Bytes?
**Magic bytes** (also called **file signatures**) are the first bytes of a file that identify its format.
They allow programs to determine a file's type by inspecting its contents rather than relying on its extension.

---
# Why are they needed?
File extensions can be renamed easily:
```text
photo.jpg
↓
photo.exe
```
The extension changes, but the file contents remain the same.
Magic bytes provide a more reliable way to identify the actual file format.

---
# Common file signatures

| File Type | Magic Bytes | ASCII |
|-----------|------------|-------|
| GIF | `47 49 46 38 39 61` | `GIF89a` |
| GIF | `47 49 46 38 37 61` | `GIF87a` |
| PNG | `89 50 4E 47 0D 0A 1A 0A` | `.PNG....` |
| JPEG | `FF D8 FF` | _(binary)_ |
| PDF | `25 50 44 46` | `%PDF` |
| ZIP | `50 4B 03 04` | `PK..` |
| Windows Executable | `4D 5A` | `MZ` |
| ELF Executable | `7F 45 4C 46` | `.ELF` |

---
# How applications use them
Many libraries inspect only the beginning of a file.
Example:
```php
exif_imagetype($file)
```
Checks the file signature to determine whether it is a supported image format.

---
# Security implications
Magic bytes improve file identification but **do not guarantee that a file is safe**.
An attacker may prepend a valid signature to malicious content:
```php
GIF89a
<?php echo file_get_contents("/etc/passwd"); ?>
```
An image validator accepts the file because it begins with `GIF89a`, while the PHP interpreter later executes the code inside `<?php ... ?>`.
This is a common technique for bypassing weak upload validation.

---
# Limitations
Magic bytes only identify the beginning of a file.
They do **not** verify:
- the entire file structure
- whether the file is well-formed
- embedded malicious content
- whether the server should execute the file

---
# Detection tools
Linux:
```bash
file image.png
```
Hex dump:
```bash
xxd image.png | head
```
or
```bash
hexdump -C image.png | head
```

---
# Takeaway
Magic bytes identify **what a file appears to be**, not **everything it contains**. They should be combined with proper extension validation, content parsing, and safe upload handling.

---
# Related
- [[hexdump]]
- [[Arbitrary File Upload]]
- [[RCE]]
- [[Polyglot File]]