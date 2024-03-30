This task increases the difficulty. All of the answers will be in the classic [rock you](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) password list.

You might have to start using hashcat here and not online tools. It might also be handy to look at some example hashes on [hashcats page](https://hashcat.net/wiki/doku.php?id=example_hashes).

Answer the questions below

| Question                                                               | Answer | SS                                   |
| ---------------------------------------------------------------------- | ------ | ------------------------------------ |
| Hash: F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 | paule  | ![[Pasted image 20240318222601.png]] |
```
echo 'F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85' > 1.txt
```
```
hashid 1.txt
```
![[Pasted image 20240318222450.png]]
```
hashcat -a 0 -m 1400 1.txt /usr/share/wordlists/rockyou.txt
```



| Question                               | Answer       | SS                                   |
| -------------------------------------- | ------------ | ------------------------------------ |
| Hash: 1DFECA0C002AE40B8619ECF94819CC1B | n63umy8lkf4i | ![[Pasted image 20240318223155.png]] |
```
hashcat -a 0 -m 1000 2.txt /usr/share/wordlists/rockyou.txt
```



| Question                                                                                                                                     | Answer | SS  |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------ | --- |
| Hash: $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.<br><br>Salt: aReallyHardSalt | waka99 |     |



| Question                                                              | Answer       | SS  |
| --------------------------------------------------------------------- | ------------ | --- |
| Hash: e5d8870e5bdd26602cab8dbe07a942c8669e56d6<br><br>Salt: tryhackme | 481616481616 |     |
