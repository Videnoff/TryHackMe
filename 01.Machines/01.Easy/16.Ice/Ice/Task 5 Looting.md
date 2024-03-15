![](https://i.imgur.com/1kmEdf6.png)  

Learn how to gather additional credentials and crack the saved hashes on the machine.

Answer the questions below

| Question                                                                                                                                                                                                                                                                                                                                                                                    | Answer           | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Prior to further action, we need to move to a process that actually has the permissions that we need to interact with the lsass service, the service responsible for authentication within Windows. First, let's list the processes using the command `ps`. Note, we can see processes being run by NT AUTHORITY\SYSTEM as we have escalated permissions (even though our process doesn't). | No answer needed | ![[Pasted image 20240312220224.png]] |



| Question                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Answer      | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------------------------------ |
| In order to interact with lsass we need to be 'living in' a process that is the same architecture as the lsass service (x64 in the case of this machine) and a process that has the same permissions as lsass. The printer spool service happens to meet our needs perfectly for this and it'll restart if we crash it! What's the name of the printer service?<br>Mentioned within this question is the term 'living in' a process. Often when we take over a running program we ultimately load another shared library into the program (a dll) which includes our malicious code. From this, we can spawn a new thread that hosts our shell. | spoolsv.exe | ![[Pasted image 20240312220444.png]] |



| Question                                                               | Answer           | SS                                   |
| ---------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Migrate to this process now with the command `migrate -N PROCESS_NAME` | No answer needed | ![[Pasted image 20240312220850.png]] |
```
migrate -N spoolsv.exe
```


| Question                                                                         | Answer              | SS                                   |
| -------------------------------------------------------------------------------- | ------------------- | ------------------------------------ |
| Let's check what user we are now with the command `getuid`. What user is listed? | NT AUTHORITY\SYSTEM | ![[Pasted image 20240312220958.png]] |


| Question                                                                                                                                                                                                                                                          | Answer           | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Now that we've made our way to full administrator permissions we'll set our sights on looting. Mimikatz is a rather infamous password dumping tool that is incredibly useful. Load it now using the command `load kiwi` (Kiwi is the updated version of Mimikatz) | No answer needed | ![[Pasted image 20240312221220.png]] |


| Question                                                                                                                                                 | Answer           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Loading kiwi into our meterpreter session will expand our help menu, take a look at the newly added section of the help menu now via the command `help`. | No answer needed |


| Question                                             | Answer    | SS                                   |
| ---------------------------------------------------- | --------- | ------------------------------------ |
| Which command allows up to retrieve all credentials? | creds_all | ![[Pasted image 20240312221741.png]] |


| Question                                                                                                                                                                                                                                                                                                                                                                                               | Answer      | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- | ------------------------------------ |
| Run this command now. What is Dark's password? Mimikatz allows us to steal this password out of memory even without the user 'Dark' logged in as there is a scheduled task that runs the Icecast as the user 'Dark'. It also helps that Windows Defender isn't running on the box ;) (Take a look again at the ps list, this box isn't in the best shape with both the firewall and defender disabled) | Password01! | ![[Pasted image 20240312221859.png]] |
