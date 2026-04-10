# Lab:Web Shell upload via path traversal

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


## Lesson Learned
Never trust client-controlled headers like Content-Type
File upload validation must be done server-side
Improper validation can lead to Remote Code Execution (RCE)
Always test multiple bypass techniques (Content-Type, extension, magic bytes, etc.)
File upload vulnerabilities are highly critical in real-world applications
