![](https://i.imgur.com/6izzNyT.png)  

Enumerate the machine and find potential privilege escalation paths to gain Admin powers!

Answer the questions below

| Question                                                                                           | Answer      | SS                                   |
| -------------------------------------------------------------------------------------------------- | ----------- | ------------------------------------ |
| Woohoo! We've gained a foothold into our victim machine! What's the name of the shell we have now? | meterpreter | ![[Pasted image 20240312201315.png]] |


| Question                                                                                                                                                                                    | Answer | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| What user was running that Icecast process? The commands used in this question and the next few are taken directly from the '[Metasploit](https://tryhackme.com/module/metasploit)' module. | Dark   | ![[Pasted image 20240312201442.png]] |
```
getuid
```


| Question                             | Answer | SS                                   |
| ------------------------------------ | ------ | ------------------------------------ |
| What build of Windows is the system? | 7601   | ![[Pasted image 20240312201607.png]] |


| Question                                                                                                                                                                           | Answer | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Now that we know some of the finer details of the system we are working with, let's start escalating our privileges. First, what is the architecture of the process we're running? | x64    | ![[Pasted image 20240312201832.png]] |


| Question                                                                                                                                                                                                                                                                                                            | Answer           | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Now that we know the architecture of the process, let's perform some further recon. While this doesn't work the best on x64 machines, let's now run the following command `run post/multi/recon/local_exploit_suggester`. *This can appear to hang as it tests exploits and might take several minutes to complete* | No answer needed | ![[Pasted image 20240312202206.png]] |
```
run post/multi/recon/local_exploit_suggester
```


| Question                                                                                                                                                                              | Answer                                   | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ------------------------------------ |
| Running the local exploit suggester will return quite a few results for potential escalation exploits. What is the full path (starting with exploit/) for the first returned exploit? | exploit/windows/local/bypassuac_eventvwr | ![[Pasted image 20240312202332.png]] |


| Question                                                                                                                                                                                                                                                                                                                                      | Answer           | SS                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Now that we have an exploit in mind for elevating our privileges, let's background our current session using the command `background` or `CTRL + z`. Take note of what session number we have, this will likely be 1 in this case. We can list all of our active sessions using the command `sessions` when outside of the meterpreter shell. | No answer needed | ![[Pasted image 20240312202807.png]] |


| Question                                                                                                     | Answer           | SS                                   |
| ------------------------------------------------------------------------------------------------------------ | ---------------- | ------------------------------------ |
| Go ahead and select our previously found local exploit for use using the command `use FULL_PATH_FOR_EXPLOIT` | No answer needed | ![[Pasted image 20240312203024.png]] |
```
use exploit/windows/local/bypassuac_eventvwr
```


| Question                                                                                                                                                               | Answer           | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Local exploits require a session to be selected (something we can verify with the command `show options`), set this now using the command `set session SESSION_NUMBER` | No answer needed | ![[Pasted image 20240312203219.png]] |


| Question                                                                                                                                                                                   | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| Now that we've set our session number, further options will be revealed in the options menu. We'll have to set one more as our listener IP isn't correct. What is the name of this option? | LHOST  |

| Question                                                                                                  | Answer           | SS                                   |
| --------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Set this option now. You might have to check your IP on the TryHackMe network using the command `ip addr` | No answer needed | ![[Pasted image 20240312203608.png]] |
```
set LHOST tun0
```


| Question                                                                                                                                                                                                                                                | Answer           | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| After we've set this last option, we can now run our privilege escalation exploit. Run this now using the command `run`. Note, this might take a few attempts and you may need to relaunch the box and exploit the service in the case that this fails. | No answer needed | ![[Pasted image 20240312203807.png]] |


| Question                                                                                                                                        | Answer           | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Following completion of the privilege escalation a new session will be opened. Interact with it now using the command `sessions SESSION_NUMBER` | No answer needed | ![[Pasted image 20240312204031.png]] |


| Question                                                                                                                                       | Answer                   | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ | ------------------------------------ |
| We can now verify that we have expanded permissions using the command `getprivs`. What permission listed allows us to take ownership of files? | SeTakeOwnershipPrivilege | ![[Pasted image 20240312204151.png]] |
