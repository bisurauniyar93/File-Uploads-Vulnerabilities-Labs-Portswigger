# Lab:Web Shell upload via path traversal

##  Objective
The goal of this lab is to upload a PHP web shell and use it to read the contents of the file /home/carlos/secret by bypassing the server's file execution restrictions.

##  Vulnerability
The application attempts to prevent execution of uploaded files by storing them in a restricted directory. However, it fails to properly validate the file path, allowing path traversal sequences (../) in the filename. This enables an attacker to upload files outside the intended directory into an executable location. 

##  Steps
1. Logged into the application using credentials wiener:peter.
2. Navigated to the avatar upload functionality.
3. Intercepted the file upload request using Burp Suite.
4. Modified the filename parameter to include path traversal sequences:
   ../../shell.php
5. Uploaded a PHP web shell instead of an image.
6. The server accepted the file and stored it outside the restricted directory.
7. Accessed the uploaded file via the browser at:
   /shell.php
8. The PHP file executed successfully and displayed the contents of /home/carlos/secret.


##  Exploit
Path traversal in the filename allowed bypassing the upload directory restriction and placing the file in an executable location.


## Payload used
<?php echo file_get_contents('/home/carlos/secret'); ?>

##  Proof 
![WhatsApp Image 2026-04-12 at 15 52 12](https://github.com/user-attachments/assets/05f5a94a-a028-40b8-ab77-0b4967627d90)

![WhatsApp Image 2026-04-12 at 15 52 13](https://github.com/user-attachments/assets/e51844d4-733e-4b88-9393-b52a41cf94fd)
![WhatsApp Image 2026-04-12 at 15 52 13(1)](https://github.com/user-attachments/assets/2da87034-b67b-4025-9e52-5db1da7c2362)

![WhatsApp Image 2026-04-12 at 15 52 13(2)](https://github.com/user-attachments/assets/204cb318-41eb-4a2e-9d12-2640032f9076)

![WhatsApp Image 2026-04-12 at 15 52 13(3)](https://github.com/user-attachments/assets/df9553a8-514e-46ae-8a47-ed53e19c46dc)
![WhatsApp Image 2026-04-12 at 15 52 13(4)](https://github.com/user-attachments/assets/29de54e2-fcc8-4109-a367-c44be01c41a1)
![WhatsApp Image 2026-04-12 at 15 52 13(5)](https://github.com/user-attachments/assets/dddbd5a0-9ff8-42b8-ae10-043044266a70)
![WhatsApp Image 2026-04-12 at 15 52 13(6)](https://github.com/user-attachments/assets/7d8ad5f8-0b52-4b2f-b9fc-d6a0979d4c57)

## Lesson Learned
- File upload restrictions can be bypassed using path traversal.
- Always validate and sanitize file paths on the server side.
- Uploaded files should be stored outside the web root or executed with strict controls.
- Never trust user-controlled filename inputs.
