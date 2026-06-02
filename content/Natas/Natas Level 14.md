#### Concept
**SQL Injection (SQLi) Authentication Bypass.**
This vulnerability occurs when user input is concatenated directly into a database query string instead of using parameterized queries. An attacker can inject SQL syntax to manipulate the query's logic, alter the execution flow, and bypass authentication mechanisms without knowing valid credentials.
#### Key Commands
- **`" or 1=1`**: A logical injection payload designed to force the `WHERE` clause to always evaluate to true.
- **`#` or `--`** : SQL comment characters used to truncate the rest of the original query, ignoring any subsequent conditions like password checks.
#### Walkthrough / Resolution
- **Analyze the Query**: The source code revealed a vulnerable dynamic SQL statement:
    ```php
	"SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\""
    ```
- **Identify the Logic**: The application grants access if the query returns more than 0 rows (`mysqli_num_rows > 0`). It doesn't validate the password separately in the PHP code.
- **Craft the Payload**: Injected the following string into the `username` field while leaving the password empty:
	==`admin" or 1=1 #`==
    - _Analysis of the injection:_ The double quote (`"`) closes the username string structure prematurely. The `or 1=1` injects a universally true condition. The `#` symbol comments out the remaining `and password="..."` portion of the developer's code.
- **Execution**: The database processed the modified query, evaluated the statement as true, returned the user records, and the server granted access to the flag.
#### Key Takeaways / Lessons Learned
- **Data vs. Code Separation**: Never construct SQL queries by concatenating raw strings. Malicious input will be interpreted as executable database commands.
- **Use Parameterized Queries / Prepared Statements**: In modern languages (like Java with Spring Data JPA/Hibernate or Node.js with SQL drivers), always use placeholders (`?` or named parameters). This ensures the database engine treats input strictly as literal data, making SQL injection impossible.
#### Pass 15
SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
