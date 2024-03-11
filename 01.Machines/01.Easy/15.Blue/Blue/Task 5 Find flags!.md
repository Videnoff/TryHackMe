Find the three flags planted on this machine. These are not traditional flags, rather, they're meant to represent key locations within the Windows system. Use the hints provided below to complete this room!

  

-----------------------------------------------------------------

  

_Completed Blue? Check out Ice: [Link](https://tryhackme.com/room/ice)_

_You can check out the third box in this series, Blaster, here: [Link](https://tryhackme.com/room/blaster)_

Answer the questions below

| Question                                            | Answer                   | SS                                   |
| --------------------------------------------------- | ------------------------ | ------------------------------------ |
| Flag1? _This flag can be found at the system root._ | flag{access_the_machine} | ![[Pasted image 20240311224101.png]] |




*Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen. 

| Question                                                                                   | Answer                             | SS                                                                           |
| ------------------------------------------------------------------------------------------ | ---------------------------------- | ---------------------------------------------------------------------------- |
| Flag2? _This flag can be found at the location where passwords are stored within Windows._ | flag{sam_database_elevated_access} | ![[Pasted image 20240311224659.png]]<br>![[Pasted image 20240311224707.png]] |

| Question                                                                                                                                  | Answer                                | ss                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ------------------------------------ |
| flag3? _This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved._ | flag{admin_documents_can_be_valuable} | ![[Pasted image 20240311225114.png]] |
