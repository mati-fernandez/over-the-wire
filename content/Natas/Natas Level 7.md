#### Summary
Local File Inclusion vulnerability due to unsafe concatenation of user input into a server-side `include()` call.
#### Target
The `page` GET parameter used to determine which file is included.
#### Exploit
1. Authenticate using the provided credentials.
2. Inspect the URL parameter `page`.
3. Modify the parameter to traverse directories or access sensitive files.
4. Retrieve the password from `/etc/natas_webpass/natas8`.
#### Payloads / Commands
Browser:
```text id="n7p1"
?page=/etc/natas_webpass/natas8
```
or directory traversal:
```text id="n7p2"
?page=../../../../etc/natas_webpass/natas8
```
#### Why it works
The application directly concatenates user-controlled input into a file path without validation. Since `include()` executes server-side file loading, an attacker can manipulate the path to read sensitive files outside the intended directory.
#### Takeaways
* Never concatenate user input into file system paths.
* Validate and sanitize file inclusion parameters.
* Use whitelists instead of dynamic file paths.
* `include()` + user input = high-risk combination.
#### Pass 8
ugXL95KQmUAJJj6bMezOlBNDyI9Imwkc
