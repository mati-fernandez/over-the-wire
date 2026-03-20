#### Concept
SETUID (Set User ID) Binaries. A Unix mechanism that allows users to execute files with the privileges of the file's owner. It is a powerful but dangerous tool if misconfigured (privilege escalation vulnerability).
#### Key Commands
- **`ls -l`:** To identify the `s` bit in permissions (`-rwsr-xr-x`).
- **`./file [command]`:** Execution of the wrapper binary.
#### Walkthrough
1. Ran `ls -l` and located the `bandit20-do` binary, which belongs to user `bandit20` and has the SETUID bit active. 
2. Executed: `./bandit20-do cat /etc/bandit_pass/bandit20`
I used this program as a "bridge" to execute the `cat` command on the next level's password file, which I didn't have direct access to, but the binary's owner did.
#### How did I know the directory?
In Bandit, passwords are conventionally stored in `/etc/bandit_pass/banditX`. In a real-world scenario, you would:
- Read the program's source code (if available).
- Use `strings bandit20-do` to see what paths are hardcoded inside the binary.
- Use intuition/standard paths.
#### Key Takeaways
I learned that Linux permissions go beyond "read, write, and execute." Special bits like SETUID allow for temporary delegation of authority. I realized that if a SETUID binary allows executing arbitrary commands, it represents a massive security hole.
#### Pass 20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

