#### Summary
The application allows users to upload files and determines the destination file extension from a **user-controlled hidden form field** (`filename`). Because the server does not validate the extension or the file contents, an attacker can upload a PHP script and execute arbitrary code.
#### Target
- `$_FILES['uploadedfile']`
- `$_POST['filename']`
- `makeRandomPathFromFilename()`
- `move_uploaded_file()`
#### Exploit
- Intercept the upload request.
- Change the hidden `filename` parameter from `*.jpg` to `*.php`.
- Upload a PHP payload.
- Open the uploaded file from the generated `/upload/` path.
- Execute PHP code to read `/etc/natas_webpass/natas13`.
#### Payloads / Commands
```php
<?php
echo file_get_contents("/etc/natas_webpass/natas13");
?>
```
#### Why it works
The application trusts a client-controlled parameter (`filename`) to determine the file extension. Since the upload directory is web-accessible and PHP files are executed by the server, uploading a PHP script results in **Remote Code Execution ([[RCE]])**.
#### Real-world Notes
- File upload vulnerabilities remain one of the most common web application flaws.
- Real applications often validate extensions, MIME types, or magic bytes, but misconfigurations and incomplete validation are still frequently exploitable.
- During a penetration test, file upload functionality is always considered a high-value attack surface. Typical tests include changing the filename extension, MIME type, request headers, and file contents to determine whether server-side validation can be bypassed.
- Secure implementations should:
    - Ignore client-provided filenames.
    - Generate server-side filenames and safe extensions.
    - Store uploads outside the web root whenever possible.
    - Disable script execution inside upload directories.
#### Takeaways
- Never trust client-controlled metadata, including hidden form fields.
- Client-side restrictions provide no security.
- File uploads should always be validated server-side.
- Allowing uploaded files to be executed by the web server can lead directly to RCE.
#### Pass 13
g8ba0olAzaSJuyS4gnmbdVVigAICLG1k
