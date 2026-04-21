#### Concept
**Command Injection Bypass via Input Manipulation.**
The application filters common shell metacharacters like `;`, `&`, and `|` to prevent command chaining. However, it still passes user input directly as an argument to the `grep` command.
#### Key Commands
- **`grep`**: A command-line utility for searching plain-text data sets for lines that match a regular expression.
- **`.` (Wildcard)**: Matches any single character.
- **`.*`**: Matches any sequence of characters.
#### Walkthrough / Resolution
- **Analysis**: The server executes `grep -i $key dictionary.txt`. Since separators are blocked, we cannot start a new command (like `cat`).
- **Exploitation**: Instead of adding a new command, we manipulate the existing `grep` command to read multiple files. `grep` accepts a pattern followed by multiple file paths.
- **Payload**: `.* /etc/natas_webpass/natas11`
    - `.*` acts as the search pattern (matching everything).
    - `/etc/natas_webpass/natas11` is added as the first file to search.
    - The original `dictionary.txt` becomes the second file.
- **Outcome**: The server executes `grep -i .* /etc/natas_webpass/natas11 dictionary.txt`, printing the contents of the password file to the screen.
#### Key Takeaways / Lessons Learned
- **Grep is multi-file:** `grep` can process multiple files in a single execution. By providing an additional path, we can force the tool to leak data from files the developer didn't intend to expose. 📂
- **Incomplete Blacklists are Weak:** Filtering specific characters (like `;` or `&`) is often insufficient. A "denylist" approach usually leaves gaps that can be exploited by using the tool's native features (like space-separated arguments). 🛡️
- **The Power of Wildcards:** Using `.` or `.*` in a regex search is a reliable way to dump the entire content of a file when the exact string format is unknown. 🔍
#### Pass 11
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
