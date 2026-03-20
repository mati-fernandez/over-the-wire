#### Concept
SSH Private Key Authentication (Identity Files). This level requires moving the key to a local environment because the server blocks internal jumps via localhost.
#### Key Commands
- `scp -P 2220`: Downloads files from the server to the local machine.
- `ssh -i`: Logs in using an identity file instead of a password.
- **Windows GUI (Security):** Managing NTFS permissions (Disabling inheritance).
#### Walkthrough
`scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private .`
I downloaded `sshkey.private` using `scp`. Since Windows doesn't handle `chmod` like Linux, I used the **Properties > Security** GUI to disable inheritance and grant "Read" permissions only to my user. Then, I connected to `bandit14@bandit.labs.overthewire.org` on port 2220.
#### Key Takeaways
I learned that SSH rejects "exposed" keys (those with shared permissions). In Windows, this is fixed by breaking permission inheritance in the GUI to ensure the file is private.
#### Pass 14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS