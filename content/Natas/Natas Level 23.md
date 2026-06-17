#### Concept
**PHP Type Juggling / Loose Comparison Bypass.**
PHP is a loosely typed language that automatically coerces variables into compatible types when executing comparisons. When a string is evaluated in a numeric context (such as using the greater-than `>` operator), PHP attempts to extract a numeric value from the string. If the string begins with numeric digits, it extracts those digits and discards the trailing characters; if it begins with alphabetical characters, it evaluates to `0`.
#### Key Commands
- **`strstr($haystack, $needle)`**: Extracts the portion of the string from the first occurrence of the needle to the end. The defect lies in checking if the keyword exists without restricting its exact position. i.e., it looks for the string anywhere in the first string parameter.
- **Loose Numerical Comparison (`> 10`)**: The logical vulnerability is caused by comparing the raw input string against an integer using a weak boundary check:
    ```php
    if(strstr($_REQUEST["passwd"],"iloveyou") && ($_REQUEST["passwd"] > 10 ))
    ```
    Since the input is not sanitized or strictly cast to an integer before the check, an attacker can craft an input that satisfies both a string match and a numerical equation simultaneously.
#### Walkthrough / Resolution
- **Analyze Constraints**: The payload must contain the substring `"iloveyou"` and its type-coerced integer representation must be strictly greater than `10`.
- **Craft Payload**: Placing a valid integer ahead of the required substring (e.g., `11iloveyou`) tricks the interpreter engine during sequential validation:
    - `strstr("11iloveyou", "iloveyou")` evaluates to `true` because the substring exists.
    - `"11iloveyou" > 10` forces a numeric type coercion. PHP reads the leading digits (`11`), discards `"iloveyou"`, and runs `11 > 10`, which evaluates to `true`.
- **Execution**: Passing `?passwd=11iloveyou` via the HTTP request successfully triggers the administrative execution block.
#### Key Takeaways / Lessons Learned
- **Enforce Strict Comparisons**: Avoid loose data binding checks. Utilize strict type checking (e.g., `===` or explicit casting like `(int)$_REQUEST["passwd"]`) to guarantee the underlying data match the expected operational type.
- **Input Sanitization**: Validate that data structural models match expectations (e.g., ensuring a password field does not accept mixed structural types for logical parameters).
#### Pass 24
MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
