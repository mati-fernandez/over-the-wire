#### Concept
**Session Poisoning via Newline Injection (Session Deserialization Exploitation).**
This vulnerability occurs when an application manages session states by reading and writing to custom flat-text files on the local disk instead of utilizing structured, secure database storage or native engine serialization. If the backend fails to sanitize control characters—specifically carriage returns or newlines (`\n`)—from user inputs before appending them into a sequential key-value file configuration, an attacker can inject structural boundaries to forge entirely new session variables and manipulate internal privilege states.
#### Key Commands
- **`mywrite()`**: The root defect. Loops through the `$_SESSION` global array and concatenates keys and values into a single string utilizing a raw newline delimiter (`$data .= "$key $value\n"`), without stripping existing `\n` characters from the user-controlled input.
- **`myread()`**: Parses the session file strictly using `explode("\n", $data)`. This allows any injected newline to split a single input array entry into multiple standalone logical configuration lines.
- **Two-Step Execution Blueprint**: Unlike immediate exploits, this injection requires an authentication persistence loop: one request to commit the poison to disk, and a secondary follow-up request to parse the newly structured privileges.
#### Walkthrough / Resolution
- **Analyze Custom Session Lifecycles**: Reviewing the source code confirmed that the application bypasses native PHP serialization by registering a custom set of handler callbacks through `session_set_save_handler()`.
- **Deconstruct the Storage Protocol**: The state synchronization operates under a primitive pattern: `key value\n`. If a standard user submits the name `mati`, the server generates a disk file containing:
    ```
    name mati
    ```
- **Formulate the Multi-Line Payload**: By structuring a payload string with an embedded escape sequence line break (`mati\nadmin 1`), we weaponize the formatting logic.
- **Execute the Dual-Stage Attack Loop**:
    - **Stage 1 (POST)**: A Node.js script ([[exploit20.js]]) initiates a `POST` request carrying a fixed tracking `PHPSESSID` cookie and the encoded multi-line payload. The server runs `mywrite()`, saving the file structure directly as:
        ```
        name mati
        admin 1
        ```
    - **Stage 2 (GET)**: The script immediately follows up with a clean `GET` request using the identical session identifier. The backend invokes `myread()`. When `explode("\n", $data)` parses line two, it isolates the string `"admin 1"`, splitting it into `$_SESSION['admin'] = 1`, overriding the execution memory context.
- **Flag Exfiltration**: With administrative privileges successfully spoofed on the second pass, `print_credentials()` yields execution truth and dumps the target data.
#### Key Takeaways / Lessons Learned
- **Input Isolation**: Never allow structural protocol markers (such as `\n`, `\r`, or delimiters like spaces/tabs in flat-file systems) to be processed raw inside storage serialization routines.
- **Do Not Invent Session Storage**: Session states should exclusively be handled via cryptographically managed data structures or production-grade state frameworks that encapsulate memory properties away from the standard filesystem storage layers.
#### Pass 21
BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
