#### Concept
**Execution After Redirect (EAR).**
An Execution After Redirect vulnerability occurs when a web application attempts to restrict access or redirect a user by injecting an HTTP redirection header (such as `302 Found` or `301 Moved Permanently`) but fails to terminate the script execution immediately afterward. Since HTTP headers only instruct the client (browser) to navigate away, the server-side engine continues executing subsequent code lines and transmitting data down the socket pipeline unless explicitly halted via a termination construct like `exit()` or `die()`.
#### Key Commands
- **Missing Termination Sentinel**: The primary flaw resides within the initial authorization gate block:
    ```php
    if(!($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1)) {
        header("Location: /");
        // Critical Defect: Missing exit; or die(); here
    }
    ```
- **Unconditional Downstream Evaluation**: Because execution does not halt at the header allocation, the engine proceeds to process the secondary condition block regardless of authentication status, embedding the administrative dataset directly inside the HTTP response body:
    ```php
    if(array_key_exists("revelio", $_GET)) {
        print "You are an admin. The credentials for the next level are:<br>";
        // Exfiltration payload prints here
    }
    ```
#### Walkthrough / Resolution
- **Source Code Inspection**: Reviewing `index-source.html` revealed that passing the query parameter `?revelio=1` invokes a conditional branch that prints credentials but triggers an upstream redirection check if the session lack admin variables.
- **Identify Client-Side Shielding**: Standard browsers implicitly follow the `Location: /` response header, clearing the execution log and blinding the human tester to the initial payload transfer.
- **Exploitation via Raw HTTP Client**: Utilizing a specialized network terminal utility (`curl`) allows explicit capture of the immediate state transaction. Since raw command-line tools do not parse or follow location headers natively unless forced (via `-L`), the connection stops after receiving the primary response packet.
- **Execution Command**:
    ```bash
    curl -u natas22:d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz "http://natas22.natas.labs.overthewire.org/index.php?revelio=1"
    ```
- **Data Harvesting**: Analyzing the standard output dump exposes the raw generated HTML trailing after the redirect statement, revealing the plaintext credentials.
#### Key Takeaways / Lessons Learned
- **Always Terminate After Redirections**: Every application flow routing statement (`header("Location: ...")` in PHP, `res.redirect()` in Node architectures before code blocks) must be immediately coupled with an explicit program exit statement to decouple downstream logic from the network state.
- **Inspect Raw Server Output**: Never rely exclusively on standard browser rendering engines during security assessments; applications can leak critical state variables within invisible response bodies.
#### Pass 23
dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
