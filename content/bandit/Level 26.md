#### Concept
**Shell Breakout (Vim Escape):** The `bandit26` user's default shell is `/usr/bin/showtext`, which terminates the session immediately after execution. To run complex commands (like the `bandit27-do` binary), it is necessary to force the system into a real shell (`/bin/bash`) by "hijacking" the Vim process.
#### Key Commands
- `:set shell=/bin/bash`: Defines which program Vim should execute when a shell is requested.
- `:shell`: Vim command to suspend the editor and provide an interactive terminal.
- `./bandit27-do [command]`: A SUID binary that allows executing actions as the next user (`bandit27`).
#### Walkthrough
- **Entry Point:** Repeated the small-window trick from the previous level to trigger `more` and enter `vi`.
- **Environment Setup:** By default, Vim's shell was still the restrictive script. This was manually overridden using `:set shell=/bin/bash`.
- **Escape:** Executed `:shell`, which finally granted a stable prompt: `bandit26@bandit:~$`.
- **Completion:** With a functional shell, executed `./bandit27-do cat /etc/bandit_pass/bandit27` to retrieve the next password.
#### Key Takeaways
"Escaping" consists of redirecting the execution flow. We moved from a script that reads and closes to an editor that opens and maintains a sub-shell. This is a fundamental technique for post-exploitation in restricted environments.
#### Pass 27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
