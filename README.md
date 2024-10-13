# Implementing-Identity-and-Access-Controls-on-Linux-and-Windows-Operating-Systems

## Objective

In this lab, I applied my knowledge of access controls and group policy management by configuring password policies and user permissions on both Windows and Linux operating systems. This hands-on experience enhanced my understanding of identity and access management and is crucial for roles in cybersecurity and system administration.

### Skills Learned

- Implemented access controls on both Windows and Linux environments, setting up user and group permissions.
- Configured advanced password policies and account lockout settings using Group Policy Objects (GPO) on Windows Server.
- Created users and groups in Active Directory, managing access permissions for shared folders.
- Used commands to create users, groups, and assign directory ownership and permissions.
- Used John the Ripper to audit and identify weak passwords on a Linux system, improving security configurations.
- Created and requested certificates using the IIS manager, demonstrating the ability to manage secure connections.
- 
### Tools Used

- **Azure Virtual Machine.**
- **Windows Server** For configuring password policies, managing user permissions with Active Directory, and setting up certificates in IIS.
- **Group Policy Management** To implement password and account lockout policies.
- **Active Directory Users and Computers (ADUC)** For managing users, groups, and folder permissions.
- **Kali Linux**  Used for managing Linux users, groups, and permissions, as well as password auditing.
- **John the Ripper** A password-cracking tool used to audit password strength.
- **IIS Manager** Used to manage and request certificates on Windows Server.

## Steps
## Part 1: Windows Server Configuration
**Step 1: Setting Up Group Policy for Password Management**
Access Group Policy Management:

Logged into the DC1 server.
Opened the Group Policy Management tool from the Server Manager.
Editing the Default Domain Policy:

Right-clicked on Default Domain Policy and selected Edit.
Navigated to Policies -> Windows Settings -> Security Settings -> Account Policies -> Password Policy.

**Configured Password Policies:**

Set Password History to 20.

Set Maximum Password Age to 60 days.

Set Minimum Password Age to 1 day.

Set Minimum Password Length to 12 characters.

Enabled Password must meet complexity requirements.
<img width="596" alt="image" src="https://github.com/user-attachments/assets/2d300782-2fd9-467c-aabb-442f4df70a65">


Set Account lockout duration to 10 minutes after 3 failed login attempts.

**Account Lockout Policies:**

Adjusted settings under Account Lockout Policy:

Lockout Duration: 10 minutes

Threshold for lockout: 3 invalid attempts.


<img width="604" alt="image" src="https://github.com/user-attachments/assets/ec1b298a-b563-45b1-b715-0c9d30c093ce">



**Step 2: User Management in Active Directory**
**Creating Folders:**
   Created two folders on the C drive: Sales Data and IT Data.
   
**Adding User to Sales Group:**
  Opened Active Directory Users and Computers.
  Verified the Sales Group exists and added user Bobby to the group.
  
  <img width="570" alt="image" src="https://github.com/user-attachments/assets/b7cc47ed-2903-46b2-9445-9569ec2151c9">

  
**Setting Folder Permissions:**

For **Sales Data** folder:

   Assigned Modify permissions to the Sales Group.

   <img width="270" alt="image" src="https://github.com/user-attachments/assets/b92d72db-9c95-48ae-bdb3-c7175ebadd89">

   
For **IT Data** folder:

   Added user Sam and explicitly denied him access to the ITData folder.

   <img width="270" alt="image" src="https://github.com/user-attachments/assets/c8b9fdc2-6193-4f0d-81cf-dfa2ce4244a8">


## Part 2: Linux Configuration
**Step 3: User and Group Management on Linux** 
**Creating a New User:**

Logged into Kali Linux.

Created a user named Floyd using the command:

<img width="97" alt="image" src="https://github.com/user-attachments/assets/b9f35cc4-9384-45b6-b0b8-9fd12e6446e3">

<img width="164" alt="image" src="https://github.com/user-attachments/assets/d72b0ee1-6d8e-4daf-b6c8-6a180613ead6">

**Creating a Group:**

Created a group called Sales:

**Directory Creation:**

Created a directory for sales information:

**Granting Permissions:**

Assigned ownership of the /sales_info directory to Floyd and the Sales group


**Set permissions so that Floyd has write and execute permissions, while the Sales group has read and execute permissions:**
I added a computer object named "Laptop01" within the domain using PowerShell. To verify, I generated a list of computers in AD and exported the results to a file on the C: drive. I confirmed the presence of "Laptop01" in the exported file.

<img width="173" alt="image" src="https://github.com/user-attachments/assets/628a68bc-b823-4cda-81ba-b8aa3489f813">


**Step 4: Password Auditing with John the Ripper**

**Creating a New User:**

Added another user Bobby and set his password:

<img width="341" alt="image" src="https://github.com/user-attachments/assets/22873b78-0f35-49b1-bdb8-1b29bb4a56e6">


**Using John the Ripper:**

**Utilized John the Ripper to audit the password strength:**

**Unzipped the RockYou Wordlist:**

I used the rockyou.txt wordlist that comes with Kali Linux, unzipping it for use with John the Ripper.


<img width="175" alt="image" src="https://github.com/user-attachments/assets/38fad3a8-e5b3-435f-b6e2-8963c5093bac">

**Edited the Wordlist:**

Opened the wordlist using vim and added a specific password to the top of the file for testing.

<img width="153" alt="image" src="https://github.com/user-attachments/assets/054cb220-c01d-4f78-a895-addd75f99518">

Run the following command to create a text file of usernames and password hashes:

<img width="347" alt="image" src="https://github.com/user-attachments/assets/7ae685fb-9fb4-4e33-bee3-d5ade96cddbd">

Cracked Passwords with John the Ripper:

Ran John the Ripper on the combined file using the modified wordlist.

<img width="426" alt="image" src="https://github.com/user-attachments/assets/ddcc1661-d31b-4e1b-95e8-c03bd5c39d92">

Saved the Results:
Redirected the cracked passwords into a file for future reporting.

<img width="337" alt="image" src="https://github.com/user-attachments/assets/bdcf8938-86a9-4420-8f4d-54f52fb68685">


