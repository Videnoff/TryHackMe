Root the box! Designed and created by [DarkStar7471](https://tryhackme.com/p/DarkStar7471), built by [Paradox](https://tryhackme.com/p/Paradox).

----------------------------------------------------

_Enjoy the room! For future rooms and write-ups, follow [@darkstar7471](https://twitter.com/darkstar7471) on Twitter._

Answer the questions below


```
export IP=10.10.3.187
```

```
nmap -sC -sV -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240604104610.png]]


![[Pasted image 20240604104629.png]]


```
gobuster dir --url $IP --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -o scans/gobuster.txt
```

![[Pasted image 20240604104719.png]]


![[Pasted image 20240604104856.png]]


![[Pasted image 20240604111411.png]]


![[Pasted image 20240604113131.png]]

![[Pasted image 20240604113118.png]]

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```


![[Pasted image 20240604113413.png]]



![[Pasted image 20240604113714.png]]

```
cat database.php
```

![[Pasted image 20240604113838.png]]


![[Pasted image 20240604113956.png]]

| Question | Answer                           |
| -------- | -------------------------------- |
| User.txt | 6470e394cbf6dab6a91682cc8585059b |


| Question | Answer                           |
| -------- | -------------------------------- |
| Root.txt | b9bbcb33e11b80be759c4e844862482d |
