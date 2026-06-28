#### Summary
Access control was based on the HTTP `Referer` header, which can be easily spoofed by the client.
#### Target
The HTTP `Referer` request header.
#### Exploit
- Authenticate using the provided credentials.
- Observe that access is denied because the expected `Referer` is missing.
- Send a new request with the `Referer` header set to `http://natas5.natas.labs.overthewire.org/`.
- Retrieve the password for the next level.
#### Payloads / Commands
```bash
curl -u natas4:JDrPnuZAKyl6MkiqQGFIddrqpvgOASth \ -H "Referer: http://natas5.natas.labs.overthewire.org/" \ http://natas4.natas.labs.overthewire.org/
```
#### Why it works
The application trusts the value of the HTTP `Referer` header to authorize access. Since HTTP headers are controlled by the client, an attacker can forge the expected value and bypass the restriction.
#### Takeaways
- Never use the `Referer` header for authentication or authorization.
- Any client-controlled HTTP header can be manipulated.
- Authorization decisions must rely on server-side validation.
#### Pass 5
e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M
