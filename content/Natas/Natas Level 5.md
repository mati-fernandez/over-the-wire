#### Summary
Authentication relied on a client-controlled cookie, allowing the login state to be modified by the user.
#### Target
The `loggedin` cookie.
#### Exploit
- Authenticate using the provided credentials.
- Inspect the browser cookies.
- Change the value of the `loggedin` cookie from `0` to `1`.
- Refresh the page to gain access and retrieve the password for the next level.
#### Payloads / Commands
Browser:
- `F12` → **Application** (or **Storage**) → **Cookies**
- Modify: `loggedin=0` to: `loggedin=1`
#### Why it works
The application trusts the value of a client-controlled cookie to determine whether the user is authenticated. Since cookies can be modified by the client, the authentication check can be bypassed.
#### Takeaways
- Never trust client-controlled cookies for authentication or authorization.
- Client-side data must be validated or cryptographically protected.
- Authentication state should be maintained securely on the server or with signed tokens.
#### Pass 6
7mhjtShJAcld2NYbKHEadnhEwRn2P8VT
