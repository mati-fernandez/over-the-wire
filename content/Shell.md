# What is a Shell?
A **shell** is a program that interprets and executes commands entered by a user or another program.
It acts as an interface between the user and the operating system.
Examples include:
- `bash`
- `sh`
- `zsh`
- `fish`
- `cmd.exe` (Windows)
- PowerShell

---
# How it works
```text
User / Application
        │
        ▼
      Shell
        │
        ▼
 Operating System
```
The shell parses the command, expands variables, interprets special characters, and launches programs.

---
# Shell parsing
Before executing a command, the shell processes constructs such as:
- Variables: `$HOME`
- Command substitution: `$(whoami)` or `` `whoami` ``
- Pipes: `|`
- Command separators: `;`
- Conditional execution: `&&`, `||`
- Redirections: `<`, `>`, `>>`
- Wildcards (globbing): `*`, `?`
Example:
```bash
echo "Current user: $(whoami)"
```
The shell first executes `whoami`, then replaces `$(whoami)` with its output before running `echo`.

---
# Why it matters in security
Many applications execute shell commands.
Example:
```php
passthru("grep -i $input dictionary.txt");
```
If user input is concatenated directly into the command, the shell may interpret injected metacharacters, leading to **[[Command Injection]]**.

---
# Shell vs. Program
Consider:
```bash
grep -i hello file.txt
```
There are two distinct stages:
1. **The shell** parses the command line and determines which program to execute.
2. **`grep`** receives the parsed arguments and processes them according to its own syntax.
This distinction is important:
- **Command Injection** abuses the **shell**.
- **Argument Injection** abuses the **target program** after the shell has finished parsing.

---
# Notes
A shell is **not** the operating system itself. It is simply a command interpreter that allows users and applications to interact with the OS.

---
# Related
- [[Command Injection]]
- [[Argument Injection]]
- [[grep]]