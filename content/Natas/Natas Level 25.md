#### Concept
**Chaining two vulnerabilities together: Local File Inclusion (LFI) and Log Poisoning.**
The application tries to block directory traversal and access to `natas_webpass`, but user-controlled data is written into log files without sanitization. By injecting PHP code into the User-Agent and including the log file through LFI, arbitrary PHP code gets executed.
#### Key Commands
```bash
# Trigger log entry with a malicious User-Agent
curl -A '<?php echo file_get_contents("/etc/natas_webpass/natas26"); ?>' \
-u natas25:ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws \
"http://natas25.natas.labs.overthewire.org/?lang=....//....//....//....//....//etc/passwd"

# Include the session log file
http://natas25.natas.labs.overthewire.org/?lang=....//....//....//....//....//var/www/natas/natas25/logs/natas25_<PHPSESSID>.log
```
#### Walkthrough / Resolution
- Looking at the source code, `safeinclude()` attempts to prevent directory traversal by removing `"../"` with `str_replace()`. This can be bypassed using `....//`, because after replacement it becomes `"../"` again.
- Another check blocks any path containing `natas_webpass`, preventing direct access to the password file.
- The `logRequest()` function stores the HTTP User-Agent inside a log file named after the current PHP session. Since the User-Agent is fully controllable, PHP code can be injected into the log (log poisoning).
- After forcing a log entry, the log file itself can be included through the LFI vulnerability. PHP executes the injected code and prints the contents of `/etc/natas_webpass/natas26`, revealing the password for the next level.
#### Key Takeaways / Lessons Learned
- Blacklist-based filtering is fragile and easy to bypass.
- Input written to logs can become dangerous when logs are later included or executed.
- Multiple low-severity vulnerabilities can be chained into Remote Code Execution.
- Always sanitize logged data and avoid including user-controlled files.
#### Pass 26
