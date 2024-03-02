Config files often contain passwords in plaintext or other reversible formats.

List the contents of the user's home directory:

`ls /home/user`

![[Pasted image 20240224095907.png]]

Note the presence of a **myvpn.ovpn** config file. View the contents of the file:

`cat /home/user/myvpn.ovpn`

![[Pasted image 20240224095947.png]]

The file should contain a reference to another location where the root user's credentials can be found. Switch to the root user, using the credentials:

![[Pasted image 20240224100224.png]]

`su root`  

![[Pasted image 20240224100256.png]]

Remember to exit out of the root shell before continuing!  

Answer the questions below

| Question                                               | Answer                |
| ------------------------------------------------------ | --------------------- |
| What file did you find the root user's credentials in? | /etc/openvpn/auth.txt |
