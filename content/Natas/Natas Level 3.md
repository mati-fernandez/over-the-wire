#### Summary
Sensitive files were exposed through a publicly accessible directory referenced in `robots.txt`.
#### Target
The `robots.txt` file and publicly accessible web directories.
#### Exploit
1. Authenticate using the provided credentials.
2. Inspect the `robots.txt` file.
3. Discover the hidden `/s3cr3t/` directory.
4. Browse the directory and open the `users.txt` file.
5. Retrieve the password for the next level.
#### Payloads / Commands
```bash
curl -u natas3:<password> http://natas3.natas.labs.overthewire.org/robots.txt
curl -u natas3:<password> http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
```
Browser:
* `/robots.txt`
* `/s3cr3t/users.txt`
#### Why it works
The `robots.txt` file is publicly accessible and intended to guide search engine crawlers. It does not enforce access control, so anyone can read it and discover hidden directories.
#### Takeaways
* `robots.txt` should never be used to hide sensitive resources.
* Hidden or unlinked directories are not secure.
* Always inspect common discovery files during web reconnaissance (`robots.txt`, `sitemap.xml`, etc.).
#### Pass 4
JDrPnuZAKyl6MkiqQGFIddrqpvgOASth

