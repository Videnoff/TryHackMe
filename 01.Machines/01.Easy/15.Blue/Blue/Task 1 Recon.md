Scan and learn what exploit this machine is vulnerable to. Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up. **This room is not meant to be a boot2root CTF, rather, this is an educational series for complete beginners. Professionals will likely get very little out of this room beyond basic practice as the process here is meant to be beginner-focused.** 

![](https://i.imgur.com/NhZIt9S.png)

_Art by one of our members, Varg - [THM Profile](https://tryhackme.com/p/Varg) - [Instagram](https://www.instagram.com/varghalladesign/) - [Blue Merch](https://www.redbubble.com/shop/ap/53637482) - [Twitter](https://twitter.com/Vargnaar)_

  

_Link to Ice, the sequel to Blue: [Link](https://tryhackme.com/room/ice)_

_You can check out the third box in this series, Blaster, here: [Link](https://tryhackme.com/room/blaster)_

-----------------------------------------

  

The virtual machine used in this room (Blue) can be downloaded for offline usage from [https://darkstar7471.com/resources.html](https://darkstar7471.com/resources.html)[](https://darkstar7471.com/resources.html)

  

_Enjoy the room! For future rooms and write-ups, follow [@darkstar7471](https://twitter.com/darkstar7471) on Twitter._

Answer the questions below

| Question                                                                                                                                   | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| Scan the machine. (If you are unsure how to tackle this, I recommend checking out the [Nmap](https://tryhackme.com/room/furthernmap) room) |        |

```
export IP=10.10.68.62
```

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap.initial $IP
```


| Question                                               | Answer |
| ------------------------------------------------------ | ------ |
| How many ports are open with a port number under 1000? | 3      |

![[Pasted image 20240310200456.png]]


| Question                                                                            | Answer   |
| ----------------------------------------------------------------------------------- | -------- |
| What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067) | ms17-010 |
*Search for nmap smb scripts:*

```
ls -al /usr/share/nmap/scripts | grep -e "smb-"
```

![[Pasted image 20240310202211.png]]

*Google every vulnerability containing ms??-??? and find out EternalBlue *:

![[Pasted image 20240310202619.png]]