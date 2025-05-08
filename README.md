# Windows Server 2019 Administration Lab Project

This repository contains a structured lab project designed to demonstrate Windows Server 2019 administration skills. It includes Active Directory, DNS, DHCP, Group Policies, OU management, file sharing, and more. Ideal for portfolio showcase or hands-on practice.

---

## 📁 Folder Structure

```
win-server-2019-lab/
├── README.md
├── Lab1_Install_Server.md
├── Lab2_Setup_AD_DS.md
├── Lab3_Join_Client.md
├── Lab4_OUs_Users.md
├── Lab5_GPO.md
├── Lab6_File_Sharing.md
├── Lab7_DHCP_DNS.md
├── Lab8_Remote_Desktop.md
├── troubleshooting.md
```

---

## 🔧 Labs Included

| Lab # | Title                              | Description |
|-------|------------------------------------|-------------|
| 1     | Install Windows Server 2019        | Set up a virtual server for the lab environment |
| 2     | Install & Configure AD DS          | Promote to Domain Controller and configure forest/domain |
| 3     | Join Client Machine to Domain      | Add a Windows 10/11 client to your domain |
| 4     | Create OUs, Users, Groups          | Manage Active Directory objects |
| 5     | Group Policies                     | Apply security and user environment policies |
| 6     | File Sharing with Permissions       | Configure shared folders with NTFS and Share permissions |
| 7     | DHCP & DNS Setup                   | Automate IP addressing and name resolution |
| 8     | Remote Desktop Setup               | Enable and manage RDP access for domain users |

---

## 🛠️ Troubleshooting

Refer to `troubleshooting.md` for solutions to common issues like:
- Domain join failures
- DNS not resolving
- Group Policy not applying
- RDP connectivity issues

---

## 🧑‍💻 Requirements
- Hyper-V or VirtualBox
- Windows Server 2019 ISO
- Windows 10/11 ISO (for client machines)
- Minimum 12 GB RAM and 100 GB disk (recommended)

---

## 💡 Tip
Always take snapshots/checkpoints before major changes to revert in case of misconfiguration.

---

## 📬 Contact / Credits
Created by [Your Name]. Feel free to fork, contribute, or reach out via GitHub!

---

---

# Lab1_Install_Server.md

## 🎯 Objective
Set up a virtual machine running Windows Server 2019.

## 🧰 Requirements
- Hyper-V or VirtualBox
- Windows Server 2019 ISO

## 📝 Steps
1. Create a new VM (min 2 vCPU, 4GB RAM, 40GB HDD).
2. Attach Windows Server 2019 ISO.
3. Boot the VM and install Windows Server 2019 Standard (Desktop Experience).
4. Set Administrator password.
5. Set a static IP address.

## ✅ Outcome
A clean install of Windows Server 2019, ready for domain setup.

---

# Lab2_Setup_AD_DS.md

## 🎯 Objective
Install Active Directory Domain Services and promote the server to a Domain Controller.

## 📝 Steps
1. Open Server Manager → Add Roles and Features.
2. Install “Active Directory Domain Services” role.
3. After installation, click “Promote this server to a domain controller”.
4. Choose “Add a new forest” → domain: `lab.local`
5. Set DSRM password, complete the wizard, and reboot.

## ✅ Outcome
Your server is now a domain controller for `lab.local`.

---

# Lab3_Join_Client.md

## 🎯 Objective
Join a Windows 10/11 client to the domain.

## 📝 Steps
1. Set client’s DNS to point to the server’s IP.
2. Rename client PC appropriately (e.g., `CLIENT01`).
3. Join domain: `System Properties → Domain: lab.local`
4. Provide domain admin credentials.
5. Reboot the client.

## ✅ Outcome
Client successfully joins the domain and appears in AD Users and Computers.

---

# Lab4_OUs_Users.md

## 🎯 Objective
Create Organizational Units (OUs), users, and groups in Active Directory.

## 📝 Steps
1. Open “Active Directory Users and Computers” (ADUC).
2. Create OUs: `Users`, `Computers`, `Admins`, `HR`, `IT`.
3. Create users with strong passwords.
4. Create security groups: `HRGroup`, `ITGroup`.
5. Assign users to groups.

## ✅ Outcome
A structured AD layout with users and groups.

---

# Lab5_GPO.md

## 🎯 Objective
Create and apply Group Policy Objects to manage user/computer settings.

## 📝 Steps
1. Open “Group Policy Management”.
2. Create a new GPO (e.g., `DisableCMD`) → Edit.
3. User Config → Admin Templates → System → “Prevent access to command prompt” = Enabled.
4. Link GPO to `IT` OU.
5. Run `gpupdate /force` on client.

## ✅ Outcome
CMD disabled for users in the IT OU.

---

# Lab6_File_Sharing.md

## 🎯 Objective
Set up shared folders with proper permissions.

## 📝 Steps
1. Create folder `D:\Shared` on DC or File Server.
2. Share it with `HRGroup` – Read or Modify.
3. Set NTFS permissions to match.
4. On client, map network drive: `\\SERVER\Shared`

## ✅ Outcome
HR users can access the shared folder with set permissions.

---

# Lab7_DHCP_DNS.md

## 🎯 Objective
Configure DHCP to assign IPs and DNS to resolve hostnames.

## 📝 DHCP Steps
1. Install DHCP role.
2. Create new IPv4 Scope: 192.168.1.100 – 192.168.1.200
3. Set options:
   - Router: 192.168.1.1
   - DNS: Server’s IP
4. Authorize and activate scope.

## 📝 DNS Steps
1. Open DNS Manager.
2. Ensure `lab.local` zone exists.
3. Add A-records for key devices.

## ✅ Outcome
Clients receive IPs from DHCP and resolve internal names via DNS.

---

# Lab8_Remote_Desktop.md

## 🎯 Objective
Enable and secure Remote Desktop access for users.

## 📝 Steps
1. Enable RDP: `System > Remote Settings > Allow Remote Connections`
2. Add users to `Remote Desktop Users` group.
3. Configure firewall: allow port 3389.
4. Test RDP from client using domain user.

## ✅ Outcome
Users can remotely access the server using their domain credentials.

---

# troubleshooting.md

## 🔧 Common Lab Issues & Fixes

### 1. Client Can’t Join Domain
- Set client DNS to server’s IP.
- Ensure server is reachable: `ping lab.local`
- Sync time on both machines.

### 2. GPOs Not Applying
- Run `gpupdate /force`
- Check with `gpresult /r`
- Ensure correct OU and no conflicting GPOs.

### 3. Can’t Access Shared Folder
- Check NTFS and Share permissions.
- Use `Effective Permissions` to test.

### 4. RDP Not Working
- Ensure RDP is enabled.
- Add user to Remote Desktop group.
- Allow port 3389 through firewall.

### 5. DHCP Not Giving IP
- Scope inactive or exhausted.
- Client not on correct virtual switch.

---

End of Lab Documentation ✅
