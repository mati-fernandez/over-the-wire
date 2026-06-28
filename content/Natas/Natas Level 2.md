#### Summary
Sensitive information was exposed through a publicly accessible directory referenced in the HTML source.
#### Target
HTML source code and publicly accessible web directories.
#### Exploit
1. Authenticate using the provided credentials.
2. Inspect the page source.
3. Identify the `/files/` directory referenced by the image.
4. Browse the directory listing.
5. Open `users.txt` and retrieve the password for the next level.
#### Payloads / Commands
```bash
curl -u natas2:<password> http://natas2.natas.labs.overthewire.org
curl -u natas2:<password> http://natas2.natas.labs.overthewire.org/files/
curl -u natas2:<password> http://natas2.natas.labs.overthewire.org/files/users.txt
```
Browser:
* `Ctrl + U` (View Source)
* `/files/`
* `/files/users.txt`
#### Why it works
The web server allows directory listing, exposing the contents of the `/files/` directory. Since `users.txt` is publicly accessible, anyone can retrieve the credentials.
#### Takeaways
* Never store sensitive files inside publicly accessible web directories.
* Disable directory listing unless it is explicitly required.
* Inspect resource paths in the HTML source during web reconnaissance.
#### Pass 3
K30JrSRHzjxq3paUQuwozY4MNvmNFyhI
