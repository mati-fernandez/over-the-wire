#### Concept
**Insecure Session Management - Cookies.**
The server uses a client-side cookie to track authentication status. Since cookies are stored on the user's machine and can be easily modified, relying on a simple boolean flag (like `0` or `1`) for security is a critical vulnerability.
#### Key Commands
- **Browser (DevTools):** `Application` / `Storage` tab -> `Cookies` section.
- **CLI (curl):** `curl -u natas5:[pass] --cookie "loggedin=1" http://natas5.natas.labs.overthewire.org/`
#### Walkthrough / Resolution
- Accessed `natas5` and received the message: "You are not logged in".
- Opened the browser's Developer Tools and navigated to the Cookies storage.
- Observed a cookie named `loggedin` with its value set to `0`.
- Manually edited the value to `1` and refreshed the page.
- The server checked the modified cookie and granted access to the password.
#### Key Takeaways / Lessons Learned
- **Trust No One:** Never trust data provided by the client. Any information stored in a cookie can be manipulated.
- **Server-Side Sessions:** Authentication state should be managed server-side (e.g., using secure, random session IDs stored in a database) rather than using simple flags on the client side.
#### Pass 6
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
