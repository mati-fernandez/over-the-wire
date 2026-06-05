#### Concept
**Boolean-Based Blind SQL Injection (Authentication Inference).**
This vulnerability occurs when an application is susceptible to SQL Injection but does not output any database records or error messages directly to the screen. Instead, the application changes its behavior based on the logical evaluation (TRUE or FALSE) of the injected query, allowing an attacker to reconstruct database contents character-by-character via binary interrogation.
#### Key Commands
- **`LIKE BINARY`**: A SQL operator used for case-sensitive pattern matching.
- **`%`**: A SQL wildcard character representing zero or more arbitrary characters.
- **`encodeURIComponent()`**: Encoders special input characters into a valid URL/URI safe format for transportation inside an HTTP POST request body.
#### Walkthrough / Resolution
- **Analyze the Restriction**: Inspecting the source code revealed a dynamic query injecting the username directly:
    ```php
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    ```
    The backend only reports if rows were found (`This user exists.`) or not (`This user doesn't exist.`), discarding actual row values from the HTTP response.
- **Formulate the Interrogation Logic**: To bypass manual extraction of a 32-character password, a custom Node.js automation script ([[exploit.js]]) was crafted.
- **Inject the Boolean Payload**: The script systematically appended characters from a standard alphanumeric alphabet (`charset`) and checked the server's boolean response using the following pattern:
    ```sql
    natas16" AND password LIKE BINARY "accumulated_chars + testing_char%
    ```
    - _Analysis of the script:_ The payload breaks the original structure with `"`. The `AND` operator links the evaluation to the password validation. If the guess matches the sequential prefix of the password, the database returns a row, triggering the string `This user exists.` inside the response body.
- **Execution**: The script ran linearly ($O(n)$ complexity), capturing true conditions and instantly jumping to the next character index until the complete 32-character token was isolated.
#### Key Takeaways / Lessons Learned
- **The Error of Implicit Data Exposure**: Silence or generic server responses do not prevent data exfiltration if the application structure allows user-controlled logical evaluation steps.
- **Defense-in-Depth Defeats Blind SQLi**: Implementing standard _Prepared Statements_ isolates variables from commands, preventing interpretation entirely. Furthermore, setting up strict **Rate Limiters** breaks automation efficiency by introducing structural bottlenecks to high-volume polling scripts.
#### Pass 16
hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
