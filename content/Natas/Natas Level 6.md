#### Summary
Sensitive application data was exposed through an accessible server-side include file.
#### Target
The exposed `secret.inc` file referenced in the application source code.
#### Exploit
1. Authenticate using the provided credentials.
2. View the application source code.
3. Identify the included file: `includes/secret.inc`.
4. Access the file directly through the browser.
5. Retrieve the secret value and submit it through the form.
6. Obtain the password for the next level.
#### Payloads / Commands
Browser:
* `Ctrl + U` (View Source)
* `/index-source.html`
* `/includes/secret.inc`
#### Why it works
The application stores a sensitive value in a PHP include file located inside the web root. Since the file is publicly accessible, its contents can be retrieved directly, exposing the secret required by the application.
#### Takeaways
* Never expose sensitive files inside publicly accessible directories.
* Server-side include files should not be directly accessible over HTTP.
* Reviewing application source code often reveals additional attack vectors.
#### Pass 7
B1szg95UcTnrzwnF3i3TzYHlyYh8iBV0
