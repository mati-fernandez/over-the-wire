# What is Command Substitution in Bash?
Command substitution allows the output of a command to be used as part of another command.

---
# Syntax
```bash
$(command)
```
or legacy:
```bash
`command`
```

---
# Example
```bash
echo $(pwd)
```
## Step-by-step:
1. Bash executes `pwd`
2. Captures output
3. Replaces `$(pwd)` with that output
4. Executes final command

---
# Real use cases
- dynamic paths
- script automation
- chaining commands
- CTF exploitation (command injection)

---
# Example in security context
```bash
curl http://target/$(whoami)
```
If vulnerable → command injection

---
# Related
- [[Variable Expansion]]
- [[Shell]]