#### Concept
Extracting human-readable data from **binary files** (non-plain text). The goal is to filter out "noise" or machine code to find printable character strings, using visual patterns (like `=`) as a guide.
#### Key Commands
- `strings`: Scans a file and returns only sequences of printable characters.
- [[grep]]: Searches for specific patterns within the command output.
- `|` (Pipe): Connects the output of one command to the input of the next.
#### Walkthrough
`strings data.txt | grep "=="` 
_Observation: The password is preceded by several equal signs, making it easier to locate within the filtered strings._
#### Key Takeaways
I learned that binary files are not entirely "unreadable"; they contain metadata and strings that can reveal sensitive information. I also mastered using `strings` to clear visual clutter before applying search filters.
#### Pro-Level Optimization
To capture **all** equal signs regardless of their count and clean the output, we can use **Regular Expressions (Regex)**.
1. Matching all equal signs
	We use the `+` quantifier, which means "one or more of the preceding character." Since `+` is a special character, we use `grep -E` (Extended Regex):

```bash
strings data.txt | grep -E "=+"
```
This tells the shell: "Find any sequence where the `=` symbol appears one or more times consecutively."
2. "Ninja Mode": Cleaning the output
	If you want the terminal to return **only** the password and strip the equal signs automatically, use `grep -o` (only-matching) with a more advanced expression:

```bash
strings data.txt | grep -oE "[a-zA-Z0-9]{10,}"
```

- **`[a-zA-Z0-9]`**: Searches only for alphanumeric characters (ignoring the `=`).
- **`{10,}`**: Filters for strings that are at least **10 characters** long. Since the password is a long alphanumeric string and the equal signs are symbols, this command "cleans" the noise and spits out the raw key.
#### Pass 10
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey