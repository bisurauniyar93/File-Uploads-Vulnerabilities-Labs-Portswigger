
## Lab: Remote Code Execution via polyglot web shell upload

## Objective
The goal of this lab is to bypass strict image content validation,upload a polyglot web shell,and use it to retrieve the contents of /home/carlos/secret

## Vulnerability
The application attempts to validate uploads by checking file contents to ensure it is a genuine image.
However
- It does not properly sanitize embedded code inside the image.
- It allows file that are valid images and valid PHP scripts(polyglots)
- The server executes PHP code if present,even within image files.
  This leads to Remote Code Execution (RCE).


## Steps
1. Logged into the application using credentials wiener:peter.
2. Navigated to the avatar upload functionality.
3. Attempted to upload a PHP file, but it was blocked due to blacklist filtering.
4. Changed the file extension and also used different techniques like double                    extension,content form changed but neither of them worked
5. Then i decided to add my php code into the image metadata:used exiftool to parse the data of the jpg and using exiftool with the jpg name - exiftool smita.jpg i came to find the metadata of the jpg file.
   Then i tried to include my php file into the meta data using the following command in kali Linux
   
   exiftool -Comment="<?php echo 'START '. file_get_contents(' /home/carlos/secret') . ' END'; ?>" smita.jpg -o smita.php
   
   and after using the above command a php file was created which i furher uploaded in the choose upload in the avatar.  
7. The file executed and displayed the contents of /home/carlos/secret.

## Exploit
By embedding PHP code inside a valid image file(polyglot),the attacker bypasses content validation and achieves code execution when the file is accessed.

## Payload used
<?php echo file_get_contents('/home/carlos/secret'); ?>

## Proof
<img width="1317" height="688" alt="WhatsApp Image 2026-04-17 at 09 06 08" src="https://github.com/user-attachments/assets/e6e33fab-a5d2-40c1-871a-35705c4ffa15" />

<img width="1324" height="690" alt="WhatsApp Image 2026-04-17 at 09 06 08(1)" src="https://github.com/user-attachments/assets/0cad3a3c-90ea-42bf-8a0b-34d2c3cf982b" />


<img width="1355" height="666" alt="WhatsApp Image 2026-04-17 at 09 06 08(2)" src="https://github.com/user-attachments/assets/9e593d25-ae6a-4bd4-9006-b60eeedc7879" />

<img width="650" height="448" alt="WhatsApp Image 2026-04-17 at 09 06 08(3)" src="https://github.com/user-attachments/assets/83fe07aa-d8fe-4ac9-90ae-b2c9be347b2e" />

<img width="774" height="405" alt="WhatsApp Image 2026-04-17 at 09 06 08(4)" src="https://github.com/user-attachments/assets/d509895e-752a-4646-92c9-8d747b00935f" />

<img width="1043" height="489" alt="WhatsApp Image 2026-04-17 at 09 06 08(5)" src="https://github.com/user-attachments/assets/c8af09ef-afba-4c8b-b621-473318372ec1" />

<img width="1161" height="517" alt="WhatsApp Image 2026-04-17 at 09 06 08(6)" src="https://github.com/user-attachments/assets/d51a73b8-717a-4c2c-b346-0a03780f313e" />

<img width="903" height="498" alt="WhatsApp Image 2026-04-17 at 09 06 08(7)" src="https://github.com/user-attachments/assets/efba20b9-1aa3-4c8c-94dd-2c53d511043a" />

<img width="1168" height="531" alt="WhatsApp Image 2026-04-17 at 09 06 08(8)" src="https://github.com/user-attachments/assets/12bfeec2-e79f-4391-aac2-cd82e354beea" />

## Lesson Learned
- Content validation alone is not sufficient.
- Files can be both: (valid images and malicious script(polyglots)
- Server may executes embedded php even inside safe files.
- Use strict allowlists for file types
- Verify file structure beyond simple checks
- Strip metadata and re-encode images
- Store uploads outside the web root
- Disable execution in upload directories
   
