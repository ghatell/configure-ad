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

- Active Directory Installation and Configuration 
- Joining a Client to the Domain
- Remote Desktop Setup for Non-Administrative Users
- Bulk User Creation and Testing

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="520" alt="1" src="https://github.com/user-attachments/assets/69227011-6d32-4271-9573-c7e145ee54d6" />
</p>
<p>
In this lab, we installed and configured Active Directory Domain Services (AD DS) on a virtual machine named DC-1. After logging into DC-1, Active Directory was installed, and the machine was promoted to a Domain Controller (DC) by setting up a new forest named mydomain.com. Once the setup was complete, the system was restarted, and we logged back in as mydomain.com\labuser.
</p>
<br />

<p>
<img width="591" alt="2" src="https://github.com/user-attachments/assets/e8e4489c-461f-4a17-8028-a560cad10c00" />
</p>
<p>
Next, we created a domain administrator user within the domain. Using Active Directory Users and Computers (ADUC), an Organizational Unit (OU) named _EMPLOYEES was created, followed by another OU named _ADMINS. A new user, Jane Doe, with the username jane_admin and password Cyberlab123!, was added to the domain and placed in the Domain Admins security group. We then logged out and back in as mydomain.com\jane_admin, using this account as the primary admin moving forward.
</p>
<br />

<p>
<img width="814" alt="3" src="https://github.com/user-attachments/assets/466c5034-9ccc-4421-b6fa-76f286e60514" />
</p>
<p>
The next step was to join a client machine, Client-1, to the domain. First, Client-1’s DNS settings were configured to use DC-1’s private IP address, and the machine was restarted. We logged into Client-1 as the local administrator, labuser, and joined it to the domain mydomain.com, which triggered another restart. Once completed, we logged into DC-1 and verified that Client-1 appeared in ADUC. A new OU named _CLIENTS was created, and Client-1 was moved into this OU.
</p>
<br />

<p>
<img width="321" alt="4" src="https://github.com/user-attachments/assets/5a141a1a-c003-4f04-968c-4fb8e4c54ac4" />
</p>
<p>
After turning on the VMs, we configured Remote Desktop access for non-administrative users on Client-1. While logged in as mydomain.com\jane_admin, we opened system properties, enabled Remote Desktop, and granted domain users access. This setup allowed non-administrative users to log into Client-1 via Remote Desktop. While this was done manually, in a real-world scenario, such changes would typically be applied across multiple systems using Group Policy.
</p>
<br />

<p>
<img width="1246" alt="5" src="https://github.com/user-attachments/assets/ab527a4c-6c05-43a0-8cb4-f331dd5580eb" />
</p>
<p>
To streamline user creation, we logged into DC-1 as jane_admin, opened PowerShell ISE as an administrator, and ran a script to create multiple users in the _EMPLOYEES OU. After running the script, the new accounts were visible in ADUC. To verify functionality, we logged into Client-1 using one of the newly created accounts and confirmed successful access. This exercise demonstrated how bulk user creation and account management can be efficiently handled using PowerShell.
</p>
<br />
