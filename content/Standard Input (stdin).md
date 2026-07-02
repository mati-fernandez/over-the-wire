# What is stdin?
`stdin` is the default input stream used by programs to receive data.

---
# The 3 standard streams
- stdin → input
- stdout → output
- stderr → errors

---
# Example
```bash
echo "hello" | grep h
```
Flow:
```text
echo → stdout
        ↓
      pipe
        ↓
grep → stdin
```

---
# Direct stdin input
```bash
cat
hello
```
`cat` reads from stdin until EOF.

---
# Redirection
```bash
command < file.txt
```
means:
- take input from file instead of keyboard

---
# Heredoc uses stdin
```bash
cat << EOF
hello
EOF
```
Everything between markers goes to stdin.

---
# Why it matters in security
Many vulnerabilities involve:
- injection into stdin-based commands
- uncontrolled input pipelines
- command chaining via pipes

---
# Related
- [[Command Substitution]]
- [[Shell]]