# What is `find`?
`find` is a Unix/Linux command used to recursively search for files and directories based on different criteria such as name, type, owner, permissions, size, or modification time.
It is one of the most useful enumeration tools during CTFs and penetration tests.

---
# Basic Syntax
```bash
find <path> <expression>
```
Examples:
```bash
find . -name "*.txt"
find /home -type f
find /var -type d
```

---
# Common Options
## Search by name
```bash
find / -name "config.php"
```
Case-insensitive:
```bash
find / -iname "config.php"
```

---
## Search by type
Files only:
```bash
find / -type f
```
Directories only:
```bash
find / -type d
```

---
## Search by owner
```bash
find / -user root
```

---
## Search by permissions
Find SUID binaries:
```bash
find / -perm -4000 2>/dev/null
```
Useful during privilege escalation.

---
## Execute a command
```bash
find . -name "*.log" -exec cat {} \;
```
`{}` represents the matched file.
`\;` terminates the `-exec` expression.

---
# Hiding Permission Errors
Searching from the filesystem root often produces many permission errors.
Suppress them with:
```bash
find / -name "*.conf" 2>/dev/null
```
`2>` redirects **stderr**.
`/dev/null` discards the output.

---
# Common Pentesting Examples
Search for configuration files:
```bash
find / -name "*.conf" 2>/dev/null
```
Search for backup files:
```bash
find / -iname "*backup*" 2>/dev/null
```
Search for passwords or secrets:
```bash
find / -iname "*pass*" 2>/dev/null
```
Search for SSH keys:
```bash
find / -name "id_*" 2>/dev/null
```
Search for writable directories:
```bash
find / -writable -type d 2>/dev/null
```

---
# Notes
- `find` searches recursively.
- `.` searches from the current directory.
- `/` searches the entire filesystem.
- Always narrow the search path when possible to improve performance.