This room is aimed at walking you through a variety of Windows Privilege Escalation techniques. To do this, you must first deploy an intentionally vulnerable Windows VM. This VM was created by Sagi Shahar as part of his [local privilege escalation workshop](https://github.com/sagishahar/lpeworkshop) but has been updated by [Tib3rius](https://twitter.com/TibSec) as part of his [Windows Privilege Escalation for OSCP and Beyond!](https://www.udemy.com/course/windows-privilege-escalation/?referralCode=9A533B41ECB74227E574) course on Udemy. Full explanations of the various techniques used in this room are available there, along with demos and tips for finding privilege escalations in Windows.

Make sure you are connected to the [TryHackMe VPN](https://tryhackme.com/access) or using the in-browser Kali instance before trying to access the Windows VM!

RDP should be available on port 3389 (it may take a few minutes for the service to start). You can login to the "user" account using the password "password321":

`xfreerdp /u:user /p:password321 /cert:ignore /v:MACHINE_IP`  

The next tasks will walk you through different privilege escalation techniques. After each technique, you should have a admin or SYSTEM shell. Remember to exit out of the shell and/or re-establish a session as the "user" account before starting the next task!

Answer the questions below

Deploy the Windows VM and login using the "user" account.
