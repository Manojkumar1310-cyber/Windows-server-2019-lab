🧪 Lab 2: Promote Server to Domain Controller

Objective

Convert the Windows Server 2019 installation into a fully functioning Domain Controller (DC) with Active Directory and DNS roles.

🔧 Steps to Promote the Server

1. Install AD DS and DNS Roles

Open Server Manager → click Add roles and features.

Select Role-based or feature-based installation.

Choose the local server.

From the Roles list, check:

Active Directory Domain Services

DNS Server

Click Next through features → Install.

![add-roles-ad-ds](./images/image-23.png)

2. Promote Server to Domain Controller

Once installed, a yellow exclamation will appear in Server Manager.

Click "Promote this server to a domain controller".

Configuration:

Select: Add a new forest

Root domain name: domain.local

![Promote this server](./images/image-24.png)

Set Directory Services Restore Mode (DSRM) password

![Restore Mode (DSRM) password](./image/image-25.png)
Confirm NetBIOS name → Default is DOMAIN



Click Next, then Install. Server will reboot.

![review options](./image/image-26.png)


3. Post-Installation Verification

Log in as domain\Administrator

Open Active Directory Users and Computers (ADUC)

Confirm domain.local is listed

![aduc-verify](./image/image-27.png)

Open DNS Manager → verify forward/reverse zones
![forword lookup zone](./images/image-28.png)
![Reverse lookup zone](./image/image-29.png)
