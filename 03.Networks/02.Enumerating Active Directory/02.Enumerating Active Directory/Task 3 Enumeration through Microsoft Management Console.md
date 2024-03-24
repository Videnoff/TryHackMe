You should have completed the [AD Basics room](https://tryhackme.com/jr/activedirectorybasics) by now, where different AD objects were initially introduced. In this task, it will be assumed that you understand what these objects are. Connect to THMJMP1 using RDP and your provisioned credentials from Task 1 to perform this task.  

Microsoft Management Console  

In this task, we will explore our first enumeration method, which is the only method that makes use of a GUI until the very last task. We will be using the Microsoft Management Console (MMC) with the [Remote Server Administration Tools'](https://docs.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps) (RSAT) AD Snap-Ins. If you use the provided Windows VM (THMJMP1), it has already been installed for you. However, if you are using your own Windows machine, you can perform the following steps to install the Snap-Ins:

1. Press **Start**
2. Search **"Apps & Features"** and press enter
3. Click **Manage Optional Features**
4. Click **Add a feature**
5. Search for **"RSAT"**
6. Select "**RSAT: Active Directory Domain Services and Lightweight Directory Tools"** and click **Install**

You can start MMC by using the Windows Start button, searching run, and typing in MMC. If we just run MMC normally, it would not work as our computer is not domain-joined, and our local account cannot be used to authenticate to the domain.

![MMC failed start due to credentials](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/dd93acc5bf807d120eb083d2250e77ef.png)  

This is where the Runas window from the previous task comes into play. In that window, we can start MMC, which will ensure that all MMC network connections will use our injected AD credentials.  

In MMC, we can now attach the AD RSAT Snap-In:

1. Click **File** -> **Add/Remove Snap-in**
2. Select and **Add** all three Active Directory Snap-ins
3. Click through any errors and warnings  

![[Pasted image 20240307230638.png]]



![[Pasted image 20240306231758.png]]


    
4. Right-click on **Active Directory Domains and Trusts** and select **Change Forest**
5. Enter _za.tryhackme.com_ as the **Root domain** and Click **OK**
6. Right-click on **Active Directory Sites and Services** and select **Change Forest**
7. Enter _za.tryhackme.com_ as the **Root domain** and Click OK
8. Right-click on **Active Directory Users and Computers** and select **Change Domain**
9. Enter _za.tryhackme.com_ as the **Domain** and Click **OK**
10. Right-click on **Active Directory Users and Computers** in the left-hand pane  
    
11. Click on **View** -> **Advanced Features**  
    

If everything up to this point worked correctly, your MMC should now be pointed to, and authenticated against, the target Domain:

![MMC AD Snap-in](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/da8bba5a4df58baf0045d4a71db37e05.png)

We can now start enumerating information about the AD structure here.

Users and Computers

Let's take a look at the Active Directory structure. For this task, we will focus on AD Users and Computers. Expand that snap-in and expand the za domain to see the initial Organisational Unit (OU) structure:

![MMC AD Snap-in](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/a5fc9efbd6a77ee9ea72a25d7ba13240.png)

Let's take a look at the People directory. Here we see that the users are divided according to department OUs. Clicking on each of these OUs will show the users that belong to that department.

![MMC AD Snap-in](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/993c161b6d86d61bf5ecc31a0ce0fa54.png)

Clicking on any of these users will allow us to review all of their properties and attributes. We can also see what groups they are a member of:

![MMC AD Snap-in](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/659127fd61749667192a19e0fb71ad55.png)

We can also use MMC to find hosts in the environment. If we click on either Servers or Workstations, the list of domain-joined machines will be displayed.

![MMC AD Snap-in](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/9e353f21616effb4a9cca2f3e86e65ad.png)

If we had the relevant permissions, we could also use MMC to directly make changes to AD, such as changing the user's password or adding an account to a specific group. Play around with MMC to better understand the AD domain structure. Make use of the search feature to look for objects.  

Benefits

- The GUI provides an excellent method to gain a holistic view of the AD environment.
- Rapid searching of different AD objects can be performed.  
    
- It provides a direct method to view specific updates of AD objects.
- If we have sufficient privileges, we can directly update existing AD objects or add new ones.

Drawbacks

- The GUI requires RDP access to the machine where it is executed.
- Although searching for an object is fast, gathering AD wide properties or attributes cannot be performed.﻿

Answer the questions below

| Question                                              | Answer |
| ----------------------------------------------------- | ------ |
| How many Computer objects are part of the Servers OU? | 2      |

![[Pasted image 20240307231603.png]]


| Question                                                   | Answer |
| ---------------------------------------------------------- | ------ |
| How many Computer objects are part of the Workstations OU? | 1      |

![[Pasted image 20240307231710.png]]

| Question                                                                       | Answer |
| ------------------------------------------------------------------------------ | ------ |
| How many departments (Organisational Units) does this organisation consist of? |        |

![[Pasted image 20240307232120.png]]


| Question                                          | Answer |
| ------------------------------------------------- | ------ |
| How many Admin tiers does this organisation have? |        |

![[Pasted image 20240307232214.png]]


| Question                                                                                         | Answer                   |
| ------------------------------------------------------------------------------------------------ | ------------------------ |
| What is the value of the flag stored in the description attribute of the t0_tinus.green account? | THM{Enumerating.Via.MMC} |

![[Pasted image 20240307232320.png]]
