#### Summary
Client-side restrictions can be bypassed easily. Disabling common browser features does not protect sensitive information.
#### Target
Client-side JavaScript preventing users from viewing the page source through right-click actions.
#### Exploit
1. Authenticate using the provided credentials.
2. Bypass the disabled right-click restriction.
3. View the page source using a browser shortcut or Developer Tools.
4. Locate the HTML comment containing the password for the next level.
#### Payloads / Commands
```bash
curl -u natas1:scfWG6qNEIdzqVyfRwEGXyNUfFZkZeQ7 http://natas1.natas.labs.overthewire.org
```
Browser:
- `Ctrl + U` (View Source)
- `F12` → Developer Tools
#### Why it works
Client-side restrictions only affect the browser's interface. They do not prevent users from accessing the HTML source or the HTTP response, making them ineffective as a security measure.
#### Takeaways
- Never rely on client-side controls for security.
- Browser restrictions can usually be bypassed easily.
- Client-side code should always be considered visible to the user.
#### Pass 2
vsDOxoXyq3wckCP1ZmTZ71ngIA606odB
