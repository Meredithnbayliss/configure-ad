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

In Step 1: we create the Domain Controller VM (Windows Server 2022) named “DC-1
</p>
</p>
<img src="https://i.imgur.com/g6RYhLn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In step 2, we create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<br />
</p>
</p>
<img src="https://i.imgur.com/OYAt5Mq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
</p>
In step 3, we set Domain Controller’s NIC Private IP address to be static:
</p>
</p>
<img src="https://i.imgur.com/61MjZuk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
</p>
In step 4, w ensure that both VMs are in the same Vnet (we can check the topology with Network Watcher):
</p>
</p>
<img src="https://i.imgur.com/89KptH5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 5, we ensure Connectivity between the client and Domain Controller

Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (perpetual ping):
</p>
</p>
<img src="https://i.imgur.com/Rbx0OLB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 6, we ogin to the Domain Controller and enable ICMPv4 in on the local windows firewall:
</p>
</p>
<img src="https://i.imgur.com/KmxQmP9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 7, we check back at Client-1 to see the ping succeed:
</p>
</p>
<img src="https://i.imgur.com/hCCekZt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 8, we install Active Directory

Login to DC-1 and install Active Directory Domain Services:
</p>
</p>
<img src="https://i.imgur.com/AiCVY4o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 9, we promote as a Domain Controller:
</p>
</p>
<img src="https://i.imgur.com/aSUybbB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 10, we setup a new forest as myactivedirectory.com (can be anything, just remember what it is - I ultimately did set it up as meredithdomain.com which you'll see in the next pic):
</p>
</p>
<img src="https://i.imgur.com/Ug7AvHN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 11, we restart and then log back into DC-1 as user: meredithdomain.com\meredithnbayliss:
</p>
</p>
<img src="https://i.imgur.com/c1ga4x8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 12, we create an Admin and Normal User Account in AD

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS":
</p>
</p>
<img src="https://i.imgur.com/76sWxK3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<img src="https://i.imgur.com/7y7nJKL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In Step 13, we create a new employee named “Jane Doe” with the username of “jane_admin”:
</p>
</p>
<img src="https://i.imgur.com/UBNfBde.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 14, we add jane_admin to the “Domain Admins” Security Group:
</p>
</p>
<img src="https://i.imgur.com/fuk7lXb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 15, we log out/close the Remote Desktop connection to DC-1 and log back in as “myadproject.com\jane_admin”. Use jane_admin as your admin account from now on:
</p>
</p>
<img src="https://i.imgur.com/NjLgzkE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 16, we join Client-1 to your domain (myadproject.com)

From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address:
</p>
</p>
<img src="https://i.imgur.com/5GKlUew.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 17, from the Azure Portal, we restart Client-1.

Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart):
</p>
</p>
<img src="https://i.imgur.com/wsmZcDu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 18, we setup Remote Desktop for non-administrative users on Client-1

Log into Client-1 as mydomain.com\jane_admin and open system properties.

Click “Remote Desktop”.

Allow “domain users” access to remote desktop.

We can now log into Client-1 as a normal, non-administrative user now.

Normally we would want to do this with Group Policy that allows us to change MANY systems at once (maybe a future lab):
</p>
</p>
<img src="https://i.imgur.com/I6htlo7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 19, we create a bunch of additional users and attempt to log into client-1 with one of the users

Login to DC-1 as jane_admin

Open PowerShell_ise as an administrator.

Create a new File and paste the contents of this script (https://github.com/Meredithnbayliss/configure-ad/blob/main/adscripts.1) into it. Run the script and observe the accounts being made
</p>
</p>
<img src="https://i.imgur.com/pfP7kZ0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<img src="https://i.imgur.com/QMDCUvC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
In step 20, we open ADUC and observe the accounts in the appropriate OU and attempt to log into Client-1 with one of the accounts (take note of the password in the script): in this example I'm going to login using user "Befo Ser."
</p>
</p>
<img src="https://i.imgur.com/7ipEsvR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<img src="https://i.imgur.com/LgT8W2t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<img src="https://i.imgur.com/MJOto2h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
I hope this tutorial helped you learn a little bit about network security protocols and observe traffic between virtual machines.

Now that we're done, don't forget to clean up our azure environment so that we don't incur unnecessary charges.

W close our Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.
