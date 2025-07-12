Scopes🧪 Lab 05: DHCP Setup

1. Install DHCP Server Role
Open PowerShell as an Administrator:

Server Manager:

Open Server Manager → Manage → Add Roles and Features.

Choose DHCP Server → click Next → Install.

Or via powershell

Install-WindowsFeature -Name DHCP -IncludeManagementTools

2. Authorize the DHCP Server in Active Directory
If your server is part of a domain:

powershell

Add-DhcpServerInDC -DnsName "your-dhcp-server-name" -IpAddress "your-dhcp-server-ip"
Or via DHCP console:

Open DHCP Management Console → Right-click on the server → Authorize.

3. Configure DHCP Scopes
A DHCP Scope defines the range of IP addresses that can be assigned to clients.

Example:

Network: 192.168.10.0/24

Scope Range: 192.168.10.100 to 192.168.10.200

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.10.1

DNS Server: 8.8.8.8

In PowerShell:

powershell

Add-DhcpServerv4Scope -Name "LabScope" -StartRange 192.168.10.100 -EndRange 192.168.10.200 -SubnetMask 255.255.255.0 -State Active
Add default gateway and DNS server:

powershell

Set-DhcpServerv4OptionValue -ScopeId 192.168.10.0 -Router 192.168.10.1
Set-DhcpServerv4OptionValue -ScopeId 192.168.10.0 -DnsServer 8.8.8.8
4. Verify DHCP Scope and Leases
Check scope:

powershell
 
Get-DhcpServerv4Scope
Check active leases:

powershell

Get-DhcpServerv4Lease -ScopeId 192.168.10.0
5. Test with a Client
Boot up a client VM on the same network.

In the Command Prompt:

bash

ipconfig /release
ipconfig /renew
ipconfig /all
Confirm the client gets an IP in the 192.168.10.100–200 range.

