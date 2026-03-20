#### Concept
**Git Tags:** Tags are typically used to mark specific points in history (such as version releases like `v1.0`). However, they can be used to store sensitive information in their metadata or to point to commits that are not linked to any active branch, making them less visible at first glance.
#### Key Commands
- `git tag`: Lists all tags in the repository.
- `git show [tag_name]`: Displays the details and content associated with a specific tag.
#### Walkthrough / Resolution
- **Cloning:** Cloned the Level 30 repository.
- **Exploration:** `ls -la` and `git log` showed no useful information.
- **Detection:** Executed `git tag` and discovered a tag named `secret`.
- **Extraction:** Upon running `git show secret`, the system returned the password for the next level.
#### Key Takeaways
Not everything in a Git repository exists within the files or the branch history. Objects like Tags can contain references to data that do not appear in the main branch. A Git forensic analysis must always include a review of tags.
#### Pass 31
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
