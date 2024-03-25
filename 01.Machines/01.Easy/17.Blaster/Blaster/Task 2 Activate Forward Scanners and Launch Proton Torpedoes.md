Now that we've launched our target, let's perform some basic enumeration of the services running on it!

  

![](https://i.imgur.com/tYPQMro.jpg)  

Answer the questions below

| Question                                      | Answer | SS                                   |
| --------------------------------------------- | ------ | ------------------------------------ |
| How many ports are open on our target system? | 2      | ![[Pasted image 20240314200630.png]] |
```
export IP=10.10.36.236
```

```
nmap -sC -sV -A -T4 -v -p- -Pn -oN scans/nmap.initial $IP
```



| Question                                                                                                | Answer             | SS                                   |
| ------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------ |
| Looks like there's a web server running, what is the title of the page we discover when browsing to it? | IIS Windows Server | ![[Pasted image 20240314200758.png]] |


| Question                                                                                                                | Answer | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Interesting, let's see if there's anything else on this web server by fuzzing it. What hidden directory do we discover? | /retro | ![[Pasted image 20240314201116.png]] |
```
gobuster dir -u http://10.10.36.236 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o scans/gobuster
```


| Question                                                                             | Answer | SS                                   |
| ------------------------------------------------------------------------------------ | ------ | ------------------------------------ |
| Navigate to our discovered hidden directory, what potential username do we discover? | Wade   | ![[Pasted image 20240314201350.png]] |


| Question                                                                                                                                 | Answer   | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------------------------------ |
| Crawling through the posts, it seems like our user has had some difficulties logging in recently. What possible password do we discover? | parzival | ![[Pasted image 20240314202300.png]] |


| Question                                                                                             | Answer               | SS                                   |
| ---------------------------------------------------------------------------------------------------- | -------------------- | ------------------------------------ |
| Log into the machine via Microsoft Remote Desktop (MSRDP) and read user.txt. What are it's contents? | THM{HACK_PLAYER_ONE} | ![[Pasted image 20240314202531.png]] |
*Using Remmina*
