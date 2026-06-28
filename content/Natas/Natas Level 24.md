#### Concept
**Function Failure Bypass via Type Incompatibility (strcmp API Defect).**
In PHP versions prior to 8.0, internal string functions such as `strcmp()` fail to securely handle non-string data types. When a complex structure like an Array is passed into a parameter expecting a primitive string, the underlying C-based routine outputs a runtime warning and returns `NULL`. Due to PHP's loose type coercion rules, `NULL` behaves as a falsy value, creating severe logical bypasses when handled via weak negation operators.
#### Key Commands
- **`strcmp($str1, $str2)`**: Compares two strings character by character, returning `0` if they are identical.
- **Weak Negation Gate (`!strcmp`)**: The structural defect lies in implicitly trusting that `strcmp()` will only ever return an integer:
    ```php
    if(!strcmp($_REQUEST["passwd"],"<censored>"))
    ```
    If an attacker forces `strcmp()` to return `NULL`, the expression evaluates as `!NULL`, which translates directly to `true`, bypassing authentication.
#### Walkthrough / Resolution
- **Identify Target Function**: The application validates the parameter `passwd` using `strcmp()`.
- **Type Disruption Payload**: Instead of trying to guess the plaintext password, the request structure is altered to supply an empty array using the square-bracket HTTP parameter syntax.
- **Execution**:
    ```http
    http://natas24.natas.labs.overthewire.org/index.php?passwd[]=
    ```
- **Bypass Logic Flow**:
    - `$_REQUEST["passwd"]` becomes `[]`.
    - `strcmp([], "<secret>")` emits a warning and evaluates to `NULL`.
    - The condition becomes `!NULL` $\rightarrow$ `!false` $\rightarrow$ `true`.
    - Bypasses the constraint and renders the administrative flag.
#### Key Takeaways / Lessons Learned
- **Enforce Strict Type Checking**: Always validate that user input matches the expected data type (e.g., using `is_string()`) before passing it into type-sensitive core functions.
- **Avoid Weak Negations on Non-Boolean Functions**: Do not use the `!` operator on functions that return integer metrics or error codes; use explicit integer evaluation instead (`strcmp($a, $b) === 0`).
#### Pass 25
ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
