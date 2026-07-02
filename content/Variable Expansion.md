# What is variable expansion (bash)?
Variable expansion is the process where [[Bash]] replaces variable references with their actual values before executing a command.

---
# Environment variables
Variables like:
```bash
$HOME
$PATH
$USER
```
are stored in the shell environment and expanded when referenced.
Example:
```bash
echo $HOME
```
Becomes:
```bash
echo /home/user
```

---
# Command substitution
Bash can also replace commands with their output using:
```bash
$(command)
```
Example:
```bash
echo $(pwd)
```
Step-by-step:
1. Bash executes `pwd`
2. Captures output
3. Substitutes it into the command
Result:
```text
/home/user
```

---
# Expansion rules
## Double quotes " "
Allows expansion:
```bash
echo "$HOME"
echo "$(pwd)"
```
## Single quotes ' '
Disables expansion:
```bash
echo '$HOME'
echo '$(pwd)'
```
Output is literal text.

---
# Why this matters
Understanding expansion is critical in:
- shell scripting
- command injection vulnerabilities
- secure handling of user input
- CTF challenges (e.g., Natas, Bandit)

---
# Common mistake
```bash
echo "<?php echo file_get_contents("$HOME"); ?>"
```
Breaks because `$HOME` is expanded inside a string.

---
# Related
- [[Shell]]
- [[Command Substitution]]
- [[Heredoc]]