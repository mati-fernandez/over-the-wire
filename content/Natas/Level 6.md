#### Concept
**Sensitive File Exposure (Inclusion Files).**
Developers often use "include" files (`.inc`, `.php`, `.conf`) to store variables or secrets. If the web server is not configured to restrict access to these file types or directories, an attacker can access them directly via URL and read the sensitive data within.
#### Key Commands
- **URL Manipulation:** Appending the include path found in the source code to the base URL.
- **View Source (Ctrl+U):** Necessary if the `.inc` file contains PHP tags that render as an empty page in the browser.
#### Walkthrough / Resolution
- Accessed `natas6` and inspected the source code.
- Found a reference to an included file: `include "includes/secret.inc";`.
- Navigated to `http://natas6.natas.labs.overthewire.org/includes/secret.inc`.
- Located the variable `$secret = "FOEIUWGHFEEUHOFUOIU"`.
- Entered the secret into the original form to receive the password for `natas7`.
#### Key Takeaways / Lessons Learned
- **Access Control:** Directories containing sensitive logic or secrets (like `/includes` or `/config`) should be protected by server rules (e.g., `.htaccess` or Nginx `deny all`).
- **File Extensions:** Sensitive files should use extensions that the server is forced to parse as code (like `.php`) or be stored outside the web root (`public_html`) entirely.
#### Pass 7
bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
