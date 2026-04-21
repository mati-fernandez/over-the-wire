#### Concept
**OS Command Injection.**
This vulnerability occurs when an application takes user input and embeds it into a system shell command without proper sanitization. By using shell metacharacters like `;`, `&&`, or `|`, an attacker can execute unintended commands with the same privileges as the web server.
#### Key Commands
- **`;` (Semicolon):** Allows running multiple commands in sequence.
- **`ls`:** List directory contents (used for reconnaissance).
- **`cat`:** Standard Unix utility to read and display file contents.
#### Walkthrough / Resolution
- **Reconnaissance:** Tested the injection by entering `; ls ;`. The server returned a list of files, confirming that shell commands could be executed.
- **Information Gathering:** Used `; ls /etc/natas_webpass/` to verify the existence of the password files.
- **Exploitation:** Injected a command to read the target file.
- **Payload:** `; cat /etc/natas_webpass/natas10 ; ""`
    - The first `;` terminates the empty `grep`.
    - The `cat` command reads the password.
    - The trailing `; ""` handles the leftover `dictionary.txt` string in the original PHP command to prevent execution errors.
#### Key Takeaways / Lessons Learned
- **Sanitization is priority:** Never pass raw user input to functions like `passthru()`, `system()`, or `exec()`.
- **Principle of Least Privilege:** Web servers should not have read access to sensitive system files like `/etc/natas_webpass/`.
#### Pass 10
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
