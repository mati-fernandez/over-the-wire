#### Concept
Obfuscation through Hashing (Algorithm Recognition): Using hashing functions to generate dynamic file paths based on environment variables (`whoami`).
#### Key Commands
- **`md5sum`:** Generates an MD5 hash of the input.
- **`cut`:** Filters text columns based on delimiters.
#### Walkthrough
I analyzed the `/usr/bin/cronjob_bandit23.sh` script and discovered that the password for `bandit23` was being copied to a file in `/tmp/` whose name was the result of an MD5 hash of the phrase **"I am user bandit23"**. I manually replicated the hash generation command in the terminal to obtain the filename and read it using `cat`.
#### Key Takeaways
I learned that security through obscurity (hiding something under a strange name) is useless if the attacker knows the algorithm generating that name. I also practiced using pipes to chain Bash logic.
#### Command Breakdown
- **`echo I am user bandit23`**: Simply prints the string. **Note:** This is the "seed" of the hash; any mistake in spaces or casing changes the result completely.
- **`| md5sum`**: MD5 (Message Digest Algorithm 5) generates a 128-bit "digital fingerprint" (32 hex characters). While no longer secure for real passwords due to collisions, it's a classic for obfuscating filenames in Bandit.
- **`| cut -d ' ' -f 1`**: `-d ' '` sets the delimiter to a space. `-f 1` selects the first field, cleaning the hash and leaving only the 32 characters.
#### Pass 23
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
