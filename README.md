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
- Install Active Directory
- Set up Active Directory
- Set up Server VM as Domain Controller
- Set up Remote Desktop access for all non-admin users

<h2>Deployment and Configuration Steps</h2>

<p>
- Step 1:
</p>

<p>
We will be using virtual machines in Azure in order to carry out this project. We need to create two virtual machines within the same Resource Group and Virtual Network.
</p>

<p>
The first virtual machine will be a Windows Server 2022, which we will use to install Active Directory and eventually we will designate it as a Domain Controller for the Windows VM (Client). When selecting the Size, we need at least 2 CPUs to be able to deploy this system efficiently. 
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
In order to ensure connectivity between both virtual machines, we need to change our inbound rules for the Server VM to allow inbound icmp.
</p>

<p>
- Step 2:
</p>

<p>
We have created the Virtual Machine that will be our Domain Controller. Now we will create a Windows 10 VM that we will use as our Client accessing that Domain Controller. Make sure that it is within the same Virtual Network as the Server machine. 
</p>

<p>
For this step, we need to connect to our Server VM. Start Menu → wf.smc for the Firewall settings.
</p>

<p>
Inboud Rules, sort by Protocol, and enable rules: Core Networking Diagnosis-ICMP Echo Request (there are 2).
</p>


<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/34276f19-8b56-47ef-bd15-1665a30155c0"/>
</p>

<p>
- Step 3:
</p>

<p>
In this step we will install Direct Directory in our Windows Server Virtual Machine.
</p>
<p>
The first step is to go to Server Manager and select Add Roles and Features.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/70a2a576-645f-4d3c-aa73-340291efaad0"/>
</p>

<p>
In the installation wizard, click Next, for Installation Type, select Role-Based or Feature-Based Installation.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/abdf9f70-b1de-44e5-81f2-8e5be7b48ee0)"/>
</p>

<p>
On Server Roles, check Active Directory Domain Services, and on the next window click on Add Features.
</p

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/eaa51de2-f520-464b-900e-8965c9f1f8a8)"/>
</p>


<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/1baa96e1-b474-4b8d-b427-291a54f9a8ef"/>
</p>

<p>
Go back to Server Manager and on the top right corner, click on the Warning Sign, and click on Promote this Server to a Domain Controller.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/b49378a3-37a4-4975-94f1-120b6a6bb623"/>
</p>

<p>
On Deployment Configuration, check Add a New Forest, and enter your domain name. I chose a random name for this tutorial: mydomain.com.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/403331aa-43c8-4dd5-bfbf-db0638c9da5c"/>
</p>

<p>
On the next step, select a password for your domain.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/112e6739-3732-453c-aafd-8700b0469589"/>
</p>

<p>
After the setup has been completed, your Virtual Machine will automatically log out. 
</p>


<p>
- Step 4:
</p>

<p>
In this step we will create a couple of Organizational Units inside our Active Directory, and will create an Admin user to be able to manage our new system efficiently.
</p>
<br />

<p>
First, we'll type Active Directory Users and Computers in the Start Menu of our Server VM. There, right-click on the domain name, in my case it's mydomain.com, then New → Organizational Unit. 
</p>
<p>
This is a way to create categories or groups of users within the organization for which an Active Directory has been created. This allows admins to assign permissions or access to files to entire groups or subgroups of users within the organization. For the purposes of illustration in this tutorial I have created two organizational units, one named "_EMPLOYEES," and one named "_ADMINS."
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/841f9482-478a-4191-9a80-9f53583dfde6"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/c27e671b-7fff-4aa3-8bf9-512ade67cec7"/>
</p>

<p>
Next, we will create a user and make her an admin. We will create this new admin user inside the _ADMINS Organizational Unit. Right-click on _ADMINS → New → User. Then, enter the name and username for that new user, and pick a Password on the next step.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/dcc393bc-b112-49fb-8394-426d836c59ac"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/2e513842-f443-4528-99b1-b36a1651a69c"/> 
</p>

<p>
Now, even though I have created Jane Doe inside the _ADMINS folder, she does not have any permissions or access assigned to her yet because I have not assigned any to the folder itself. So, now, inside the _ADMINS folder, right-click on Jane Doe's name → Properties → Member Of tab → Add... Then type "Domain Admins", then Check Name, and Add.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/92f397d1-1302-41d2-be7b-5955d1f94d42)"/> 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/a3308d33-8cca-4e4d-8095-2cad715f2ffd"/> 
</p><br />
  
<p>
- Step 5:
</p>

<p>
This next step involves setting up our Server VM as the Domain Controller for our Client VM (Windows 10 VM). In order to achieve this, we need to set the Client Window's 10 VM DNS settings to the Server's IP Address. Right now, the Client is connected to the Virtual Net's DNS server, but after this step, the Client's DNS server will be our other Virtual Machine with the Active Directory installed.
</p>
<p>
The first step involved is to go to the Azure portal and copy the Private IP Address of the VM that is hosting our Active Directory. Go to Networking, then copy the NIC Private IP address.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/4eb7b19a-176b-487a-9b14-9b44f0de0265"/> 
</p>

<p>
Next, we will click on the Client VM on Azure, go to Networking, then click on the Network Interface value.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/4c81b891-f09f-423f-9373-23b8176e78b3"/> 
</p>

<p>
On the right menu, click on DNS Servers, then Custome, and enter the Server VM's Private IP Address. *Make sure that there are no spaces before the first number of the IP Address. Afterwards, restart the Client VM from Azure.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/81a83630-4fc7-43f0-bc3d-dc36a12593d2"/>
</p>

<p>
The last step to join our Client VM to be part of the Domain of our newly configured Domain Controller. For this part, we need to connect remotely to our Client VM, then Control Panel → Settings → System → About → Rename this PC (Advanced) → Change... Then enter the domain name you chose for your Domain Controller earlier in the setup. 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/6cff592c-9019-44b0-a02c-abb5f569baf8)"/> 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/442c04e6-49b5-4fa8-9c8b-7d094881117c"/> 
</p>

<p>
RESTART YOUR VIRTUAL MACHINE
</p>

<p>
- Step 6:
</p>
<p>
After we reboot our Client VM, we will log back in, but this time with our admin credentials. In my case, I created the admin user jane.doe, so I will use her credentials.
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/375d6f84-832d-46ff-82d8-00eea6aa23f7"/> 
</p>

<p>
Because we want all users that are not admins to be able to access this computer using their credentials, we will allow access to all Domain users:
</p>
<p>
Control Panel → System → Remote Desktop → Select Users that can remotely access this PC → Add → type in "Domain Users" → Check Name → OK

  
<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/8480f762-c7e0-485a-95f9-259bbff27618"/> 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/1eaa989f-694e-43ab-a2d6-c4bb147f6834"/> 
</p>

<p>
<img src="https://github.com/mariamcpherson/activedirectory/assets/139581822/26e4069c-3d53-447a-b817-7aafd5f1ac68)"/> 
</p>

<p>
Now, every user inside the Domain Users folder will have access to the Client VM.
</p>
<br />


