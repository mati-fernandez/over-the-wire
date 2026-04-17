#### Concept
**HTTP Referer Spoofing.** The server checks the `Referer` header to authorize access. Since headers are client-side information, they can be easily manipulated by the user to trick the server into believing the request originated from a specific trusted page.
#### Key Commands
- **CLI (WSL/curl):** `curl -u natas4:[pass] --referer http://natas5.natas.labs.overthewire.org/ http://natas4.natas.labs.overthewire.org/`
- **Browser (Console):** Using `fetch()` with a custom `"Referer"` header in the DevTools console.
  This is possible by copying the request as a fetch from the Network tab.
#### Walkthrough / Resolution
- Accessed `natas4` and saw the message: "Access disallowed. You are visiting from...".
- Identified that the server requires the `Referer` header to be `http://natas5.natas.labs.overthewire.org/`.
- Used `curl` with the `--referer` flag to spoof the origin of the request.
- The server accepted the spoofed header and returned the password for `natas5`.
#### Key Takeaways / Lessons Learned
- **Headers are untrusted:** Never use HTTP headers (like Referer or User-Agent) for critical security checks or authentication.
- **Manipulation:** Tools like `curl`, Burp Suite, or browser consoles allow full control over what the client sends to the server.
>**Browser Limitations:** Modern browsers (Chrome, Firefox, etc.) often include security measures that prevent scripts from modifying "Forbidden Header Names" like `Referer`. This is a protection against CSRF attacks. While `fetch()` might appear to execute, the browser may override or strip the custom header. Using tools like `curl` or a specialized intercepting proxy (e.g., Burp Suite) is more reliable as they do not enforce these client-side safety restrictions.
#### Pass 5
0n35PkggAPm2zbEpOU802c0x0Msn1ToK
