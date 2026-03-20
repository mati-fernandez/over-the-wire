#### Concept
**Cronjobs & Insecure Temporary Files:** The use of automated tasks that deposit sensitive information into globally writable directories (like `/tmp`) with excessive permissions.
#### Key Commands
- - **`cat /etc/cron.d/[name]`:** To inspect scheduled tasks.
- **`&> /dev/null`:** Total redirection to the system's "black hole" (silencing output).
#### Walkthrough
I investigated the cron configuration in `/etc/cron.d/` and found a scheduled task for the user `bandit22`. The cron job executed a script every minute. Upon inspecting said script, I discovered it dumped the password for the next level into a temporary file within `/tmp/` with public read permissions. Simply reading that temporary file was enough to obtain the credential.
#### Key Annotations
I learned to trace automation in Linux. If a process has more privileges than I do and runs a script, that script is an attack surface. I also understood the basic syntax of crontab files. 
**Security Note:** This is a prime example of **Insecure File Permissions**. The administrator is storing sensitive information in a public folder (`/tmp`).
#### Pass 22
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q