The large majority of home users are logged into their Windows systems as local administrators. Remember from the previous task that any user with administrator as the account type can make changes to the system.

A user doesn't need to run with high (elevated) privileges on the system to run tasks that don't require such privileges, such as surfing the Internet, working on a Word document, etc. This elevated privilege increases the risk of system compromise because it makes it easier for malware to infect the system. Consequently, since the user account can make changes to the system, the malware would run in the context of the logged-in user.

To protect the local user with such privileges, Microsoft introduced **User Account Control** (UAC). This concept was first introduced with the short-lived [Windows Vista](https://en.wikipedia.org/wiki/Windows_Vista) and continued with versions of Windows that followed.

**Note**: UAC (by default) doesn't apply for the built-in local administrator account. 

How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run. 

Let's look at the program on the account you're currently logged into, the built-in administrator account—Right-click to view its Properties.

In the Security tab, we can see the users/groups and their permissions to this file. Notice that the standard user is not listed. 

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark.png)  

Log in as the standard user and try to install this program. To do this, you can remote desktop into the machine as the standard user account. 

**Note**: You have the username and password for the standard user. It's visible in `lusrmgr.msc`.

Before installing the program, notice the icon. Do you see the difference? When you're logged in as the standard user, the shield icon is on the program's default icon. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark.png)  

This shield icon is an indicator that UAC will prompt to allow higher-level privileges to install the program.

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark2.png)  

Double-click the program, and you'll see the UAC prompt. Notice that the built-in administrator account is already set as the user name and prompts the account's password. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-uac.png)  

After some time, if a password is not entered, the UAC prompt disappears, and the program does not install. 

This feature reduces the likelihood of malware successfully compromising your system. You can read more about [UAC](https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-control-works) here.

Answer the questions below

| Question            | Answer |
| ------------------- | ------ |
| What does UAC mean? | User Account Control       |
