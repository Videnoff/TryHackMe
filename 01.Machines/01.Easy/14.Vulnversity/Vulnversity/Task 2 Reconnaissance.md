Gather information about this machine using a network scanning tool called `Nmap`. Check out the [Nmap](https://tryhackme.com/room/furthernmap) room for more on this!  

Need a Linux machine with Nmap on? Deploy your own [AttackBox](https://tryhackme.com/my-machine) and control it with your browser.

Answer the questions below

Scan the box: 

```
nmap -sV {MACHINE_IP}
```

![[Pasted image 20240301184459.png]]


**![](https://i.imgur.com/gZqOO8D.png)**

Nmap is a free, open-source and powerful tool used to discover hosts and services on a computer network. In our example, we use Nmap to scan this machine to identify all services running on a particular port. Nmap has many capabilities; a table summarises some of its functionality below.

| **Nmap flag** | **Description**                                                                     |
| ------------- | ----------------------------------------------------------------------------------- |
| -sV           | Attempts to determine the version of the services running                           |
| -p <x> or -p- | Port scan for port <x> or scan all ports                                            |
| -Pn           | Disable host discovery and scan for open ports                                      |
| -A            | Enables OS and version detection, executes in-build scripts for further enumeration |
| -sC           | Scan with the default Nmap scripts                                                  |
| -v            | Verbose mode                                                                        |
| -sU           | UDP port scan                                                                       |
| -sS           | TCP SYN port scan                                                                   |

| Question                                                                                                                                                                                                                                                                                                                             | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| There are many Nmap "cheatsheets" online that you can use too.                                                                                                                                                                                                                                                                       |        |
| Scan the box; how many ports are open?                                                                                                                                                                                                                                                                                               | 6      |
| What version of the squid proxy is running on the machine?                                                                                                                                                                                                                                                                           | 3.5.12 |
| How many ports will Nmap scan if the flag **-p-400** was used?                                                                                                                                                                                                                                                                       | 400    |
| What is the most likely operating system this machine is running?                                                                                                                                                                                                                                                                    | Ubuntu |
| What port is the web server running on?                                                                                                                                                                                                                                                                                              | 3333   |
| It's essential to ensure you are always doing your reconnaissance thoroughly before progressing. Knowing all open services (which can all be points of exploitation) is very important, don't forget that ports on a higher range might be open, so constantly scan ports after 1000 (even if you leave checking in the background). |        |
| What is the flag for enabling verbose mode using Nmap?                                                                                                                                                                                                                                                                               | -v     |
