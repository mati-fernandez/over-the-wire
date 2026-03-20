## Analizing [[Informática/Ciberseguridad/OverTheWire/content/Bandit-tmp/Level 23]] script from Over The Wire
`bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh`
```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
### 1. The Loop `for` (The Sweeper)
```bash
for i in * .*;
```
- **`i`**: This is a temporary variable. It could be called `file`.
- **`*`**: A wildcard that means "all visible files".
- **`.*`**: Means "all hidden files" (those that begin with a period).
- **Translation**: "For everything you find in this folder...".
##### The space between `*` and `.*`
These are **two separate arguments**.
- In Bash, the space is the **universal delimiter**.
- `*` tells the loop: "Search for everything visible."
- `.*` tells it: "Search for everything hidden (that starts with a period)."
- If you put them together (`*.*`), it would only search for files that have a period in the middle (like `foto.jpg`), ignoring folders or files without an extension.
### 2. The security filter
```bash
if [ "$i" != "." -a "$i" != ".." ];
```
- **`!=`**: Means "Not equal to".
- **`-a`**: Is a logical **AND**.
Why it exists: In Linux, each folder has two invisible folders: `.` (itself) and `..` (the one above it). If the script tried to "delete" or "execute" `..`, it would break the entire system. This `if` statement says: "If it's neither the parent nor the current folder, proceed."
### 3. The Property Inspector
```bash
owner="$(stat --format "%U" ./$i)"
```
- **`$()`**: Executes a command and saves the result to a variable.
- **`stat --format "%U"`**: It's like a scanner that only looks at the owner's name.
- **Purpose**: The Bandit administrator is sneaky. He doesn't want a script from `bandit1` to steal the password from `bandit24`. He only allows **YOU** (`bandit23`) to run scripts there.
### 4. The Bodyguard (Timeout)
```bash
timeout -s 9 60 ./$i
```
- **`timeout`**: Prevents a script from running indefinitely (an "infinite loop") and crashing the server.
- **`-s 9`**: Sends the **SIGKILL** signal (single kill, no questions asked).
- **`60`**: Maximum number of seconds to live.
#### Why the 9 in `timeout -s 9`?
In Linux, processes communicate using **Signals**. Each number represents a different command:
- 15 (SIGTERM): This is a polite "Please close when you can."
- 9 (SIGKILL): This is a "Die right now!" The operating system kills the process instantly, preventing it from saving anything or complaining. It's the most aggressive way to stop a misbehaving script.