![](https://i.imgur.com/FFqM2ZK.png)  

Exploit the target vulnerable service to gain a foothold!

Answer the questions below

| Question                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Answer | SS                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Now that we've identified some interesting services running on our target machine, let's do a little bit of research into one of the weirder services identified: Icecast. Icecast, or well at least this version running on our target, is heavily flawed and has a high level vulnerability with a score of 7.5 (7.4 depending on where you view it). What is the **Impact Score** for this vulnerability? Use [https://www.cvedetails.com](https://www.cvedetails.com) for this question and the next. | 6.4    | ![[Pasted image 20240312195718.png]] |


| Question                                                                                 | Answer        | SS                                   |
| ---------------------------------------------------------------------------------------- | ------------- | ------------------------------------ |
| What is the CVE number for this vulnerability? This will be in the format: CVE-0000-0000 | CVE-2004-1561 | ![[Pasted image 20240312195812.png]] |


| Question                                                                                                                                                                                                                       | Answer           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- |
| Now that we've found our vulnerability, let's find our exploit. For this section of the room, we'll use the Metasploit module associated with this exploit. Let's go ahead and start Metasploit using the command `msfconsole` | No answer needed |


| Question                                                                                                                                                                                                                                                                                                   | Answer                              | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | ------------------------------------ |
| After Metasploit has started, let's search for our target exploit using the command 'search icecast'. What is the full path (starting with exploit) for the exploitation module? If you are not familiar with metasploit, take a look at the [Metasploit](https://tryhackme.com/module/metasploit) module. | exploit/windows/http/icecast_header | ![[Pasted image 20240312200141.png]] |


| Question                                                                                                                     | Answer           |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Let's go ahead and select this module for use. Type either the command `use icecast` or `use 0` to select our search result. | No answer needed |


| Question                                                                                                                                                                      | Answer | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Following selecting our module, we now have to check what options we have to set. Run the command `show options`. What is the only required setting which currently is blank? | RHOSTS | ![[Pasted image 20240312200436.png]] |


| Question                                                                                                                                                                                                                                                                                       | Answer           | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| First let's check that the LHOST option is set to our tun0 IP (which can be found on the [access](https://tryhackme.com/access) page). With that done, let's set that last option to our target IP. Now that we have everything ready to go, let's run our exploit using the command `exploit` | No answer needed | ![[Pasted image 20240312201206.png]] |
