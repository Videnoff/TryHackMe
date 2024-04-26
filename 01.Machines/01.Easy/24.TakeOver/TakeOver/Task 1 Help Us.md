Hello there,  
  
I am the CEO and one of the co-founders of futurevera.thm. In Futurevera, we believe that the future is in space. We do a lot of space research and write blogs about it. We used to help students with space questions, but we are rebuilding our support.  

Recently blackhat hackers approached us saying they could takeover and are asking us for a big ransom. Please help us to find what they can takeover.  
  
Our website is located at [https://futurevera.thm](https://futurevera.thm)

Hint: Don't forget to add the MACHINE_IP in /etc/hosts for futurevera.thm ; )

Answer the questions below

| Question                      | Answer                                |
| ----------------------------- | ------------------------------------- |
| What's the value of the flag? | lag{beea0d6edfcee06a59b83fb50ae81b2f} |

*Add futurevera.thm in /etc/hosts:*

```
echo '10.10.239.115 futurevera.thm' | sudo tee -a /etc/hosts
```

![[Pasted image 20240423191830.png]]


```
export IP=10.10.239.115
```

*Nmap scan:*

```
nmap -sC -sV -A -T4 -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240423195530.png]]



*Gobuster scan:*

```
gobuster vhost --url futurevera.thm --wordlist /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 50 --append-domain -o scans/gobuster
```

![[Pasted image 20240423200753.png]]


*Enumerate using FFuF:*

```
ffuf -u https://$IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host:FUZZ.futurevera.thm" -fs 4605
```

![[Pasted image 20240423201019.png]]



*Add to /etc/hosts:*

```
echo '10.10.239.115 portal.futurevera.thm' | sudo tee -a /etc/hosts
```
```
echo '10.10.239.115 blog.futurevera.thm' | sudo tee -a /etc/hosts
```
```
echo '10.10.239.115 payroll.futurevera.thm' | sudo tee -a /etc/hosts
```
```
echo '10.10.239.115 support.futurevera.thm' | sudo tee -a /etc/hosts
```


![[Pasted image 20240423195741.png]]


*Check the pages:*

```
https://portal.futurevera.thm
```

![[Pasted image 20240423202122.png]]



```
https://blog.futurevera.thm/
```

![[Pasted image 20240423202145.png]]


```
https://payroll.futurevera.thm/
```

![[Pasted image 20240423202230.png]]


```
https://support.futurevera.thm/
```

![[Pasted image 20240423202300.png]]


*Check the certificate:*

![[Pasted image 20240423202355.png]]


![[Pasted image 20240423202425.png]]


```
secrethelpdesk934752.support.futurevera.thm
```

*Add to /etc/hosts:*

```
echo '10.10.239.115 secrethelpdesk934752.support.futurevera.thm' | sudo tee -a /etc/hosts
```

*Open the address:*

![[Pasted image 20240423203635.png]]
