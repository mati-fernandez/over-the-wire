#### Concept
**Data Exfiltration via Git:** Version control (Git) is a developer tool, but in security, it is a critical source of information. If a repository has read permissions, an attacker can clone the entire project to their local machine to analyze code and history for forgotten credentials.
#### Key Commands
- `git clone [URL]`: Copies a remote repository (including all history and files) to a local directory.
- `ls -la`: Allows viewing hidden files (such as the `.git` folder) within the cloned repository.
#### Command Anatomy (The URL)
The structure used was: `ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo`
- `ssh://`: Secure transfer protocol.
- `bandit27-git`: Repository user (uses bandit27's password).
- `bandit.labs.overthewire.org:2220`: Game server and port.
- `/home/bandit27-git/repo`: Physical path of the repository on the OverTheWire server.
#### Resolution
- **Cloning:** Ran the `git clone` command. When prompted for a password, used the one from Level 27.
```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```
- **Inspection:** Entered the automatically created directory (`cd repo`) and listed the files.
- **Extraction:** Read the text file (e.g., `README`) which contained the next level's password.
#### Key Takeaways
- **Git Security:** Never upload files containing passwords to version control. Even if deleted later, they remain stored forever in previous commits.
- **Local vs. Remote:** The `git clone` command doesn't just download files; it establishes a bridge between your local folder and the server's absolute path.
#### Pass 28
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
