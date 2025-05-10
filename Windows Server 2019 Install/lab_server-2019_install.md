WINDOWS SERVER 2019 LAB

Requirements:
 Hyper-V or VirtualBox
- Windows Server 2019 ISO
- Windows 10/11 ISO (for client machines)
- Minimum 12 GB RAM and 100 GB disk (recommended)



Download the server 2019 ISO from the link provided: 
Windows Server 2019 Link: 
[Windows Server 2019 | Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

![ISO Download page](./images/image.png)
 
Now open Hyper-V or Virtual Box :

and select create a Virtual switch, and set it to Internal.

 ![Action-VirtualSwitch](./images/image-1.png)           
 ![VirtualSwitch-Manager](./images/image-2.png)

 Now apply the setting

 ![VirtualSwitch-Manager1](./images/image-3.png)


In Hyper-V action bar, select New->New Virtual Machine

![Action create VM](./images/image-4.png)
 

 Name and location of the VM 
 ![Name Location](./images/image-5.png)
 this is name of the machine not the actual VM
           
 Always select Generation 2 for the Generation 
![Gen-2](./images/image-6.png)

Gen 2 uses UEFI (Unified Extensible Firmware Interface) instead of traditional BIOS.
More secure and faster booting.Supports Dynamic Memory more efficiently.

 ![Assigning Memory](./images/image-7.png)

Use 4096GB RAM for the Server 



Select Switch that we created at the start

![Switch config](./images/image-8.png)


Check the Name, location and size(50GB) of the VM
![Storage and location](./images/image-9.png) 

In installation option, Select the second option and in Image, select the Windoes Server 2019 ISO
![Select ISO](./images/image-10.png)

	
Now the VM Will be created and connect to the VM and follow  Basic OS installation process

![HOME with VM](./images/image-11.png)



![Boot time](./images/image-12.png)
Windows Server 2019 Desktop Experiance for the desktop interface 
![OS version Standard desktop experiance](./images/image-13.png)

for First time, select Custom installation
![Upgrade or Custom installation](./images/image-14.png)


Craete new and apply. select next to install OS 
![Disk Partition](./images/image-15.png)

After setup the windows will restart with OS installed
![Setting up](./images/image-16.png)


Once the restart is complect. you'll set the admininstrator Password
 ![Admin-Password](./images/image-17.png)

In Desktop You'll see the Server Manager 
![Server manager page](./images/image-18.png)

	
     













