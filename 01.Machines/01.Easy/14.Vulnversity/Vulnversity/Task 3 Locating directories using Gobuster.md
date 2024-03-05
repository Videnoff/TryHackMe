Using a fast directory discovery tool called `Gobuster`, you will locate a directory to which you can use to upload a shell.  

Answer the questions below

Let's first start by scanning the website to find any hidden directories. To do this, we're going to use Gobuster.

![](https://i.imgur.com/gODlTeh.png)


Gobuster is a tool used to brute-force URIs (directories and files), DNS subdomains, and virtual host names. For this machine, we will focus on using it to brute-force directories.

Download Gobuster [here](https://github.com/OJ/gobuster), or if you're on Kali Linux run sudo apt-get install gobuster

To get started, you will need a wordlist for Gobuster (which will be used to quickly go through the wordlist to identify if a public directory is available. If you are using [Kali Linux](https://tryhackme.com/room/kali), you can find many wordlists under **/usr/share/wordlists**. You can also use the wordlist for directories located at **/usr/share/wordlists/dirbuster/directory-list-1.0.txt** in the AttackBox.


| **Gobuster flag** | **Description**                           |
| ----------------- | ----------------------------------------- |
| -e                | Print the full URLs in your console       |
| -u                | The target URL                            |
| -w                | Path to your wordlist                     |
| -U and -P         | Username and Password for Basic Auth      |
| -p **<x>**        | Proxy to use for requests                 |
| -c <http cookies> | Specify a cookie for simulating your auth |

Now let's run Gobuster with a wordlist using 

```
gobuster dir -u http://MACHINE_IP:3333 -w <word list location>
```

![[Pasted image 20240302123729.png]]

| Question                                                | Answer     |
| ------------------------------------------------------- | ---------- |
| What is the directory that has an upload form page?<br> | /internal/ |

![[Pasted image 20240302120815.png]]
