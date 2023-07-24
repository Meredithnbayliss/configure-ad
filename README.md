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
- Join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a manu additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

In Step 1: We create a Resource Group inside Azure.

<p>
<img src="https://i.imgur.com/C1atwQb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In step 2, create your Windows virtual machine. I typically create the VM in (US) East US.

While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the Administrator Account section:
</p>
<br />

<p>
