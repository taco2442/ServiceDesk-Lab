## Introduction
In this Lab, I will be going over how to set up a Service Desk environment to allow users to get hand on experience. We will go over the set up portion of how we can have two VM's (Domain Controller and ClienPC) in Virtual box. We will also explore Active Directory in creating a better hierarchy for a new company and managing the new users associated with that. 
<br>After the lab is over you will having some knowledge in the following: </br>
* Virtual box
* Active Directory - Adding/Deleting Users, Password Resets, Group Policy
* Configuring a Domain Controller
* Windows server 2016
* Networking and DNS

## Setup
For this lab you will need to download and install the latest version of Virtual box
![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/e980f7d0-d4df-489e-a24f-6bbed87f2b89)
<br>I will be using the Windows option but any one you pick will be fine</br>
<br>We will also need the ISO's for Windows 10 and Windows 2016</br>
Links:
- Windows server 2016 ISO https://go.microsoft.com/fwlink/p/?LinkID=2195174&clcid=0x409&culture=en-us&country=US
- Windows 10 ISO https://go.microsoft.com/fwlink/?LinkId=691209

<br>Once you download the MediaCreationTool and run it you will be prompted with: </br>
![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/94c1a4d8-f70b-4465-800f-1a03d63e1e78)

<br>Click on create ISO and save both to a folder so you can easily access them.</br>

## Virtual Box
We can now create the Virtual Machines our environment will take place in.
<br><b>Domain Controller</b></br>
* In virtual box select New. Set Name to DomainController and version to Windows 2016 (64-bit)
* It is important to leave the ISO image blank as adding it now will cause errors later

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/fdba54ed-13dd-40ab-a3ca-4f91f1ada4fa)</br>

* Type an easy to remember Username and Password. There isn't as much of a need to worry about security here as this is just a lab

Hardware/Virtual Hard disk:
* For hardware and virtual hard disk these options don't matter too much as long as you are allocating enough space. If the default options are too much it is ok to downsize them. When you are done click Finish.

* Now we can right click our VM we just created and select settings. Go to storage and select the empty disk. Now we can select our Windows server 2016 ISO from the drop down on the right and hit OK.

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b1b3a6bf-3f4b-48f5-8c6f-f7ff44183d83)</br>

<br><b>ClientPC</b></br>
<br>Follwing a similar process we can now make the ClienPC</br>
* In virtual box select New. Set Name to ClientPC and leave ISO blank
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/8ca132e3-0c5e-4319-8b36-369c56166d84)</br>

* Follow the same steps to create an easy to remember Username/Password. Select the Hardware/Virtual Hard disk options you wish to allocate for this lab. Click Finish when done.

## Domain Controller
Running the VM DomainController will prompt you with Installation options
<br>Follow the options:</br>
* Install Now
* Windows Server 2016 Standard Evaluation (Desktop Experience)
* Custom Install
* After Install has finished you can choose a password for your administrator account

Server Manager should start on its own. If not you can hit the windows key and search for Server Manager.
<br>You can now go to Manage at the top left and click on Add Roles and Features.</br>
![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/f7888351-efdf-4f02-91d8-7ab01504c1d8)

* Click Next through the options until you get to Server Roles
* Select Active Directory Domain Services and then Add Features
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b1c1e02f-23e1-4cb4-8b3d-3b9c02342f80)</br>
* After that we are done with options and you can continue selecting Next until you Install
* Once finished we need to Promote this server to a domain controller. We will also need to Add a new forest and set Root domain name to ServiceDesk.com. Click Next.
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/ec17de7d-f197-4ddd-80cc-ee226143d1de)</br>
* Create a Password under Domain controller options
* For the NetBIOS domain name set it to SERVICEDESK
* Select Next until we Install (Ignore warnings for Prerequisities check)[The PC will restart]

<b>Now we are going to give the Domain Controller a static IP address</b>
<br>To do this click on the windows start button in the bottom right and type cmd</br>
* Open Command prompt
* Type ipconfig into the terminal
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/cf4f7357-3661-4999-9e6e-1fb9b9148256)</br>
Now we can take that IP address and make our Domain Controller have a static IP address
<br>To open the Control Panel use the same process as you did to open Command prompt by clicking the bottom right windows start icon and typing Control Panel</br>
* Under Network and Internet select View network status and tasks
* On the left side select Change Adapter Settings
* Open Ethernet
* Open Properties
* Open Internet Protocol Version 4(TCP/IPv4)
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/3e823ceb-18de-46ed-a63d-94a6d3a86d43)</br>
<br>We can easily plug in the information we got from using ipconfig</br>

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/9edbc8c6-6c90-479e-b038-f971c6b8524e)</br>
* click OK and close

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/895c5477-0f6d-456e-b415-b820ed2bdd7c)</br>
* At the top of the VM under Devices, Under Network, Click network settings
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/0ac1bf57-c85e-4989-977f-98a55b4ad40b)</br>
* Changed Attached to: Host-only Adapter


