#### Summary
Information disclosure through HTML source code. Sensitive data was exposed inside an HTML comment sent to the client.
#### Target
Client-side HTML source code.
#### Exploit
1. Authenticate using the provided credentials.
2. View the page source.
3. Locate the HTML comment containing the password for the next level.
#### Payloads / Commands
```bash
curl -u natas0:natas0 http://natas0.natas.labs.overthewire.org
```
Browser:
- `Ctrl + U` (View Source)
- `F12` → Elements
#### Why it works
HTML comments are included in the HTTP response and delivered to the client. Although they are not rendered by the browser, anyone can inspect the source code and read their contents.
#### Takeaways
- Never store secrets in client-side code.
- HTML comments do not provide security.
- Always inspect the page source during web reconnaissance.
#### Pass 1
scfWG6qNEIdzqVyfRwEGXyNUfFZkZeQ7
