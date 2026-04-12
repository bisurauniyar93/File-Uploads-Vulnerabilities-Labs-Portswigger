# Lab:Web Shell upload via extension blacklist bypass

##  Objective
The Goal of this lab is to upload a PHP web shell and use it to retrive the contents of the file /home/carlos/secret by bypassing the file extension blacklist.

##  Vulnerability
The application uses a blacklist to block certain dangerous file extensions such as .php.However ,this blacklist is incomplete and fails to block alternative PHP extensions like .phtml,which are still executed by the server.

##  Steps
1. Logged into the application using credentials winner:peter
2. Navigated to the avatar avatar upload functionality
3. Attempted to upload a PHP file,but it was blocked due to blacklist filtering.
4. Changed the file successfully as the blacklist did not block this extension.
5. Uploaded the file successfully as the blacklist did not block this extension.
6. Accessed the uploaded file via: /files/avatars/shell.phtml
7. The file executed and displayed the contents of /home/carlos/secret
   

##  Exploit
Bypassing the blacklist 

##Payload used

##  Proof (optional)
Screenshot or request

## Lesson Learned
What you understood
