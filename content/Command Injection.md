# What is Command Injection?
**Command Injection** is a vulnerability that allows an attacker to execute arbitrary operating system commands by injecting input into a shell command constructed by the application.
It typically occurs when user input is concatenated into a command without proper validation or escaping.

---
# Typical vulnerable code
```php
$user = $_GET["input"];
passthru("grep -i $user dictionary.txt");
```
If the application does not sanitize the input, the shell interprets special characters as part of the command.

---
# How it works
Application:
```text
User Input
     │
     ▼
Application builds a shell command
     │
     ▼
Shell parses the command
     │
     ▼
Operating System executes it
```
The vulnerability exists because the **shell**, not the application, interprets the final command string.

---
# Common shell metacharacters
|Character|Purpose|
|---|---|
|`;`|Execute the next command.|
|`&&`|Execute the next command only if the previous one succeeds.|
|`\|`|Execute the next command only if the previous one fails.|
|`|`|
|`` `cmd` ``|Command substitution.|
|`$(cmd)`|Command substitution (modern syntax).|
|`>`|Redirect output to a file.|
|`<`|Redirect input from a file.|

---
# Example
User input:
```text
; cat /etc/passwd
```
Application builds:
```bash
grep -i ; cat /etc/passwd dictionary.txt
```
The shell executes both commands, allowing the attacker to read sensitive files.

---
# Impact
Depending on the application's privileges, Command Injection may allow an attacker to:
- Read sensitive files.
- Execute arbitrary system commands.
- Modify or delete files.
- Install malware.
- Obtain Remote Code Execution (RCE).
- Escalate privileges.

---
# Command Injection vs. Argument Injection
## Command Injection
The attacker breaks the shell command and executes **new commands**.
Example:
```text
; cat /etc/passwd
```
Requires shell metacharacters such as `;`, `|`, `&&`, or `$()`.

---
## [[Argument Injection]]
The attacker does **not** execute new commands.
Instead, they change how the target program interprets its arguments.
Example:
```text
.* /etc/passwd
```
The shell remains intact, but the injected arguments alter the behavior of the executed program.

---
# Prevention
- Avoid executing shell commands whenever possible.
- Use language APIs instead of external CLI tools.
- Escape user input (e.g., `escapeshellarg()` in PHP).
- Prefer allowlists over blacklists.
- Validate all user-controlled input.

---
# Related
- [[Argument Injection]]
- [[grep]]
- [[Shell]]
- [[RCE]]