#### Concept
Transport Encryption (SSL/TLS). Using secure tunnels for transmitting sensitive data.
#### Key Commands
- **`openssl s_client`:** A generic client to connect to services using SSL/TLS.
- **`-connect`:** Flag used to specify the host and port.
- **`-ign_eof`:** Prevents the connection from closing prematurely after sending data (not used in this instance).
#### Walkthrough
```bash
openssl s_client -connect localhost:30001
```
I established an encrypted connection to `localhost` on port 30001 using the OpenSSL client. Once the handshake was completed, I sent the current password, and the service responded with the credential for the next level.
#### Key Takeaways
I learned that some ports do not accept plaintext connections for security reasons. I understood that SSL/TLS is not exclusively for websites (HTTPS); it can wrap any port communication to protect data from potential "sniffers" on the network.
#### Difference from the previous level
While `nc` only opens a basic data pipe, `s_client` first performs a **handshake**: it exchanges certificates, negotiates the encryption algorithm, and establishes a secure tunnel. Only after this tunnel is unbreakable does it allow you to type.
#### Pass 16
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx