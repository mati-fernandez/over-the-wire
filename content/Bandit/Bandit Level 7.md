#### Concept
Searching for specific strings within a large text file using **grep**.
#### Comandos clave
`grep "millionth" data.txt`
#### Walkthrough
The password is stored in the file `data.txt` next to the word "millionth". Instead of reading the entire file (which is massive), we use `grep` to filter only the line containing that specific keyword.
#### Key Takeaways
- Efficiency in log analysis and data extraction using `grep`.
- Handling large files without overloading the terminal buffer.
#### Advanced One-Liner
The password is located in `data.txt` next to the word "millionth". While a simple `grep` would return the entire line, we can optimize the output to extract **only** the password string.
Instead of cleaning the output manually, we use **Perl-Compatible Regular Expressions (PCRE)** to isolate the secret:
`grep -Po "millionth\s+\K\S+" data.txt`
**Regex Breakdown:**
- **`-P` (--perl-regexp):** Activates the Perl engine, enabling advanced operators like `\s` and `\K`.
- **`-o` (--only-matching):** _Note: In some versions, -P already narrows it down, but -o ensures we only see the match._
- **`millionth`**: Matches the literal anchor word.
- **`\s+`**: Matches one or more whitespace characters.
- **`\K`**: The **"Keep-out"** operator. It tells the engine to discard everything matched to its left from the final output.
- **`\S+`**: Matches one or more non-whitespace characters (the actual password).
##### Lessons Learned
- Using **anchors** and **look-behind equivalents** (`\K`) to clean terminal output.
- The power of **PCRE** over basic Regex for complex data extraction.
- Filtering noise directly from the command line to feed scripts or clipboards.
#### Pass 8
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc