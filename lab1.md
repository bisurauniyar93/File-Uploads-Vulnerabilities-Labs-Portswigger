#  Lab: 



## Vulnerability Type
(File Upload → e.g., Unrestricted / MIME Bypass / Extension Bypass / Storage Misconfig)

## Goal of the Lab
(What are you supposed to achieve?)
- Upload file?
- Execute code?
- Bypass filter?


## Entry Point
- Upload feature location
- Endpoint (if visible)
- Parameters involved


## Application Behavior (VERY IMPORTANT)
Observe before attacking:

- Allowed file types:
- Blocked file types:
- Error messages:
- File rename behavior:
- File storage location:
- File accessible via URL? (Yes/No)
- Is file executed or downloaded?

## Validation Analysis (CORE SECTION)

### 1. Client-Side Validation
- Any JS restricting file type?
- Can be bypassed? ✔️


### 2. Server-Side Validation
Check what server validates:

- Extension check? ✔️ / ❌  
- MIME type check? ✔️ / ❌  
- File content check? ✔️ / ❌  
- File size restriction? ✔️ / ❌  


###3. Storage Behavior
- Stored inside web root? ✔️ / ❌  
- Renamed? ✔️ / ❌  
- Randomized path? ✔️ / ❌  


## Attack Surface (Think Like Hacker)

What can you try here?

- Upload executable file?
- Bypass extension filter?
- Trick MIME type?
- Inject payload inside file?
- Access uploaded file?


##Payloads & Techniques Used

### 1. Primary Payload
```php
<?php system($_GET['cmd']); ?>


2. Bypass Technique Used
(Choose what applies)
Double extension → file.php.jpg
MIME bypass → Content-Type: image/jpeg
Null byte → file.php%00.jpg
Alternate extension → .phtml
Magic bytes → fake image header

Exploitation Steps (Step-by-Step)
Intercept request (Burp)
Modify file name / headers
Upload file
Locate uploaded file
Execute payload

File Access Path

/files/[uploaded-file]


Why It Works (DEEP THINKING)
Break it logically:
What validation failed?
What assumption did the server make?
Why did the payload bypass security?
Why was execution possible?
Example:
Server trusted file extension
Did not validate file content
Stored file in executable directory

Impact
Remote Code Execution (RCE)
Server takeover
Sensitive data access
Defacement

Real-World Mapping (VERY IMPORTANT)
If you see this in real apps:
Try multiple extensions
Always intercept request
Check file execution behavior
Look for upload → access chain

Variations to Try (Train Your Brain)
file.php.jpg
file.php.png
file.phtml
file.php%00.jpg
Change MIME type
Add magic bytes

Mitigation
Strict server-side validation
Allowlist extensions only
Store files outside web root
Rename files securely
Disable execution in upload directory

Key Learnings (Your Brain Notes)
What trick worked?
What failed?
What will you try next time?

Proof of Concept
(Add screenshot)
