#### Concept
Substitution cipher (ROT13).
#### Key Commands
`tr` (Translate).
#### Walkthrough
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
To solve this level, I used the `tr` (translate) command to apply a ROT13 decryption. Since `tr` doesn't understand mathematical rotations, I provided two character sets to perform a direct mapping:
- **Search set (`'A-Za-z'`):** Represents the complete standard alphabet.
- **Replacement set (`'N-ZA-Mn-za-m'`):** Defines the new order. By writing `N-ZA-M`, I instruct the tool that the range must "wrap around": it starts at N, goes up to Z, and continues immediately from A to M.
This way, each letter in the `data.txt` file was substituted by its corresponding counterpart 13 positions ahead, revealing the plaintext password.
#### Key Takeaways
How to map character ranges to shift the alphabet. I understood that ROT13 is reversible using the exact same command.
#### Pass 12
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