## Client PC
Once started you will be prompted with the VM failed to boot (this is fine)
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/84b9e443-6171-41d3-b134-7ec0300e6bcd)</br>
We need to open the drop down menu and select Windows 10 ISO

<br>Running the VM ClientPC will prompt you with Installation options</br>
<br>Follow the options:</br>
* Install Now
* I don't have a product key
* Windows 10 Pro
* Accept and Next
* Custom Install and Next

<br>Now we are in the personalization stage of setting up windows</br>
<br>For these options we can keep them as default by selecting Yes, Next or Skip</br>
* Choose the name you want the PC to have and skip setting a password
* Finish last personalization steps of setting up windows (this won't affect you later in the lab)

<br><b>Before we can change anything or add ourselves to the Domain Controller we must make ourselves an administrator of the ClientPC</b></br>
<br>To do this: </br>
* Open File explorer and right click This PC, In the drop down select Manage
* In Computer Management Select Local Users and Groups
* Open Users, right click administrators and select propteries
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/a8d81fa2-2d13-4f0a-86dd-b286013e71b3)</br>
* Check Account is disabled and Apply

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/738f1c63-cfdb-4fd6-8702-198e6ac0c30a)</br>
Now the account has been enabled
* now we can right click Administrator and Set password
* Afterwards sign out of the VM and log in as the new administrator account


<br><b>Now we will Change the Name, Domain and IP address of the ClientPC</b></br>
First you will need to change your IP address
* Open Control Panel
* Under Network and Internet select View network status and tasks
* On the left side select Change Adapter Settings
* Open Ethernet
* Open Properties
* Open Internet Protocol Version 4(TCP/IPv4)
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/ce4ec0b5-c1e3-45d9-a447-16e46a72e6e4)</br>
<br>Now both our Domain Controller and ClientPC have static IP addresses and we are almost ready to communicate between them</br>

* At the top of the VM select Devices, Network, Network settings
* Once Open we can switch to Attached to: Host-only Adapter
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b579411e-9da5-49fa-83af-2d69ad4b3798)</br>

* Open File explorer, Right click on This PC and select Properties
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/4daa5ae2-5ada-4351-9102-389de3b364fd)</br>
* Scroll down to Rename this PC (advanced)
* Under To rename this computer... select Change
* Select Domain: ServiceDesk.com

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/614bff1f-5a7a-4274-a646-12e7d4e4cdbb)</br>
* enter the username and password you created for the admin account

<br>Now you should be able to see your desktop under Computers in your Domain Controller</br>
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/cde2a6e5-df5e-4e47-a5f0-7b03e85ae5fc)</br>

Congratulations you made it through setting up the environment. Now you can access your Domain Controller from a seperate VM. In the next section we will go over Active Directory and how we can start dealing with user passwords, Group/Role policy and other problems one might face in a help desk environment. 

## Active Directory
<b>Reformatting a office</b>
<br>Suppose we have a newer organization that we need to set up in Active Directory. This means that we will need to do a lot of overhead work to make sure that all new users have been added with the right group policy added accordingly. We might also encounter scenarios in this setting that would require us to change usernames because of name changes, disable/delete accounts of users that have left the company and change where people might be situated within the company. There is a lot to do in Active Directory and we will now be going over some of the problems that one might face.</br>
<br>We will be going over: </br>
* Account Lockouts/Password Reset
* Group Policy
* Assinging users to new Organizational Units
* Account Disable/Deletion
* Username Changes

<b>New Organizational Units</b>
<br>People will be promoted, demoted or need access to different resources and we will need to know how to accomplish this task.</br>
<br>First we must make 3 new Organizational Units to put our new users into.</br>
* Right click the domain, under New, Add Organizational Unit

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b9c174ed-60da-48a3-a6b8-483813362a7b)</br>
We are going to name these new OU: HR, IT, ADMINISTRATOR. This will give us a better idea of how to section our staff.

