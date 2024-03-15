![](https://i.imgur.com/7tFp450.png)  

Scan and enumerate our victim!

Answer the questions below

| Question                                                        | Answer           |
| --------------------------------------------------------------- | ---------------- |
| Deploy the machine! This may take up to three minutes to start. | No answer needed |

| Question                                                                                                                                                                                                                                                                      | Answer           |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Launch a scan against our target machine, I recommend using a SYN scan set to scan all ports on the machine. The scan command will be provided as a hint, however, it's recommended to complete the room '[Nmap](https://tryhackme.com/room/furthernmap)' prior to this room. | No asnwer needed |
```
nmap -sC -sV -sS -v -p- -oN scans/nmap.initial $IP
```

![[Pasted image 20240312191948.png]]


| Question                                                                                                                                                                                                                                                                                                                                             | Answer | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------ |
| Once the scan completes, we'll see a number of interesting ports open on this machine. As you might have guessed, the firewall has been disabled (with the service completely shutdown), leaving very little to protect this machine. One of the more interesting ports that is open is Microsoft Remote Desktop (MSRDP). What port is this open on? | 3389   | ![[Pasted image 20240312194039.png]] |


| Question                                                                             | Answer  | SS                                   |
| ------------------------------------------------------------------------------------ | ------- | ------------------------------------ |
| What service did nmap identify as running on port 8000? (First word of this service) | Icecast | ![[Pasted image 20240312194309.png]] |


| Question                                                                          | Answer  |                                      |
| --------------------------------------------------------------------------------- | ------- | ------------------------------------ |
| What does Nmap identify as the hostname of the machine? (All caps for the answer) | Dark-PC | ![[Pasted image 20240312194437.png]] |
