#### Concept
**File Reading via Editor (Vim):** Instead of spawning a functional shell, we exploit the `more` pager's ability to escape into an editor (`vi`). Once inside, internal commands can be used to read files the user has permissions for, even if the interactive shell is restricted.
#### Key Commands
- `ssh -i private_key bandit26@bandit.labs.overthewire.org -p 2220`: Direct connection from local machine to bypass localhost restrictions.
- `stty rows 3`: Forces the server to use a pager for the welcome text by shrinking the terminal display area.
- `v` (inside `more`): Opens the `vi` editor.
- `:r [file]`: Reads the content of a file into the current editor buffer.
#### Walkthrough / Resolution
- **Extraction:** Obtained the `bandit26.sshkey` private key from Level 25.
- **Network Bypass:** Attempting to connect from `bandit25@localhost` failed ("Connecting from localhost is blocked"). Connection was made from the local machine using the copied key.
- **Forcing Pagination:** Resized the terminal window and used `stty rows 3`. Upon connection, the welcome text paused at `--More--`.
- **Direct Access:** Pressed `v` to enter `vi`, then executed `:r /etc/bandit_pass/bandit26`. This displayed the password directly within the editor buffer without needing a shell escape.
#### Key Takeaways
System exploitation isn't always about "breaking" the shell. If you have access to a text editor with the target user's privileges, you can read sensitive information (like `/etc/bandit_pass/...`) directly from the buffer.
#### Why was Bandit 25 rejected?
OverTheWire blocks SSH connections from `localhost` to `localhost` on port 2220 to prevent resource exhaustion from infinite tunneling. Connecting from an external machine (like your WSL) is seen as a legitimate connection. 
**Crucial Step:** You cannot jump to Level 26 from a Bandit 25 session. You must exfiltrate the private key, save it locally (`chmod 600`), and connect from outside. Otherwise, the server terminates the session before `more` can even trigger.
#### Pass 26
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
