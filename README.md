<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Preparing AD Infrastructure in Azure
- Deploying Active Directory
- Creating users with PowerShell
- Group policy and Managing Accounts

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/x2nOmFj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I started by creating a resource group, virtual networks, and subnet, I also created a domain controller VM (Windows Server 2022) named "DC-1". After creating DC-1 VM, I set the Domain Controller’s NIC Private IP address to be static as shown in the image above. After logging into the VM I disabled the Windows Firewall, to test the connectivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/oA06C7R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moreover, I created the Client VM (Windows 10) named “Client-1” and then, attached it to the same region and virtual network as DC-1. After the VM was created, Client-1’s DNS settings were set to DC-1’s Private IP address, therefore after, From the Azure Portal, I restarted Client-1 and then logged into Client-1 attempting to ping DC-1’s private IP address then I ensured the ping succeeded which it did. Then after, From Client-1, I opened PowerShell and ran ipconfig /all, The output for the DNS settings was showing  DC-1’s private IP Address circled in red ink in the image above.

</p>
<br />

<p>
<img src="https://i.imgur.com/1CkmlaY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I started  by logging into DC-1 and installing Active Directory Domain Services. Next, I configured the active directory to become a domain controller, after a new forest was set as mydomain.com, I restarted and logged back into DC-1 as a user. Furthermore, in Active Directory Users and Computers (ADUC), I created an Organizational Unit (OU) called “_EMPLOYEES” then after, I Created another new OU named “_ADMINS”. Next, I made a new employee named “Jane Doe” with the username of “jane_admin” / Cyberlab123! as the password, then I added jane_admin to the “Domain Admins” Security Group, then I logged out which closed the connection to DC-1, and logged back in as “mydomain.com\jane_admin”. From now on, the user jane_admin will be my admin account. Moreover, I logged into the domain controller and verified if Client-1 showed up in ADUC, then I created a new OU named “_CLIENTS” and dragged Client-1 into it as shown in the image above.



</p>
<br />

<p>
<img src="https://i.imgur.com/MTPeRJ5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I began by logging into Client-1 as mydomain.com\jane_admin opened system properties clicked on “Remote Desktop” and then again clicked on allow “domain users” access to remote desktop. Moreover, I can now log into Client-1 as a normal, non-administrative user as shown in the image above. Normally this would be done with a Group Policy that allows you to change many systems at once, this was done already in a future lab.

</p>
<br />

<p>
<img src="https://i.imgur.com/ebArncr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I moved on to create a bunch of additional users and attempted to log into client-1 with one of the users. I started this step by logging in to DC-1 as jane_admin then opened PowerShell_ise as an administrator I created a new file and pasted the contents of the script into it then Ranned the script and observed the accounts being created, when that process was finished, I opened ADUC and observe the accounts in the appropriate Organizational Unit (OU) under the name "_EMPLOYEES". Lastly, I attempted to log into Client-1 with one of the accounts and It was successful an example is shown in the image above.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
