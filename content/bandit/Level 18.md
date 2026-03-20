#### Concept
SSH Non-interactive Shell / Command Execution. Bypassing startup scripts (`.bashrc` / `.profile`) that force a logout.
#### Key Commands
`ssh [user]@[host] "[command]"`: Executes a remote command without starting an interactive session.
#### Walkthrough
The bandit18 server was immediately closing the connection upon a normal login attempt ("Bye bye!"). To bypass this, I used SSH to directly execute the cat readme command from my local terminal. By not requesting an interactive shell, the "auto-exit" script was not triggered, allowing me to read the file.
#### Key Takeaways
I learned that SSH is not just for "entering" a remote computer; it serves as a tunnel to execute isolated instructions. This is fundamental for server automation and bypassing shell restrictions. SSH has two modes: **Interactive** (provides a terminal to type in) and **Non-interactive** (executes a command, returns the text, and disconnects). By putting a command in quotes at the end, SSH assumes you only want the result of that instruction and skips the full "shell" loading that was kicking me out.
#### Pass 19
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
