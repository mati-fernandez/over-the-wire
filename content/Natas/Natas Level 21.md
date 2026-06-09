#### Concept
**Cross-Site Session Infusion via Shared Session Storage (Co-location Vulnerability).**
This vulnerability arises from an infrastructure design flaw where multiple distinct web applications deployed on the same server (co-located) share the identical physical storage directory for session files. If one collateral application contains weak input handling logic, an attacker can manipulate their session properties within the insecure boundary and seamlessly carry those elevated state privileges over to the hardened primary application using the shared session identifier.
#### Key Functions & Code Defects
- **The Whitelist Illusion**: The developer defined a `$validkeys` array intended as a whitelist:
```php
$validkeys = array("align" => "center", "fontsize" => "100%", "bgcolor" => "yellow");
```
  However, this was only used to render the CSS/UI components. It was never used as a server-side validation gate for incoming data.
* **Blind Global Assignment**: The core vulnerability lies in the request processing loop:
```php
if(array_key_exists("submit", $_REQUEST)) {
    foreach($_REQUEST as $key => $val) {
        $_SESSION[$key] = $val; // <--- Root Cause: Unsanitized mapping
    }
}
```
This logic allows any arbitrary key-value pair included in the HTTP request to be injected directly into the session file.
#### Walkthrough / Resolution
- **Infrastructure Recon**: Identified that the primary domain shares session storage with `natas21-experimenter`.
- **Intercept & Inspect**: Accessed the experimenter site and used the **Network tab (F12)** to capture a legitimate `POST` request to `index.php` after clicking "Update".
- **Manual Request Tampering**: Used the browser's native **"Edit and Resend"** feature. The original body (`align=center&fontsize=100%&bgcolor=yellow&submit=Update`) was manually appended with the injection payload: **`&admin=1`**.
- **Session Carry-over**: After sending the tampered request, the server-side session was successfully updated with `admin => 1`. The `PHPSESSID` cookie was then copied and injected into the `natas21` primary domain. Refreshing the main page bypassed the admin check due to the shared backend session file.
#### Key Takeaways / Lessons Learned
- **Isolate Application Contexts**: Co-located web components should never share resource spaces, databases, or temporary cache files (like `/var/lib/php/sessions`). Use isolated containers, unique application scopes, or independent session prefixes.
- **Strict Whitelisting Over Global Assignments**: Superglobal variable matrices like `$_REQUEST` should never be implicitly trusted to bind internal session fields. Explicitly copy only expected boundaries.
#### Pass 22
d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
