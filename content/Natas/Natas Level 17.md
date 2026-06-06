#### Concept
**Dynamic Time-Based Blind SQL Injection (Side-Channel Attack).**
This vulnerability occurs when an application executes a database query containing user-controlled input but suppresses all visual feedback. Regardless of whether the query returns records, empty sets, or internal database errors, the HTTP response body remains visually identical. To exfiltrate data, the attacker must switch from the visual channel to a structural **side-channel**: measuring the precise **server execution time**. By forcing the database engine to execute a time-delay function (like MySQL's `SLEEP()`) when a logical condition is met, data can be inferred binary-style based on network response latency.
#### Key Commands & Functions
- **`IF(condition, true_action, false_action)`**: A native MySQL control flow function.
- **`SLEEP(seconds)`**: A MySQL utility function that pauses query processing for a specified duration (accepts floating-point decimals for sub-second precision).
- **`performance.now()`**: A high-resolution Node.js API used to measure timestamps in milliseconds, crucial for baseline network calibration.
#### Walkthrough / Resolution
- **Analyze the Absolute Silence**: Inspecting the application structure confirmed that the backend completely stripped row evaluations:
    ```php
    $res = mysqli_query($link, $query);
    if($res) {
        echo "We dont log errors anymore, nor do we show text blocks.<br>";
    } else {
            passthru("grep -i \"$key\" dictionary.txt");
    }
    ```
    Since the HTML response was completely static, boolean-based text detection (like in Natas 15) was rendered useless.
- **Implement Network Baseline Calibration**: To avoid rigid, time-consuming fixed delays (e.g., 5 seconds per request), a dynamic script ([[exploit17.js]]) was engineered. The script starts by making a vanilla network request to isolate the current round-trip time (RTT/Ping), establishing a baseline network latency.
- **Build an Adaptive Threshold**: The script added a safety buffer of `300ms` over the baseline to set a dynamic truth-threshold. The `SLEEP()` parameter inside the payload was mapped mathematically to match this threshold:
    ```php
    sleepSeconds = (baseline + 300) / 1000
    ```
- **Data Exfiltration**: The final injection string broke the syntax, embedded the conditional time-lock, and commented out the rest of the query:
    ```sql
    natas18" AND IF(password LIKE BINARY "accumulated_chars + testing_char%", SLEEP(dynamic_seconds), 0) #
    ```
    If a character guess was true, MySQL entered the sleep state, dragging the execution time past the dynamic threshold. If false, it returned instantly, minimizing the time footprint.
#### Key Takeaways / Lessons Learned
- **Side-Channels cannot be ignored**: Obfuscating errors and outputs does not mean data is unreadable. As long as system resource computation varies depending on input veracity, the data can be measured.
- **Mitigation**: Use Parameterized Queries (Prepared Statements) so input structures can never change command interpretation logic. To mitigate time-based attacks explicitly, decouple execution time from user actions using asynchronous processing queues or uniform query execution time normalization.
#### Pass 18
6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
