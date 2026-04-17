#### Concept
**Local File Inclusion (LFI).**
LFI occurs when an application includes a file without properly sanitizing the input, allowing an attacker to manipulate the input and inject paths to files on the local server. This can lead to sensitive information disclosure or even remote code execution.
#### Key Commands
- **Path Traversal / Absolute Paths:** Using direct paths like `/etc/natas_webpass/natas8` in URL parameters.
- **URL Parameter Manipulation:** Changing values in the query string (`?page=...`).
#### Walkthrough / Resolution
- Accessed `natas7` and noticed the URL structure when navigating through "Home" and "About": `index.php?page=home`.
- Inspected the source code and found a hint in a comment: `<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->`.
- Replaced the value of the `page` parameter with the provided absolute path: `index.php?page=/etc/natas_webpass/natas8`.
- The server executed the `include` command on that path and rendered the content of the password file directly onto the page.
#### Key Takeaways / Lessons Learned
- **Input Validation:** Never trust user input in functions that interact with the file system (`include`, `require`, `file_get_contents`).
- **Whitelisting:** Instead of allowing any path, use a whitelist of allowed files (e.g., only "home" and "about").
- **Permissions:** Web applications should run with the minimum necessary privileges so they cannot read sensitive system files like those in `/etc/`.
#### Pass 8
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
