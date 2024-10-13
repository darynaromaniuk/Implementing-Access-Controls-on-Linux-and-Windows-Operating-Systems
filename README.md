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
Creating a New User:

Logged into Kali Linux.

Created a user named Floyd using the command:

<img width="97" alt="image" src="https://github.com/user-attachments/assets/b9f35cc4-9384-45b6-b0b8-9fd12e6446e3">


**4.Creating a User in Active Directory**
Inside the newly created "IT Admins" OU, I added a new user, setting their first name, last name, and login credentials. After creating the user, I was able to see them listed in the OU, which was now ready for management.

<img width="343" alt="image" src="https://github.com/user-attachments/assets/107be2dd-5fc7-4fed-9af2-8b83f6556c91">

**5.Creating a Security Group**
I created a new security group called "Desktop Support" within the same OU. This group would allow me to assign security settings and policies more easily to users and devices that belong to this group.

<img width="299" alt="image" src="https://github.com/user-attachments/assets/965e60b6-97a1-45d7-ba7a-76abc950ca77">


**6.Adding a Computer Object in AD**
I added a computer object named "Laptop01" within the domain using PowerShell. To verify, I generated a list of computers in AD and exported the results to a file on the C: drive. I confirmed the presence of "Laptop01" in the exported file.

<img width="328" alt="image" src="https://github.com/user-attachments/assets/f57654eb-7b8c-4b00-96da-1617fa491aa3">

<img width="401" alt="image" src="https://github.com/user-attachments/assets/d2f6d133-b4b0-4188-97f7-eeb50492b132">

<img width="404" alt="image" src="https://github.com/user-attachments/assets/3d4aa398-bee7-4fba-92e1-22c543c9b2be">


**7.Configuring Group Policy Objects (GPOs)** I then moved to the Group Policy Management Console (GPMC). Within the Default Domain Policy, I configured several password policies:

Minimum password length: 14 characters

Maximum password age: 90 days

Minimum password age: 1 day

Password history: 20 passwords

Reversible encryption: Disabled
This ensured that the security standards for user accounts in the domain met strict requirements.

<img width="637" alt="image" src="https://github.com/user-attachments/assets/b59e6627-34ab-4872-a4da-83cefe642bd7">

**8.Generating a GPO Report in PowerShell**
After setting the GPOs, I used PowerShell to generate a report of the changes, saving the file as HTML on the C: drive. I confirmed the new password policies were successfully applied and viewed the report to ensure everything was in order.

<img width="220" alt="image" src="https://github.com/user-attachments/assets/1ea55477-9652-47bd-b109-4fc3790af938">



<img width="743" alt="image" src="https://github.com/user-attachments/assets/d2eefa20-0f38-42ad-9aae-71ec118dd7ec">
