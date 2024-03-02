This room is aimed at walking you through a variety of Linux Privilege Escalation techniques. To do this, you must first deploy an intentionally vulnerable Debian VM. This VM was created by Sagi Shahar as part of his [local privilege escalation workshop](https://github.com/sagishahar/lpeworkshop) but has been updated by [Tib3rius](https://twitter.com/TibSec) as part of his [Linux Privilege Escalation for OSCP and Beyond!](https://www.udemy.com/course/linux-privilege-escalation/?referralCode=0B0B7AA1E52B4B7F4C06) course on Udemy. Full explanations of the various techniques used in this room are available there, along with demos and tips for finding privilege escalations in Linux.

**Make sure you are connected to the [TryHackMe VPN](https://tryhackme.com/access) or using the in-browser Kali instance before trying to access the Debian VM!**

SSH should be available on port 22. You can login to the "user" account using the following command:

`ssh user@MACHINE_IP`

If you see the following message: "Are you sure you want to continue connecting (yes/no)?" type **yes** and press **Enter**.

The password for the "user" account is "**password321**".

**Note:** If you get an error saying `Unable to negotiate with <IP> port 22: no matching how to key type found. Their offer: ssh-rsa, ssh-dss` this is because OpenSSH have deprecated ssh-rsa. Add `-oHostKeyAlgorithms=+ssh-rsa` to your command to connect.

```
ssh user@10.10.94.222 -oHostKeyAlgorithms=+ssh-rsa
```

![[Pasted image 20240219192817.png]]

The next tasks will walk you through different privilege escalation techniques. After each technique, you should have a root shell. **Remember to exit out of the shell and/or re-establish a session as the "user" account before starting the next task!**

Answer the questions below

| Question | Answer    |
| -------- | --- |
| Deploy the machine and login to the "user" account using SSH.         |     |

| Question                                  | Answer    |
| ----------------------------------------- | --- |
| Run the "id" command. What is the result? | uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)    |

```
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```


![[Pasted image 20240219192918.png]]
