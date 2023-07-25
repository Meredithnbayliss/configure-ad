<p align="center">
<img src="https://i.imgur.com/nWb3kwY.png" alt="osTicket logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>

This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>List of Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mine is called meredithdomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a manu additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

In Step 1: Create the Domain Controller VM (Windows Server 2022) named “DC-1
</p>
</p>
<img src="https://i.imgur.com/g6RYhLn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In step 2, Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<br />
</p>
</p>
<img src="https://i.imgur.com/OYAt5Mq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
</p>
In step 3, Set Domain Controller’s NIC Private IP address to be static:
</p>
</p>
<img src="https://i.imgur.com/61MjZuk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
</p>
In step 4, Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher):
</p>
</p>
<img src="https://i.imgur.com/89KptH5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 5, Ensure Connectivity between the client and Domain Controller

Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (perpetual ping):
</p>
</p>
<img src="https://i.imgur.com/Rbx0OLB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 6, Login to the Domain Controller and enable ICMPv4 in on the local windows firewall:
</p>
</p>
<img src="https://i.imgur.com/KmxQmP9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 7, Check back at Client-1 to see the ping succeed:
</p>
</p>
<img src="https://i.imgur.com/hCCekZt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 8, Install Active Directory

Login to DC-1 and install Active Directory Domain Services:
</p>
</p>
<img src="https://i.imgur.com/AiCVY4o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 9, Promote as a Domain Controller:
</p>
</p>
<img src="https://i.imgur.com/aSUybbB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 10, Setup a new forest as myactivedirectory.com (can be anything, just remember what it is - I ultimately did set it up as meredithdomain.com which you'll see in the next pic):
</p>
</p>
<img src="https://i.imgur.com/Ug7AvHN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>