<br><b>Account Creation</b></br>
<br>We need to create the accounts we will be applying these changes to.</br>
* Right click Guest and select Copy

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/105aed01-b05d-42d2-b583-01f55414fbcd)</br>
* Choose the name and password you want for the new user accounts
Ex.

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/7d7a5428-0df8-47fa-8dd2-5ef1d1b7a3b5)</br>
* Create 5 new user accounts
* Right click the user accounts select move. HR will contain 1, IT will contain 2, Users will contain 2
* Right click Administrator in Users and select Copy, After creation right click to select move and place the new account into the OU ADMINISTRATOR

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/bc7bf7da-bcbf-4698-8589-951be0442109)</br>
<br>Now even though most of the accounts only have basic user permissions we are much more equiped and organized to manage these accounts.</br>

<b>Group Policy</b>
<br>We will go over how to create new Group and Roles for better cybersecurity health.</br>
* In Server Manager right click tools, select Group Policy Management

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/43a19e47-a4fb-4da6-8519-e4ccb6aca6a8)</br>
* Go to Default Domain Policy

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/5fadd529-cbe9-44e7-b1eb-3383f761277a)</br>
* Right click Default Domain Policy, Select Edit
* Navigate down to Account Lockout Policies. Computer Configuration, Windows Settings, Security Settings, Account Policies, Lockout Policy

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b77ee045-ae34-4fa9-83fc-9368e984c1e0)</br>
Now we are in the area where we can change account lockout settings
* Open Lockout threshold and change the attempts to 5

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/996ff2da-391c-4580-8fde-e79723349480)</br>
The other options will automatically change to 30 min lockout duration.
<br>Now we have a new lockout policy to lock users out of their accounts once they have failed 5 log in attempts and set the lockout duration to 30 minutes.</br>
<br>to set up a new policy to stop HR from accessing Task Manager: </br>
* In Server Manager, Tools, Group Policy Managemnet
* Navigate to Group Policy Objects and create a new GPO called Task Manager

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/ddf15b09-eaa6-44fb-9b36-b07fb78ec53c)</br>
* Righ click Task Manager and select Edit
* Navigate to Ctrl+Alt+Del options, User Configuration/Administrative Templates/System

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/4ef16123-a56e-4a10-815d-f3d012cb6378)</br>
* Double click Remove Task Manager, select enabled and hit Apply and OK
* Drag and drop Task Manager to our HR OU

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/f24160f7-5171-421f-b667-e3d6db52b0f0)</br>
<br>Now HR has a new GPO that makes it so they can not access Task Manager on their devices</br>

<b>Account Lockouts</b>
<br>One of the most common problems is Account lockouts and having to reset passwords.</br>
* On our ClientPC you will need to lock the account through failed passwords
  
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/1aa6ba2f-014f-4bdc-a764-31681b33ebb2)</br>
* Open the OU that contains the account you locked out. For me I used an account in IT.
* Right click and select Properties
* Select Unlock Account and Apply

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/f813822b-75cb-4a6f-896e-f92ab016aa1c)</br>

<b>Reset Password</b>
* Right click User and select Reset Password
<br>Here we can change passwords as well as unlocking the users account from here</br>

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/d6a060c8-7992-4647-9420-a5c9675cd3e0)</br>
<br>This process can become more difficult as the number of users increases. A good practice to follow is using Find... and chang Directories to the desired OU if known or using the Entire Directory tab</br>

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/59352997-41e9-4b21-b048-1f524608aa29)</br>

<b>Account Disable/Deletion</b>
<br>People will eventually leave the company and we must know how to deal with their account in that scenario or have a need to disable the account.</br>
1. User is on a paid leave which will last 3 weeks and we must go and disable the account until they return.
* In the Find search option change directories to Entire Directory and search desired name
* Right click the account and select Disable Account

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/6e2d7bf6-0281-42f0-9a22-57086b88644a)</br>
2. User has been fired from the company and we must remove the account
* In the Find search option change directories to Entire Directory and search desired name
* Right click the account and select Delete

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/3224c504-1f78-45d3-a515-c62e31e92e25)</br>

<b>Username Changes</b>
<br>Sometimes you might have to change the name of a user within the company.</br>
* Right click the user and select Properties
* Here we can change name, display name and other descriptions about the person

<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/69ea1d3b-d72d-4ba2-8db9-1ed3bf48d63a)</br>

## Conclusion
<br>In this tutorial we went over many different topics in VM, AD and different policies. We covered the setup portion of how to download and install various software to have a working AD environment. In AD we went over how a possible service desk personnel can reset passwords, unlock accounts and create new users. Now that you have your own lab setup you should be able to experiment within AD however you see fit. Good Luck!</br>

<br>If you have made it through the whole tutorial congratulations. You should now have a much better understanding of Active Directory and how to set up environments in Virtual box. </br>





