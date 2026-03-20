#### Concept
**Client-Server Model (Localhost):** Interaction between two independent processes communicating via local network ports. Sockets: Using communication endpoints (IP:Port) to securely transfer data between privilege levels.
#### Key Commands
- **`nc -l -p [port] < [file]`:** Creates a listener (server) that serves the file content to whoever connects.
- **`./suconnect [port]`:** A SETUID client that validates the current level's password to provide the next one.
- **Job Control (Single terminal):**
       - `&`: Run in the background.
       - `jobs`: List background tasks.
       - `fg`: Bring task to the foreground.
       - `CTRL+Z`: Pause current process.
#### Walkthrough
For this challenge, I used a dual-session SSH approach to separate system responsibilities:
1. **Server Terminal:** Created a temporary file with the L20 password and set `nc` to listen on port 12345: `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" > /tmp/p20` `nc -l -p 12345 < /tmp/p20`
2. **Client Terminal:** In a parallel session, I ran the binary: `./suconnect 12345` The binary successfully connected to the `nc` server, received the password, validated it internally (thanks to its SETUID permissions), and returned the [[Level 21]] credential.
>You could also use [[Job Control]] to manage the server in the background and use a single terminal.
#### Key Takeaways
I learned that Inter-Process Communication (IPC) via network is extremely useful when a program needs external data for security validation. I also understood the operational difference between a process that "listens" (server) and one that "connects" (client). Using **Job Control** allows managing multiple tasks in a single interactive shell, turning a process into a background daemon using the `&` symbol.

**Single-Terminal Version:**
**IPC (Inter-Process Communication):** I learned that Linux's "Job Control" allows you to manage background processes using the `&` symbol. This allows one process to act as a server (daemon) while another acts as a client in the same session.
**[[Job Control]] and Background Processes**: Managing multiple tasks in a single interactive shell.
#### Pass 21
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
