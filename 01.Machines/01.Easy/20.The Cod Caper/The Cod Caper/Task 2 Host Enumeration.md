The first step is to see what ports and services are running on the target machine.

Recommended Tool - nmap:  

Useful flags:  

| -p  | Used to specify which port to analyze, can also be used to specify a range of ports i.e `-p 1-1000` |
| --- | --------------------------------------------------------------------------------------------------- |
| -sC | Runs default scripts on the port, useful for doing basic analysis on the service running on a port  |
| -A  | Aggressive mode, go all out and try to get as much information as possible                          |

Answer the questions below

| Question                                       | Answer | SS                                   |
| ---------------------------------------------- | ------ | ------------------------------------ |
| How many ports are open on the target machine? | 2      | ![[Pasted image 20240324215355.png]] |
```
export IP=10.10.210.201
```

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap $IP
```


| Question                                  | Answer                                | SS                                   |
| ----------------------------------------- | ------------------------------------- | ------------------------------------ |
| What is the http-title of the web server? | Apache2 Ubuntu Default Page: It works | ![[Pasted image 20240324215324.png]] |


| Question                         | Answer                          | SS                                   |
| -------------------------------- | ------------------------------- | ------------------------------------ |
| What version is the ssh service? | OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 | ![[Pasted image 20240324215522.png]] |


| Question                               | Answer        | SS                                   |
| -------------------------------------- | ------------- | ------------------------------------ |
| What is the version of the web server? | Apache/2.4.18 | ![[Pasted image 20240324215629.png]] |
