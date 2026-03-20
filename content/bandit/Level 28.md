#### Concept
**Persistence in Git History:** Deleting sensitive information from the "present" (the latest commit) does not remove it from the Git database. If a file was uploaded with a password and then edited to remove it, the original version still exists within Git objects.
#### Key Commands
- `git log`: Displays the chronological list of changes (commits).
- `git log -p [file]`: Shows the history of a specific file, detailing which lines were removed (`-`) and which were added (`+`).
- `git show [commit_id]`: Allows viewing the exact content of a specific change from the past.
#### Walkthrough / Resolution
- **Cloning:** Downloaded the repository using Git.
- **Identification:** The current `README.md` had the password censored with `XXXXX`.
- **Investigation:** Ran `git log -p` to inspect previous states of the file.
- **Extraction:** Located a commit where the developer replaced the actual password with `X`s. The line marked in red (`-`) contained the valid key.
#### Key Takeaways
Git history is immutable by default. Deleting a password in the last commit does not purge it from the repository's database. An attacker can always use `git log -p` to view "diffs" and recover overwritten sensitive information. In a real-world scenario, the only secure fix is to **rotate the secret** (invalidate and change it) or use specialized tools to rewrite the history (though this is discouraged in collaborative environments).
#### Pass 29
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
