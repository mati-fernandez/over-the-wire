**Port Analysis (Reconnaissance)** After scanning the 31000-32000 range, 5 open ports were identified. Manual enumeration revealed:
- **31046:** Discarded. Does not use SSL (Handshake error).
- **31518:** Echo Server. Uses SSL but merely returns the same string sent. 
- **31691:** Discarded. Similar behavior to 31046.
- **31790:** **WINNER!** SSL port that, upon receiving the L15 password, returns the L17 credential.
- **31960:** Discarded. Does not respond to credentials.
#### Concept
Scanning and Enumerating SSL Services. This level combines port discovery (`nmap`) with manual interaction in encrypted services to extract non-trivial credentials (RSA keys).
#### Key Commands
- `nmap -p 31000-32000 localhost`: Basic port scan.
- `nmap -p 31000-32000 -sV localhost`: Scan with version and service detection (failed/timed out).
- `openssl s_client -connect localhost:31790 -ign_eof`: Manual connection keeping the tunnel open.
#### Walkthrough
- Ran `nmap` to locate open ports.
- Used `openssl s_client` with the `-ign_eof` flag on port 31790.
- Sent the Level 15 password.
- The server responded with an **RSA Private Key**.
- Saved the key as `bandit17.key` and adjusted Windows permissions (**Security > Advanced > Disable inheritance**) to ensure the file was private (Read-only for my user).
#### Key Takeaways
I learned that `nmap` is only the first step; manual enumeration is what confirms which service is actually useful. I also understood that servers can return different types of credentials, such as RSA keys, which require more careful file handling than simple plaintext passwords.
#### Pass 17
There is no password for this level. Access the `bandit17` server using the RSA key obtained:
`ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220`
[RSA Key](Informática/Ciberseguridad/OverTheWire/content/Bandit/bandit17.key)

