#### Concept
**Information Leakage in Branches:** In real-world projects, developers use various branches (e.g., `main`, `dev`, `fix`) to organize work. Often, the main branch is "clean," but development or experimental branches may contain credentials that were forgotten before merging or simply left "alive" in the remote repository.
#### Key Commands
- `git branch -a`: Lists all branches, including remote ones (`remotes/origin/...`) that haven't been checked out locally.
- `git checkout [branch]`: Switches the state of your local working directory to the specified branch.
- `git log --all`: Displays the commit history for all existing branches, not just the current one.
#### Walkthrough / Resolution
- **Cloning:** Downloaded the Level 29 repository. The `README.md` stated there were no passwords in production.
- **Detection:** Ran `git branch -a` and discovered a remote branch named `dev` (or similar).
- **Inspection:** Instead of switching branches, a more direct command was used to see all commits across all branches: `git log --all --oneline`.
- **Extraction:** A commit in the development branch contained the password that had been replaced by the "no passwords" message in the main branch. It was retrieved using `git show [commit_hash]`.
#### Key Takeaways
Auditing the main branch (`main`/`master`) is not enough. When performing a security audit on a repository, it is mandatory to inspect all branches and their histories. Development or testing branches are often gold mines for finding debug configurations and access keys that should have never left the developer's local environment.
#### Pass 30
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
