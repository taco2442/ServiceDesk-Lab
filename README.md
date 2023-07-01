## Introduction
In this Lab, I will be going over how to set up a Service Desk environment to allow users to get hand on experience. We will  set up two VM's in Virtual box (one for the Domain Controller and one for the clientPC) this will allow us to access the DC from a seperate PC. We will also experiment with Jira ticketing system and get familiar with tickets.
After the lab is over you will having some knowledge in the following:
* Virtual box
* Active Directory - Adding/Deleting Users, Password Resets, Group/Role Policy
* Configuring a Domain Controller
* Windows server 2016
* Jira Ticketing system

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

<br>Click on create ISO and save both to folder you can easily access them.</br>

## Virtual Box
We can now create the Virtual Machines our environment will take place in.
<br><b>Domain Controller</b></br>
* In virtual box select New. Set Name to DomainController and version to Windows 2016 (64-bit)
* It is important to leave the ISO image blank as adding it now will cause errors later

![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/fdba54ed-13dd-40ab-a3ca-4f91f1ada4fa)

* Type an easy to remember Username and Password. There isn't as much of a need to worry about security here as this is just a lab

Hardware/Virtual Hard disk:
* For hardware and virtual hard disk these options don't matter too much as long as you are allocating enough space. If the default options are too much it is ok to downsize them. When you are done click Finish.

* Now we can right click our VM we just created and select settings. Go to storage and select the empty disk. Now we can select our Windows server 2016 ISO from the drop down on the right and hit OK.
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b1b3a6bf-3f4b-48f5-8c6f-f7ff44183d83)</br>

<br><b>ClientPC</b></br>
<br>Follwing a similar process we can now make the ClienPC</br>
* In virtual box select New. Set Name to ClientPC and select the Windows 10 ISO
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/b1e417b8-c82b-4376-bb15-b8ee1b456710)</br>

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
* Once finished we need to Promote this server to a domain controller. We will also need to Add a new forest and set Root domain name to ServiceDesk.com.
<br>![image](https://github.com/taco2442/ServiceDesk-Lab/assets/58244861/ec17de7d-f197-4ddd-80cc-ee226143d1de)
</br>

## Client PC




## Active Directory
