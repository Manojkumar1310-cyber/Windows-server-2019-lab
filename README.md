# Windows Server 2019 Administration Lab  
**A comprehensive lab environment for practicing Active Directory, DNS, DHCP, Group Policy, and core Windows Server administration tasks.**  

---

## **Lab Overview**  
This lab simulates a real-world Windows Server 2019 environment with the following roles and features:  
✅ **Active Directory Domain Services (AD DS)** – Domain controller setup and user/group management  
✅ **DNS Server** – Name resolution and forward/reverse zones  
✅ **DHCP Server** – IP address management and scope configuration  
✅ **Group Policy Objects (GPOs)** – Centralized policy management for users and computers  
✅ **File & Print Services** – Shared folders and printer management  
✅ **Basic PowerShell Automation** – Common admin tasks via PowerShell  

---

## **Lab Requirements**  

### **Hardware Requirements**  
- **Minimum**: 8GB RAM, 4-core CPU, 100GB disk space (SSD recommended for better performance)  
- **Recommended**: 16GB+ RAM, 6-core CPU, 200GB+ SSD  
- **Virtualization Support**: Intel VT-x / AMD-V enabled in BIOS  

### **Software Requirements**  
- **Hypervisor**: VMware Workstation, Hyper-V, or VirtualBox  
- **OS Images**:  
  - **Windows Server 2019** (Evaluation ISO available from Microsoft)  
  - **Windows 10/11** (for client testing, optional)  

---

## **Lab Setup Guide**  

### **1. Virtual Machines (VMs) Setup**  
| **VM Name**  | **Role**               | **vCPU** | **RAM** | **Disk** | **Network** |  
|--------------|------------------------|----------|---------|----------|-------------|  
| **DC1**      | Domain Controller      | 2        | 4GB     | 50GB     | NAT/Bridged |  
| **SRV1**     | Member Server (DHCP/DNS)| 2        | 4GB     | 50GB     | NAT/Bridged |  
| **CLIENT1**  | Windows 10/11 Client   | 2        | 2GB     | 40GB     | NAT/Bridged |  

### **2. Installation Steps**  

#### **Step 1: Install & Promote DC1 as Domain Controller**  
1. Install Windows Server 2019 on **DC1**.  
2. Set a static IP (e.g., `192.168.1.10/24`, Gateway `192.168.1.1`, DNS `127.0.0.1`).  
3. Install **Active Directory Domain Services (AD DS)** and **DNS Server** roles:  
   ```powershell
   Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
   Install-WindowsFeature DNS -IncludeManagementTools
   ```  
4. Promote the server to a domain controller and create a new forest (e.g., `lab.local`).  

#### **Step 2: Configure SRV1 as Member Server**  
1. Install Windows Server 2019 on **SRV1**.  
2. Set a static IP (e.g., `192.168.1.20/24`, DNS pointing to `DC1 (192.168.1.10)`).  
3. Join **SRV1** to the domain (`lab.local`).  
4. Install **DHCP Server** role:  
   ```powershell
   Install-WindowsFeature DHCP -IncludeManagementTools
   ```  
5. Authorize the DHCP server in AD and create a scope (e.g., `192.168.1.100-192.168.1.200`).  

#### **Step 3: Set Up CLIENT1 for Testing**  
1. Install Windows 10/11 on **CLIENT1**.  
2. Configure for DHCP (should get an IP from **SRV1**).  
3. Join the domain (`lab.local`) and test logins with AD users.  

---

## **Lab Exercises**  

### **1. Active Directory Management**  
✔ Create OUs (e.g., `Users`, `Computers`, `Servers`)  
✔ Add users and groups (e.g., `Helpdesk`, `Admins`)  
✔ Test login with domain accounts  

### **2. DNS & DHCP Configuration**  
✔ Create forward/reverse lookup zones  
✔ Test DNS resolution (`nslookup`, `ping`)  
✔ Configure DHCP reservations for servers  

### **3. Group Policy (GPO) Deployment**  
✔ Enforce password policies  
✔ Deploy desktop restrictions  
✔ Map network drives via GPO  

### **4. File & Print Services**  
✔ Create shared folders with NTFS permissions  
✔ Test access from **CLIENT1**  
✔ (Optional) Set up a network printer  

### **5. PowerShell Automation**  
✔ Bulk user creation (`New-ADUser`)  
✔ Export AD users to CSV  
✔ Remote server management  

---

## **Troubleshooting Tips**  
🔹 **Can’t join domain?** Verify DNS points to **DC1**.  
🔹 **DHCP not leasing IPs?** Ensure the scope is activated and authorized in AD.  
🔹 **GPO not applying?** Run `gpupdate /force` and check `rsop.msc`.  

---

## **Resources**  
📌 [Microsoft Windows Server 2019 Docs](https://docs.microsoft.com/en-us/windows-server/)  
📌 [Active Directory PowerShell Commands](https://learn.microsoft.com/en-us/powershell/module/activedirectory/)  
📌 [Windows Server Lab Best Practices](https://techcommunity.microsoft.com/)  

---

### **Happy Labbing!** 🚀  
_Experiment, break things, and learn how to fix them—this is how you master Windows Server!_
