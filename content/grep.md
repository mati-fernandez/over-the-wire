# What is grep?
`grep` is a command-line tool used to **search text using patterns (regular expressions)**.
It reads input line by line and prints only the lines that match a given pattern.
The name comes from `g/re/p` (global / regular expression / print).

---
# Basic syntax
```bash
grep [options] pattern file
```
Example:
```bash
grep "error" logfile.txt
```

---
# Core behavior
- Searches **line by line**
- Matches **patterns (regex by default)**
- Outputs **only matching lines**
- Can read from files or pipes
Example with pipe:
```bash
cat file.txt | grep "hello"
```

---
# Common options
## Ignore case or case (i)nsensitive
```bash
grep -i "hello" file.txt
```

---
## Recursive search
```bash
grep -r "password" .
```

---
## Show line numbers
```bash
grep -n "error" file.txt
```

---
## Invert match (exclude matches)
```bash
grep -v "debug" file.txt
```

---
## Match whole words only
```bash
grep -w "cat" file.txt
```

---
## Count matches
```bash
grep -c "error" file.txt
```

---
## Extended regex
```bash
grep -E "error|fail|critical" file.txt
```
Equivalent to `egrep` (deprecated naming).

---
# Security relevance
`grep` becomes dangerous in web apps when:
- user input is passed directly into shell commands
- input is not escaped or validated
Example vulnerable pattern:
```php
passthru("grep -i $input file.txt");
```
This can lead to **command injection**.

---
# Pentesting usage
- Search for secrets in files:
    ```bash
    grep -r "password" /etc
    ```
- Filter logs:
    ```bash
    grep "GET /admin" access.log
    ```
- Combine with other tools:
    ```bash
    cat file | grep "token" | sort | uniq
    ```

---
# Mental model
Think of `grep` as:
> “a filter that keeps only matching lines”
Not a file scanner, not a parser — just a **line filter engine**.