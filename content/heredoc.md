# What is a Heredoc (Here Document)?
A **Here Document (heredoc)** is a Bash syntax for sending multiple lines of text to a command through standard input.
It is commonly used to generate files, feed interactive programs, or embed scripts.

---
# Basic syntax
```bash
command << EOF
text
more text
EOF
```
Everything between the two `EOF` markers is passed to `command`.
`EOF` is just a delimiter and can be replaced with any identifier.
Example:
```bash
cat << END
Hello
World
END
```
Output:
```text
Hello
World
```

---
# Creating a file
```bash
cat > hello.txt << EOF
Hello
World
EOF
```
Produces:
```text
Hello
World
```
inside `hello.txt`.

---
# Preventing variable expansion
Without quotes:
```bash
cat << EOF
Home: $HOME
EOF
```
Output:
```text
Home: /home/user
```
Because Bash expands variables before sending the text.
With quotes:
```bash
cat << 'EOF'
Home: $HOME
EOF
```
Output:
```text
Home: $HOME
```
The contents are treated literally.

---
# Why use heredocs?
They avoid escaping quotes and special characters when generating files.
Instead of:
```bash
echo '<?php
echo file_get_contents("/etc/passwd");
?>' > exploit.php
```
You can write:
```bash
cat > exploit.php << 'EOF'
<?php
echo file_get_contents("/etc/passwd");
?>
EOF
```
This is easier to read and less error-prone.

---
# Related
- [[Bash]]
- [[Standard Input (stdin)]]
- [[Variable Expansion]]