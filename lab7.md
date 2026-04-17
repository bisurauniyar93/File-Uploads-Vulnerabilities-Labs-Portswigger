Lab: Web Shell upload via race condition

##  Objective
The goal of this lab is to exploit a race condition in the file upload mechanism to upload a PHP web shell and retrieve the contents of 
/home/carlos/secret

##  Vulnerability
The application performs robust validation on uploaded files.However,the process is flawed:
- The file is temporary stored on the server before validation completes
- During this short time window,the file is accessible.
- If accessed quickly enough,the server executes the file before it is deleted.
  THIS RESULTS IN A RACE-CONDITION (TOCTOU -TIME-OF-CHECK TO TIME-OF-USE) Vulnerability 

##  Steps

##  Exploit

##Payload used

##  Proof
Screenshot or request

## Lesson Learned
What you understood
# Lab: Web shell upload via extension blacklist bypass
