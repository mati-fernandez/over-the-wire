#### Acceso
For this level, a plaintext password is not used; instead, an RSA private key obtained from the previous level is required.
**Connection Command:**
```bash
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```
#### Concept
File Diffing. Identifying changes between versions of the same dataset. This is fundamental for forensic analysis or configuration auditing.
#### Key Commands
- **`diff [file1] [file2]`:** Compares files line by line.
- **`cat`:** To verify the content before comparing.
- **`sort`:** Useful if the files are not in the same order (though they usually are in this level).
#### Walkthrough
Upon entering the server with the RSA key, I found two files: `passwords.old` and `passwords.new`. I used `diff` to identify which line had changed. The command pointed out that line 42 had been modified. The string marked with `>` is the new password.
#### Key Takeaways
I learned to read the `diff` syntax: the `<` symbol represents the source file and `>` represents the destination file. This tool is vital to avoid searching manually through thousands of lines of similar text.
#### Pass 
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
