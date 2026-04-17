#### Concept
**Client-side Restrictions Bypass.** Blocking right-click via JavaScript is a "security through obscurity" tactic. It doesn't actually protect the source code, as the browser must still download it to render the page.
#### Key Commands
- `Ctrl + U`: View source directly.
- `F12`: Open Developer Tools.
- `curl -u natas1:[password] [url]`: Bypass all browser-level restrictions.
#### Walkthrough / Resolution
- Accessed `natas1`.
- Confirmed that right-click was disabled by a script.
- Used the keyboard shortcut `Ctrl + U` to bypass the restriction and view the source.
- Located the password for the next level in a comment.
#### Key Takeaways / Lessons Learned
- Never rely on client-side scripts (JS) for security.
- If the browser can see it, the user can see it.
#### Pass 2
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
