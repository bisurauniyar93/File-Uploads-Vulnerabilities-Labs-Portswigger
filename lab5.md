# Lab:Web Shell upload via obfuscated file extension 

##  Objective 
Explore an insecure file upload vulnerability to achieve remote code execution by uploading a php web shell and retrive sensitive data from the server (/home/carlos/secret)

##  Vulnerability
The application is vulnerable to unrestricted file upload,as it fails to validate file types and content.This allows attackers to upload and execute files(eg.a PHP web shell),leading to remote code execution.

##  Steps
Log in using the provided credentials(wiener:peter),
Navigate to the image upload functionality,
Create a simple php file without any restrictions,
Access the uploaded file via the browswer to execute commands,
change the file type from file.php to file.php.jpg and then to different file extensions like .jpg.php , .php.jpg , .pHp , .php%00.jpg , .php;.jpg .
And finally .jph%00.jpg will work.
Use the web shell to read /home/carls/secret.
Sunmit the retrived secret to compare the lab.

##  Exploit

PHP Web Shell Payload: <?php echo file_get_contents('/home/carlos/secret'); ?>

Bypass Technique: Modified the file name from filename=file.php to filename=php%00.jpg using Burp Suite.  The server trusted this user-controlled header and allowed the PHP file upload.

Content-Type: application/octet-stream

--

##Payload used
<?php echo file_get_contents('/home/carlos/secret'); ?>

##  Proof
![WhatsApp Image 2026-04-13 at 09 37 34](https://github.com/user-attachments/assets/9a110c0e-dc5e-4edf-ac05-5dad3d1d6aeb)
![WhatsApp Image 2026-04-13 at 09 37 34(2)](https://github.com/user-attachments/assets/1cbacb5c-f5c2-4c18-94ee-0b6f2e39b2bd)
![WhatsApp Image 2026-04-13 at 09 40 34](https://github.com/user-attachments/assets/11b4ced0-f750-485e-ab68-5f95b80b3d06)
![WhatsApp Image 2026-04-13 at 09 40 34](https://github.com/user-attachments/assets/a4322adc-c9f6-4f31-a35d-3740bbdcf5d2)
![WhatsApp Image 2026-04-13 at 09 40 34](https://github.com/user-attachments/assets/de14ccea-8aa3-4e17-a9b2-ae4b011e6933)
![WhatsApp Image 2026-04-13 at 09 37 34(1)](https://github.com/user-attachments/assets/ad4709e1-8834-44d6-b857-08202ec07f7e)




## Lesson Learned
Never trust client-controlled headers like Content-Type
File upload validation must be done server-side
Improper validation can lead to Remote Code Execution (RCE)
Always test multiple bypass techniques (Content-Type, extension, magic bytes, etc.)
File upload vulnerabilities are highly critical in real-world applications
