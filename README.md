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
I began by logging into Client-1 as mydomain.com\jane_admin opened system properties, clicked on “Remote Desktop,” and then clicked on "Allow domain users to access the remote desktop." Moreover, as shown in the image above, I can now log into Client-1 as a normal, non-administrative user. Normally, this would be done with a Group Policy that allows you to change many systems at once.'[[[[

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
<img src="https://i.imgur.com/JiG1rCd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moving forward in this section of the lab I am now going to explain how I dealt with a locked account. I started by logging into dc-1 and picking a random user account that I created previously in my earlier explanations, then I attempted to log in with it 10 times with a bad password to get the user account locked out. Next, I configured the Group Policy to lock out the account after 5 attempts, then attempted again to log in with it 6 times with a bad password. Furthermore, I observed that the account had been locked out within Active Directory as shown in the screenshot above, then I proceeded to unlock the account and attempted to log in which was a success.


</p>
<br />

<p>
<img src="https://i.imgur.com/1zW7hEo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moving further this section I am demonstrating how I enabled and disabled an account, I started by disabling the bag.mur user account in Active Directory and attempted to login with it, and observed the error message as the account appeared to be disabled. I then re-enabled the account and attempted to login with it and it was a success. Furthermore, I observed the logs using Event Viewer and signing in as an administrator, and observed how I failed to log in because the user account I was trying to login with earlier was disabled then it showed that I was able to log in after enabling the account, as shown in the example screenshot above.



</p>
<br />

<p>
<img src="https://i.imgur.com/JiG1rCd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moving forward in this section of the lab I am now going to explain how I dealt with a locked account. I started by logging into dc-1 and picking a random user account that I created previously in my earlier explanations, then I attempted to log in with it 10 times with a bad password to get the user account locked out. Next, I configured the Group Policy to lock out the account after 5 attempts, then attempted again to log in with it 6 times with a bad password. Furthermore, I observed that the account had been locked out within Active Directory as shown in the screenshot above, then I proceeded to unlock the account and attempted to log in which was a success.


</p>
<br />
