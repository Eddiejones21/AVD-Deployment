# AVD-Deployment
	AVD-Deployment
 This repo serves to document my journey of deploying Azure Virtual Desktop. A couple of challenges I faced were due to permissions issues such as not being able to access the VM's I deployed.
 
 	1.  Signed into https://portal.azure.com/
	
	2. Created a User
		- Navigated to Users in the search tab
		- Created a User Principal Name
		- Created a display name
		- Created a password
		- Clicked next which took me to the Properties tab
		- Filled out the information
		- Clicked next which took me to the Assignments tab
		- Assigned a role to the user 
		- Clicked Review + Create
	
	3. Created a Resource Group 
		- Navigated to Resource Group in the search tab
		- Clicked add
		- In project details I selected "Azure Subscription 1" for my subscription
		- Created a name for the resource group (example: avd-vm-1)
		- Selected my region (example: (US) East US)
		- Clicked Review + Create
	
	4. Created a Virtual Network 
		- Navigated to Virtual Networks in the search tab
		- Clicked add
		- In project details I selected "Azure Subscription 1" 
		- Created a name for the resource group (example: avd-vm-1)
		- In the instance Details I created a "Name" and for the region I selected the same region as my resource group (example: (US) East US)
		- Clicked next which took me to the IP Addresses tab
		- Selected the default IP Address and Subnet
		- Clicked Review + Create
	
	5. Created a Host Pool
		- Navigated to Azure Virtual Desktop
		- Clicked on Create a Host Pool
		- In project details I selected "Azure Subscription 1" 
		- Created a name for the resource group (example: avd-host-pool-1)
		- Created a name for the Host Pool Name
		- For the region I selected the same region as my resource group (example: (US) East US).
		- For the Preferred app group type I selected "Desktop"
		- For the Host Pool Type I selected "Pooled" which gave me a drop-down
		- Load Balancing algorithm I chose Breadth-first and chose a Max session limit of 2 users per session host
		- Clicked next which took me to the Virtual Machines tab
		- Clicked "Yes" on Add Virtual Machines
		- Selected my resource group 
		- Created a name for the Name Prefix
		- I selected the same region as my resource group (example: (US) East US) for the virtual machine location
		- For Availability options I selected "No infrastructure redundancy required
		- I selected Standard for the security type
		- I Chose Windows 10 Enterprise Multi-Session, Version 21H1 - Gen 2
		- For Number of Virtual Machines, I chose 2 then Standard SSD for the OS Disk Type
		- For Network and Security in the drop down menu for Virtual Network I chose the Virtual Network I created
		- I chose Basic for the Network Security Group
		- Under Domain to Join I selected "Azure Active Directory" when asked to select which directory you would like to use, then clicked "No" to Enroll VM with Intune
		- Clicked Review + Create
		- Waited for my Deployment to be completed before continuing
		- Selected the Host Pool that I created (example: avd-host-pool-1)
		- Clicked on RDP Properties to set up RDP access
		- Clicked on Advanced and pasted ;targetisaadjoined:i:1 to let any applications know that this is going to be an Azure AD computer
		- Clicked save
	
	6. Created a User
		- Navigated to Users in the search tab
		- Created a User Principal Name
		- Created a display name
		- Created a password
		- Clicked next which took me to the Properties tab
		- Filled out the information
		- Clicked next which took me to the Assignments tab
		- Assigned a role to the user 
		- Clicked Review + Create
	
	7. Assigned an AD User
		- Navigated to the Host Pool
		- Clicked on the Host Pool to open up the overview
		- Clicked on Application Groups
		- Clicked on the DAG (Desktop Application Group) that was created by AD
		- On the left hand side of the window I clicked on Assignments 
		- Clicked Add
		- Added a user, then clicked select
		- Navigated to Resource Group in the search tab 
		- Selected my Resource Group
		- On the left hand side of the window I clicked on Access Control (IAM)
		- Clicked Add Role Assignment
		- In the role tab I searched for Virtual Machine User Login, selected the role, then clicked next
		- In the Members tab I selected a user, clicked select, then Review + Assign
		- Clicked on the Access Control (IAM) again 
		- Clicked Add Role Assignment
		- In the role tab I searched for Virtual Machine Administrator Login, selected the role, then clicked next
		- In the Members tab I selected a user, clicked select, then Review + Assign
	
	8. Created a Workspace
		- Navigated to Azure Virtual Desktop 
		- Clicked on Workspaces
		- Clicked create 
		- For the subscription I selected "Azure Subscription 1" 
		- For the Resource Group I selected the resource group I previously created in the drop-down options
		- In the Instance Details I created a Workspace Name (example: avd-workspace)
		- I created a Friendly name 
		- I selected the same region as my resource group (example: (US) East US) for the  location
		- Clicked Review + Create
		- Once the deployment was completed I clicked on go to resource
		- On the left hand side of the window I clicked on Application groups 
		- Clicked add
		- Selected the application group already created on the right side of the window 
	
	9.  Opened a new tab in my browser and navigated to https://rdweb.wvd.microsoft.com/arm/webclient/index.html logged in, and successfully connected to my virtual desktop![image](https://github.com/Eddiejones21/AVD-VM-	Deployment/assets/97210819/cd3d42ff-90bc-46f9-8017-e4778397fd8a)
