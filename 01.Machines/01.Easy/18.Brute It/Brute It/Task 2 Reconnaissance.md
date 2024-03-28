Before attacking, let's get information about the target  

Answer the questions below

| Question                                                        | Answer | SS                                   |
| --------------------------------------------------------------- | ------ | ------------------------------------ |
| Search for open ports using nmap.  <br>How many ports are open? | 2      | ![[Pasted image 20240315200802.png]] |
```
export IP=10.10.15.157
```
```
nmap -sC -sV -A -T4 -v -p- -Pn -oN scans/nmap.initial $IP
```


| Question                        | Answer        | SS                                   |
| ------------------------------- | ------------- | ------------------------------------ |
| What version of SSH is running? | OpenSSH 7.6p1 | ![[Pasted image 20240315200910.png]] |



| Question                           | Answer | SS                                   |
| ---------------------------------- | ------ | ------------------------------------ |
| What version of Apache is running? | 2.4.29 | ![[Pasted image 20240315200952.png]] |



| Question                             | Answer | SS                                   |
| ------------------------------------ | ------ | ------------------------------------ |
| Which Linux distribution is running? | Ubuntu | ![[Pasted image 20240315201238.png]] |
  


| Question                                                                        | Answer | SS                                   |
| ------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Search for hidden directories on web server.  <br>What is the hidden directory? | /admin | ![[Pasted image 20240315201428.png]] |
```
gobuster dir -u http://10.10.15.157 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o scans/gobuster
```
