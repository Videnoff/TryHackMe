**Exploitation**

Linux VM

1. In command prompt type: **cat /home/user/myvpn.ovpn**

![[Pasted image 20240530194217.png]]


2. From the output, make note of the value of the “auth-user-pass” directive.

![[Pasted image 20240530194309.png]]


5. In command prompt type: **cat /etc/openvpn/auth.txt**

![[Pasted image 20240530230812.png]]


7. From the output, make note of the clear-text credentials.

8. In command prompt type: **cat /home/user/.irssi/config | grep -i passw**

![[Pasted image 20240530230752.png]]


9. From the output, make note of the clear-text credentials.

Answer the questions below

| Question                    | Answer      |
| --------------------------- | ----------- |
| What password did you find? | password321 |

![[Pasted image 20240530230917.png]]

| Question                                                       | Answer |
| -------------------------------------------------------------- | ------ |
| What user's credentials were exposed in the OpenVPN auth file? | user   |

![[Pasted image 20240530230959.png]]
