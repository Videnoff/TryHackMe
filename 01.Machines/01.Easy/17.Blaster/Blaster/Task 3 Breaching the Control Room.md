Now that we've gained access to our target system, let's see if we can find a way to escalate. To start, let's scout around the system to see if we can find anything of interest.

  
  
![](https://i.imgur.com/V9vvTIY.jpg)

Answer the questions below

| Question                                                                                                                                                                                             | Answer        | SS  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | --- |
| When enumerating a machine, it's often useful to look at what the user was last doing. Look around the machine and see if you can find the CVE which was researched on this server. What CVE was it? | CVE-2019-1388 |     |


| Question                                                                                                                                                                               | Answer | SS                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Looks like an executable file is necessary for exploitation of this vulnerability and the user didn't really clean up very well after testing it. What is the name of this executable? | hhupd  | ![[Pasted image 20240314205305.png]] |


| Question                                                                                   | Answer           | SS  |
| ------------------------------------------------------------------------------------------ | ---------------- | --- |
| Research vulnerability and how to exploit it. Exploit it now to gain an elevated terminal! | No answer needed |     |

*Right click the HHUPD.EXE file and Run as administrator. In the UAC dialog box click on Show more Details:*

![[Pasted image 20240314222206.png]]

![[Pasted image 20240314222507.png]]

*Click Show information about the publisher’s certificate*

![[Pasted image 20240314222637.png]]

*Click VeriSign Commercial Software Publishers CA, Ok and No.*

![[Pasted image 20240314222820.png]]

*A browser is now launched as System with a 404 Verisign website being displayed. Save the webpage by clicking on the gear, File, Save as…:*

![[Pasted image 20240314223146.png]]

*Click OK.*
![[Pasted image 20240314223325.png]]

*In the File name field, input:*
```
c:\windows\system32\*.*
```

![[Pasted image 20240314223605.png]]

*Find ==cmd==, right click and hit open:*

![[Pasted image 20240314224045.png]]

*Command prompt opens as system:*

![[Pasted image 20240314224259.png]]


| Question                                                                                                            | Answer              | SS                                   |
| ------------------------------------------------------------------------------------------------------------------- | ------------------- | ------------------------------------ |
| Now that we've spawned a terminal, let's go ahead and run the command 'whoami'. What is the output of running this? | nt authority\system | ![[Pasted image 20240314224618.png]] |



| Question                                                                                                                                                                                                               | Answer                          | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | ------------------------------------ |
| Now that we've confirmed that we have an elevated prompt, read the contents of root.txt on the Administrator's desktop. What are the contents? Keep your terminal up after exploitation so we can use it in task four! | THM{COIN_OPERATED_EXPLOITATION} | ![[Pasted image 20240314224845.png]] |
