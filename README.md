</p>
<br />
<p align="center">
<img src="https://static.wixstatic.com/shapes/2ebf04_1a0a78f30bf34163afef25e7e8f6f848.svg" alt="Microsoft Active Directory Logo"/>
</p>
<br />

<h1>On-Premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial provides a comprehensive guide to the implementation of on-premises Active Directory (AD) on Azure Virtual Machines (VMs). It covers the technical aspects involved in setting up and configuring AD within an Azure VM environment, including the necessary network infrastructure, domain controller deployment, and synchronization of AD with on-premises directory services.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy On-Premises Active Directory within Azure Virtual Machines](https://youtu.be/lzHRxxSmQXc)

[![YouTube](https://static.wixstatic.com/media/2ebf04_d73739cd053d4595b1632b44d846170b~mv2.png)](https://youtu.be/lzHRxxSmQXc)
</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Active Directory Domain Services
- PowerShell ISE

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create an Azure virtual network: To set up Active Directory, you'll first need to create an Azure virtual network to which your virtual machines will be connected. You can create this virtual network using the Azure Portal.
- Create a virtual machine: You'll need to create a virtual machine that will act as the Active Directory domain controller. You can use one of the pre-built images available in the Azure Marketplace, or you can create a custom virtual machine image.
- Install Active Directory Domain Services: Once you have created the virtual machine, you will need to install Active Directory Domain Services on it. This involves adding the Active Directory Domain Services role to the server and running the necessary configuration wizards.
- Configure DNS: As part of the Active Directory setup process, you will need to configure DNS. This involves setting up a DNS server on the domain controller virtual machine and configuring your virtual network to use this DNS server.
- Join other virtual machines to the domain: Once you have set up the domain controller virtual machine and configured DNS, you can join other virtual machines to the domain. This involves changing the network settings on the virtual machines to use the DNS server you set up in step 4 and joining the virtual machines to the domain using the Active Directory Domain Services configuration.
- Configure Active Directory Group Policies: After joining the virtual machines to the domain, you can use Active Directory Group Policies to manage and configure the virtual machines.

<h2>Deployment and Configuration Steps</h2>

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_603f4353531c4e6f923ac17dad835795~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 1: Create a resource group that can be utilized on both virtual machines (VM).
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_5464c352bd08402bb7c682b246726a80~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 2: Set up the domain controller running Active Directory by creating the first virtual machine with Windows Server 2022 as the image.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_c5c8268a6fbc430a9a2d1c48701e9cdc~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 3: Create a username and password for the Windows Server virtual machine, then click on "Review + Create".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_6a90fb6b8c8a4676970fc880771c3dd8~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 4: Set up the second virtual machine with Windows 10 Pro, Version 21H2, create a username and password, then click on "Review + Create".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_54d1c0b97da64f4295263c613c908d7b~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 5: Ensure that VM2 running Windows 10 Pro is added to the same virtual network and resource group as VM1 running Windows Server, by going to the networking tab.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_abcadc2bd9a840d2bfd4c2d58fa16877~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 6: Navigate to the Azure virtual machines and select Virtual Machine 1, then click on "Networking" and choose "Network interface".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_6afd1f4b28714e52a4d435b25aa98164~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 7: Proceed to "IP Configurations" and select "ipconfig 1".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_9be41f151f394d5ca2577f7eb188e3cd~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 8: Switch the Private IP address assignment from Dynamic to Static, then select "Save".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_004b3e69435640a5ad30979a0756e40e~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 9: Use Remote Desktop Connection to connect to VM1 using its public IP address.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_0b79d63027284f9e95e7affa10c3201b~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 10: Once logged into the virtual machine, navigate to Windows Defender Firewall with Advanced Security, and click on Inbound Security Rules. Enable the following rules:
<li> Core Networking Diagnostics – ICMP Echo Request (ICMPv4-In) from <b><i>any remote address</b></i>. </li>
•	Core Networking Diagnostics – ICMP Echo Request (ICMPv4-In) from <b><i>the local subnet</b></i>.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_a4ef98e50ae54c1e92b7b4fad9f9ff70~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 11: Open Server Manager and select "Add Roles and Features."
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_48b908e3f8924632b324ece872af3497~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 12: Follow the default installation settings until you reach "Server Roles." Select "Active Directory Domain Services" and click "Next."
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_54771f89b17947e493a85f50579624c3~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 13: Continue with the default installation settings until the final page, then click "Install."
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_0836ce5db2b74e728ee07c32528c9759~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 14: Click on the flag icon in Server Manager with the yellow warning sign and select "Promote this server to a domain controller."
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_afac43aa566a45f09d21da0cbe93951c~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 15: Select "Add a new forest" and choose a domain name for the root.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_b06ff6b33d5841acabe5f406ce2a5f4c~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 16: Choose a password for Directory Services Restore Mode (DSRM).
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_600036509a034aa6a24137a63add799c~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 17: Proceed with the default installation settings and click the "Install" button.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_d608270bf12e45e580b5ba70f4fdd25d~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 18: After successfully installing Active Directory Domain Services, the remote desktop connection will automatically restart.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_50ee1cb680064114b6f8441fb758f676~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 19: To log back into the virtual machine, use Remote Desktop Connection with the domain name chosen for root followed by a backslash and the username you selected for the VM. Enter the password and click on the "Ok" button.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_01b6df7404084f40b153dfdb176ef2ed~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 20: To organize users into different categories, navigate to Tools in Server Manager and select Active Directory Users and Computers.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_d422da2a5c05422e823885caf80bb74e~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 21: Create two folders named "Employees" and "Admins" by right-clicking on the created domain, select "New", then choose "Organizational Unit" in Server Manager.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_5bbadb6c32174480b67739df0d04c60a~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 22: Navigate to the newly created "Admins" folder, then select "New" and choose "User" to create a user account. that with administrative privileges.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_43ff9a5f03bb48808993b3f2f3a08c38~mv2.png" height="50%" width="50%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 23: To give the newly created user administrative privileges, right-click on the user in the Admins folder and select Properties. Then, navigate to the "Member of" tab and click on "Add". Finally, add the user to the Domain Admins group.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_75c27af4ae794f26b4216832643916dc~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 24: After logging off, use the remote desktop connection to access the domain controller with the newly created admin user.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_2e678d71387f41089cca917b72af32ba~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 25: Return to the Azure portal on your local computer and navigate to Virtual Machine 1. Then, go to Networking and copy the NIC Private IP. Finally, update virtual machine 2's DNS to match this IP address.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_ba1e5deb73904fcda9d1a2f2cc3ae134~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 26: Navigate to the Network Interface section of virtual machine 2 in the Azure Portal.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_e9bea6246b734d9fa4ff69670f07c694~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 27: Navigate to Network Interface in the Azure Portal for virtual machine 2. Then, select DNS Servers and choose "Custom" to update the DNS Server settings with virtual machine 1's Private IP. Finally, click on "Save" to save the changes.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_dfee12c4b27e422891420c5f833c1792~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 28: Use the selected username and password during the initial setup of the Windows 10 virtual machine to re-establish a Remote Desktop Connection.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_305d1d2278f340e5acf5ae8a296d60dc~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 29: Right-click the Windows logo located in the bottom left corner of the screen, select "System", then "About", and click on "Rename this PC (advanced)" followed by "Change".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_451df308c0194308a87da5f185e707d5~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 30: Next, click on "Domain" under the "Member of" section and enter the domain name that was previously chosen for root, click "OK", and provide the username and password of the admin user.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_6ee318e0728d48588f91c1985c1265c5~mv2.png" height="30%" width="30%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 31: In the event that the joining of VM2 to the domain controller VM1 is successful, a welcome message should be received.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_ba46d5b15472496296db24bce708108a~mv2.png" height="30%" width="30%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 32: After successfully joining the domain controller, a machine restart will be initiated to apply the changes.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_9b2dbe93bd224bc8a00e127bbb5f8e26~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 33: To proceed, remotely connect back to VM2 using the admin user credentials, then navigate to "System", go to "About", followed by "Remote Desktop", and click on “Select users who have remote access to this PC".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_6fe1be950a75430f8eb9decc3bb7a31e~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_4710dd3f58c04c5dabf210b6ae01f744~mv2.png" height="40%" width="40%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 34: Subsequently, click on "Add", enter "Domain Users", and click "OK" to grant access to <b><i>all</b></i> user accounts created in Active Directory to the domain controller.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_c7a095899b6143f49cc2ee6cbfca82ca~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 35: Launch Windows PowerShell ISE with administrator privileges to create additional user accounts.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_2319dc164f87456e81c52ff601d33804~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 36: Copy and paste the code provided in the "Text Document" uploaded to this tutorial into PowerShell ISE.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_582629d2c89e483f8dce9d15e0cab5e6~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 37: Open PowerShell ISE, create a new script, paste the provided code, and click the green "run script" button.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_286eff84d6f94de394014660d796c31b~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 38 – If the aforementioned steps were executed correctly, user accounts should start to generate within PowerShell.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_ba261af7adb046af8532b76ff3a88781~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 39: Launch Active Directory Users and Computers in Server Manager and observe the various accounts populating in the Employees folder.
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_3dd04031bb534bd6b526152a907a30e1~mv2.png" height="80%" width="80%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 40: Select a user account at random and try to log into virtual machine 2 using the default password assigned to all user accounts, which is "Password1".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_d78f58f24a0849af83920875e19bbb91~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_61d6255d81ee411e93fde25cd355a124~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 41: Once a user account on Active Directory is successfully logged in, this lab will conclude. In addition, several other account options are available, including the capability to unlock "locked" user accounts due to failed password attempts, reset passwords, disable accounts, and more.
</p>
<br />

<p align="center"><b><i>🙌💥Hard work beats talent when talent doesn't work hard. ~ Tim Notke🙌💥</b></i></p>
</p>
<br />

<p align="right"> Next: <a href="https://github.com/stevenmnocent/dns-management"
>DNS Management of A-Records, CNMAE Records and Local DNS Cache</a></p>
