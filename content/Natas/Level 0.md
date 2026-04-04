#### Concept
**Information Exposure via Source Code.** Web developers sometimes leave sensitive data, such as credentials or internal notes, within HTML comments. While these aren't rendered on the main page, they remain accessible to anyone viewing the raw source code sent by the server.
#### Key Commands
- **Browser:** `Ctrl + U` (View Page Source) or `F12` (DevTools).
- **CLI (WSL):** `curl -u natas0:natas0 http://natas0.natas.labs.overthewire.org`
#### Walkthrough / Resolution
- Accessed the URL and authenticated with the provided credentials (`natas0` / `natas0`).
- Inspected the HTML source code of the landing page.
- Found an HTML comment containing the password for the next level.
#### Key Takeaways / Lessons Learned
- Never store passwords or sensitive information in client-side code (HTML, JS, CSS).
- HTML comments are not a secure way to hide information from users.
- `curl` with the `-u` flag is an efficient way to retrieve page content directly from the terminal.
#### Pass 1
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
