#### Concept
**Security through Obscurity & Robots.txt Misconfiguration.** Relying on `robots.txt` to hide directories is a common mistake. Since the file must be world-readable for bots to see it, it also serves as a map for attackers to find hidden or sensitive areas of a site.
#### Key Commands
- **Direct URL access:** `base-url/robots.txt`
- **Directory Traversal:** Accessing the paths listed in the `Disallow` directive.
#### Walkthrough / Resolution
- Navigated to `/robots.txt`.
- Found a `Disallow` entry pointing to a hidden directory.
- Accessed that directory via the browser.
- Found a text file containing the password for `natas4`.
#### Key Takeaways / Lessons Learned
- `robots.txt` is **not** a security mechanism.
- Sensitive directories should be protected by authentication or kept outside the web root, not just "hidden" from search engines.
#### Pass 4
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
