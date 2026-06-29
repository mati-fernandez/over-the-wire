#### Summary
User input is passed directly to `grep` without proper escaping. Although some shell metacharacters are blacklisted, additional **arguments** can still be injected into the command, resulting in **Argument Injection**.
#### Target
The `needle` query parameter, which is concatenated into:
```php
passthru("grep -i $key dictionary.txt");
```
#### Exploit
1. Inspect the source code.
2. Notice that `;`, `|`, and `&` are filtered, preventing the previous Command Injection technique.
3. Analyze `grep`'s syntax:
    ```
    grep [OPTIONS] PATTERN [FILE...]
    ```
4. Supply a pattern that matches every line (`.*`) followed by the target file.
5. `grep` searches both files and prints matching lines, revealing the password.
#### Payloads / Commands
```text
.* /etc/natas_webpass/natas11
```
Resulting command:
```bash
grep -i .* /etc/natas_webpass/natas11 dictionary.txt
```
#### Why it works
The application prevents a few shell metacharacters but still concatenates user input directly into the command line. Since spaces are allowed, an attacker can inject **additional arguments** to `grep`. By providing both a matching pattern and an extra filename, `grep` reads and prints the contents of the protected file.
#### Real-World Notes
Blacklisting a small set of dangerous characters is not an effective defense. Programs that invoke command-line tools should treat **every user-controlled argument** as untrusted.
In a real penetration test, after identifying Argument Injection, it is useful to consult the target program's documentation (e.g., `grep --help` or `man grep`) to understand its syntax, supported options, and argument parsing.
Related notes:
- [[grep]]
- [[Command Injection]]
#### Takeaways
- Blacklists are fragile and easy to bypass.
- Command Injection and Argument Injection are different vulnerability classes.
- Understanding how a CLI tool parses its arguments is often enough to discover an exploit.
- Always escape user input (e.g., `escapeshellarg()` in PHP) or avoid invoking the shell entirely.
#### Pass 11
<% tp.file.cursor(2) %>