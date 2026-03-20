#### Concept
**Git Push and Ignored Files:** Sometimes the challenge is not extracting information, but interacting with the remote server. `.gitignore` files are used to prevent sensitive or temporary files from being uploaded to the repo. In security, however, this can be a trap to prevent an auditor from "seeing" or uploading their tools.
#### Key Commands
- `git add -f [file]`: The `-f` (force) flag forces Git to track a file even if it is blacklisted in `.gitignore`.
- `rm .gitignore`: An alternative way is simply deleting the ignore file altogether.
- `git push`: Uploads your local changes to the remote server.
#### Walkthrough / Resolution
- **Cloning:** Cloned the Level 31 repository.
- **Task:** The `README.md` required creating a file named `key.txt` with the content: `May I come in?`.
- **The Obstacle:** When attempting to add it, Git rejected the file due to `.gitignore` rules.
- **Bypass:** Forced the staging of the file using `git add -f key.txt`.
- **Execution:** Committed the change and pushed it: `git commit -m "Submit key"` followed by `git push`.
- **Extraction:** Upon processing the push, the OverTheWire server triggered an automated script that read the file and returned the next password via the terminal output.
#### Key Takeaways / Lessons Learned
A `.gitignore` file is not a real security measure; it is merely a developer convenience. As an attacker or auditor, you should always check which files are being ignored, as they often hide configuration files or keys that the developer doesn't want "traveling" through the repository history.
#### Pass 32
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
