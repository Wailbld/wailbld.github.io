---
title: Creating an Active Directory Home Lab (Part 2)
date: 2023-06-25 12:00:00 -500
categories: [Hacking, RedTeam]
tags: [redTeam,pentesting,hacking,windows,activedirectory] # TAG names should always be lowercase
image:
  path: Windows.png
  alt:  Image By bleepingcomputer.
img_path: /assets/img/images/Part-2/
---


## Configure Active Directory Domain Services

In this post, we will configure the Active Directory services on the windows server we set up in [Part 1](https://wailbld.github.io/posts/Active-Directory-Lab-Part-1/) of this series and learn how to quickly automate the process of creating 100 domain users with created PowerShell Script, representing a small business organization plus we add our windows 10 workstation to our network.


## Active Directory Setup

We will start installing the Active Directory services and create the forest root domain called “ATTACKLAB.LOCAL”. To begin the setup process, we click on the “Add roles and features” option in the server’s dashboard to add the AD role.

![Desktop View](1-Add-Role.png){: width="500" height="300"}

Next, select the server from the Server Pool list; in our case, “DC01” and click “Next”.

![Desktop View](2-Add-Role.png){: width="500" height="300"}
![Desktop View](3-Add-Role.png){: width="500" height="300"}
![Desktop View](4-Add-Role.png){: width="500" height="300"}

In the Server Roles section, check the “Active Directory Domain Services” box and click on “Add Features” to install the additional capabilities that come with the role.

![Desktop View](5-Add-ADDS.png){: width="500" height="300"}
![Desktop View](6-Add-ADDS.png){: width="500" height="300"}

Here We need add to `Group Policy Management` Feature , so we check it .
![Desktop View](7-Add-ADDS.png){: width="500" height="300"}
![Desktop View](8-Add-ADDS.png){: width="500" height="300"}
![Desktop View](9-1-Add-ADDS.png){: width="500" height="300"}

After the installation is complete, a new notification will show for the Post-deployment Configuration to ask if we want to promote the server to a domain controller.

![Desktop View](9-Add-ADDS.png){: width="500" height="300"}

Click on it to start the Domain Controller configuration, and select `Add a new forest`; we will call the lab forest `attacklab.local”`.

![Desktop View](10-configure-domain.png){: width="500" height="300"}

> `Directory Services Restore Mode (DSRM)` is a special boot mode only available on the domain controller that allows the domain administrators to log into the domain controller using the DSRM password when the Active Directory fails. It is the local administrator account for the domain controller server.
{: .prompt-info }

![Desktop View](11-configure-domain.png){: width="500" height="300"}



For the `DNS Options`, we will leave the “Create DNS Delegation” box unchecked and click “Next”.


![Desktop View](12-configure-domain.png){: width="500" height="300"}

Verify the NetBIOS domain name is the same as the forest name; in our case, it is `ATTACKLAB`. If all is good, click “Next” to move to the “Paths” section.

![Desktop View](13-configure-domain.png){: width="500" height="300"}

> NTDS is a database that stores Active Directory data, including information about users, computers, groups, and network resource objects.
{: .prompt-info }

> SYSVOL folder is located locally on the domain controller. It consists of public files, folders such as Group Policy Objects (GPOs), and scripts used to manage the domain users and computers in the forest.
{: .prompt-info }

![Desktop View](14-configure-domain.png){: width="500" height="300"}
![Desktop View](15-configure-domain.png){: width="500" height="300"}

Now that we have configured everything we need for the Active Directory, we can see that all prequisite checks passed successfully, So we can click On  “Install” in the “Pre-requisite Check” section. The process will take a few seconds, and you will need to reboot the machine when it ends.

![Desktop View](16-configure-domain.png){: width="500" height="300"}

After the machine restarts, we can go to the server dashboard and check the newly created domain “attacklab.local”.

![Desktop View](17-configure-domain.png){: width="500" height="300"}

Now we have installed Active Directory, take a snapshot of the current state before adding domain users.

## Adding Domain Users

![Desktop View](18-configure-domain.png){: width="500" height="300"}
![Desktop View](19-add-users.png){: width="500" height="300"}
![Desktop View](20-add-users.png){: width="500" height="300"}
![Desktop View](21-add-users.png){: width="500" height="300"}
![Desktop View](22-0-add-users.png){: width="500" height="300"}
![Desktop View](22-1-add-users.png){: width="500" height="300"}
![Desktop View](22-2-add-users.png){: width="500" height="300"}
![Desktop View](22-3-add-users.png){: width="500" height="300"}


## Adding Windows 10 Workstation

![Desktop View](23-add-workstation.png){: width="500" height="300"}
![Desktop View](24-add-workstation.png){: width="500" height="300"}
![Desktop View](25-add-workstation.png){: width="500" height="300"}
![Desktop View](26-add-workstation.png){: width="500" height="300"}
![Desktop View](27-add-workstation.png){: width="500" height="300"}
![Desktop View](28-add-workstation.png){: width="500" height="300"}
![Desktop View](29-add-workstation.png){: width="500" height="300"}
![Desktop View](30-add-workstation.png){: width="500" height="300"}

