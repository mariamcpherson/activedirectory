<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

<p>
Active Directory (AD) is a directory service developed by Microsoft and is a core component of the Windows Server operating system. It provides a centralized and standardized way to manage and organize network resources, such as users, computers, groups, and other devices, within a Windows domain network.
</p>
<p>
Active Directory plays a crucial role in managing user accounts, providing security, and simplifying administrative tasks within Windows-based networks. It is widely used in organizations of all sizes to create a centralized and efficient network environment.
</p>

<p>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.</p><br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up a Windows Server and a Windows 10 Virtual Machine in Azure
- Change inboud rules for the Windows Server Machine
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
- Step 1:
</p>

<p>
We will be using virtual machines in Azure in order to carry out this project. We need to create two virtual machines within the same Resource Group and Virtual Network.
</p>

<p>
The first virtual machine will be a Windows Server 2022, which we will use as our Domain Controller. When selecting the Size, we need at least 2 CPUs to be able to deploy this system efficiently. 
</p>
<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/8c38ee19-3041-4615-b55a-671227006bde"/>
</p>

<p>
Now, we will change the Private IP Address of this VM to Static. For this, click on the VM's name, on the left Menu click on Networking, then on the right, click on the Network Interface Value. 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/bf46f175-6df3-4968-a9f1-2423072d6008"/>
</p>

<p>
Click on IP Configurations, and you can see that the IP Address is dynamic.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/a94b8c9f-2bff-4803-86b0-0a6b623cccaa"/>
</p>

<p>
Now, click on ipconfig1, and change it to static.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/df86f66e-9eba-4c4f-af54-537673e29e3b"/>
</p>

<p>
In order to connect our Client to our Domain Controller, we need to change our inbound rules for the Domain Controller's Firewall, to allow icmp traffic from the Client.
</p>

<p>
- Step 2:
</p>

<p>
We have created the Virtual Machine that will be our Domain Controller. No we will create a Windows 10 VM that we will use as our Client accessing that Domain Controller. Make sure that it is within the same Virtual Network as the Server machine. 
</p>

<p>
For this step, we need to connect to our Server VM. Start Menu → wf.smc for the Firewall settings.
</p>

<p>
Inboud Rules, sort by Protocol, and enable rules:
</p>

<p>
Core Networking Diagnosis
</p>

<p>
ICMP Echo Request
</p>


<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
