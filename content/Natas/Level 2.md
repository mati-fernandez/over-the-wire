#### Concept
**Information Disclosure & Directory Listing.**
This level demonstrates how misconfigured web servers can expose sensitive files through "Directory Indexing". If a folder (like `/files/`) doesn't have an `index.html` or `index.php` file, and the server is not configured to deny access, it will list all its contents to any visitor.
#### Key Commands
- **URL Manipulation:** Appending directory paths to the base URL (e.g., `/files/`).
- **DevTools (F12):** Used to inspect the `src` attribute of elements to discover hidden paths.
#### Walkthrough / Resolution
- Authenticated into `natas2`.
- Inspected the source code and found an image tag: `<img src="files/pixel.png">`.
- Noticed the image is stored in a subdirectory called `files/`.
- Navigated to `http://natas2.natas.labs.overthewire.org/files/`.
- The server displayed a directory listing containing `pixel.png` and `users.txt`.
- Opened `users.txt`, which contained credentials for several users, including `natas3`.
#### Key Takeaways / Lessons Learned
- **Disable Directory Listing:** Production servers should always have directory indexing disabled to prevent reconnaissance.
- **Sensitive Files:** Never store files containing credentials (`users.txt`, `.env`, `config.php`) in publicly accessible directories.
- **Reconnaissance:** Even a single image source can reveal the internal structure of a web application.
#### Pass 3
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
