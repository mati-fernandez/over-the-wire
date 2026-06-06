#### Concept
**Boolean-Based Blind Command Injection (Inverted Logic).**
This vulnerability occurs when user input is passed directly into a system shell command execution function (like PHP's `passthru()`). Even when robust character filtering prevents traditional command chaining (`|`, `&`, `;`), sub-shell command substitution (`$()`) can still be exploited. Since the output of the injected command is not directly printed to the screen, data must be exfiltrated character-by-character by observing how the primary command's behavior changes based on the internal command's outcome.
#### Key Commands
- **`$()`**: Bash command substitution syntax. It executes an inner command and replaces itself with the command's standard output before running the outer command.
- **`grep ^`**: The caret (`^`) anchor in regular expressions specifies that the match must occur at the beginning of a line.
#### Walkthrough / Resolution
- **Analyze the Sanitization**: The source code implemented a strict character filter using a regular expression:
    ```php
    if(preg_match('/[;|&`\'"]/',$key))
    ```
    While it successfully blocked command chaining and backticks, it completely omitted the dollar sign (`$`) and parentheses `()`, leaving the `$()` substitution syntax active.
- **Identify the Logic Loophole**: The server executes the following command:
    ```bash
    grep -i "$key" dictionary.txt
    ```
    If a word from `dictionary.txt` (e.g., `African`) is appended to a sub-shell command, the output behaves inversely:
    - **If the guess is FALSE**: The inner `grep` returns nothing. The outer command evaluates `grep -i "African" dictionary.txt`, finds the word, and prints it.
    - **If the guess is TRUE**: The inner `grep` returns text from the password file. The outer command evaluates `grep -i "extracted_textAfrican" dictionary.txt`, fails to find this non-existent word, and leaves the screen completely blank.
- **Automation**: A custom Node.js script ([[exploit16.js]]) was implemented to scan each position of the password against an alphanumeric charset, advancing only when the keyword `African` disappeared from the HTML response body.
#### Key Takeaways / Lessons Learned
- **Flawed Blacklisting**: Relying on a list of banned characters (blacklisting) instead of validating expected input shapes (whitelisting) almost always leaves syntax edge-cases open.
- **Avoid System Shell Execution**: Dynamic user input should never be passed directly to underlying operating system utilities. Safer alternatives include using native programming language functions or tightly scoped APIs.
#### Pass 17
EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
