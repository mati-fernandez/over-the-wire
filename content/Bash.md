# What is Bash?
Bash (Bourne Again Shell) is a command-line interpreter used in Linux and Unix systems.
It executes commands, runs scripts, and manages system interaction.

---
# What Bash does
- interprets commands
- expands variables
- handles pipes
- executes programs
- runs scripts

---
# Core concepts
## Variables
```bash
echo $HOME
```

---
## Command substitution
```bash
echo $(pwd)
```

---
## Functions
```bash
myfunc() {
  echo "hello"
}
```

---
## Input/output
- stdin → input stream
- stdout → output stream
- stderr → errors

---
# Why Bash matters in security
Bash is often involved in:
- command injection vulnerabilities
- privilege escalation
- system enumeration
- CTF challenges (Bandit, Natas)

---
# Key idea
Bash is not just a terminal language.
It is:
> a full execution layer between user input and the operating system

---
# Related
- [[Shell]]
- [[Variable Expansion]]
- [[Command Substitution]]
- [[Standard Input (stdin)]]