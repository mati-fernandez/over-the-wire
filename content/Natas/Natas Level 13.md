### Summary
Bypassed server-side image validation by prepending valid GIF [[Magic Bytes]] to a PHP payload. Although the server verified the uploaded file with `exif_imagetype()`, it still stored the file with a `.php` extension and executed it.
### Target
The application validates uploaded files using `exif_imagetype()`, which only checks the file signature (magic bytes). It still trusts the client-controlled `filename` parameter to determine the final extension.
### Exploit
1. Inspect the source code.
2. Notice the new validation:
   ```php
   exif_imagetype($_FILES['uploadedfile']['tmp_name'])
   ```
3. Craft a polyglot payload beginning with the GIF signature:
   ```php
   GIF89a
   <?php echo file_get_contents('/etc/natas_webpass/natas14'); ?>
   ```
4. Use DevTools to change the hidden `filename` field from `.jpg` to `.php`.
5. Upload the file.
6. Open the generated URL to execute the PHP code and retrieve the password.
### Payloads / Commands
```php
GIF89a
<?php echo file_get_contents('/etc/natas_webpass/natas14'); ?>
```
### Why it works
`exif_imagetype()` only inspects the first bytes of the file to identify its format. Since the payload starts with the valid GIF signature (`GIF89a`), the validation succeeds.
Later, when the uploaded file is requested, the web server executes it as PHP because it was saved with a `.php` extension. The `GIF89a` header is treated as plain output until the interpreter reaches the `<?php` tag.
### Real-world Notes
- Validating only magic bytes or MIME types is insufficient to secure file uploads.
- Upload directories should not allow execution of server-side scripts.
- The server should generate its own filename and extension instead of trusting client-controlled metadata.
- Modern applications often combine extension validation, MIME detection, magic-byte inspection, and storage outside the web root to mitigate arbitrary file upload vulnerabilities.
### Takeaways
- File signature validation alone does not guarantee that a file is safe.
- The file extension ultimately determines how the web server processes the uploaded file.
- A single file may be interpreted differently by different programs (e.g., as an image validator and as a PHP script), enabling upload bypasses.
### Pass 14
A0xXu2x9FW8rb8OSQ4ei6n5VBbLUz8h8