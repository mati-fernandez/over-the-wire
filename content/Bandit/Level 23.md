#### Concept
**Insecure Cronjob Execution:** Privilege escalation by exploiting automatic script execution in directories with write permissions for lower-level users.
#### Comandos clave
[[Informática/Ciberseguridad/OverTheWire/content/Bandit/Bash Scripting#Analizando script del Level 23 de Over The Wire|Breakdown of the script found]]
- **`mkdir /tmp/name`**: Creates a temporary directory.
- **`nano script.sh`**: Simple text editor to write the attack code.
- **`chmod 777`**: Grants full permissions (read, write, execute) so the `bandit24` process doesn't fail when accessing or writing.
- **`cp`**: Copies the script to the "hot" folder watched by the cronjob.
#### Walkthrough
The goal was to "trick" an automated process running with `bandit24` privileges.
1. **Reconnaissance**: I analyzed `/usr/bin/cronjob_bandit24.sh` and discovered it executes any file I own inside `/var/spool/bandit24/foo` and then deletes it.
2. **Setup**: Created `/tmp/my_attack_23` and gave it `777` permissions so `bandit24` could write the result there later.
3. **The Thief Script**: Used `nano` to create `getpass.sh`:
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/my_attack_23/pass.txt
```
4. **Execution Permissions**: Ran `chmod 777 getpass.sh`. Without this, the cronjob would see the file but couldn't "run" it.
5. **Injection**: `cp getpass.sh /var/spool/bandit24/foo/`
6. **Exfiltration**: Waited a minute. Once the script disappeared from the `foo` folder, I read the generated file: `cat /tmp/my_attack_23/pass.txt`.
#### Key Takeaways
I learned that if a process with more power than me executes my scripts, I can order it to hand over files I normally can't access. The key was ensuring both my folder and script had `777` permissions. "Who executes the code" is more important than "who wrote it."
#### Pass 24
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
