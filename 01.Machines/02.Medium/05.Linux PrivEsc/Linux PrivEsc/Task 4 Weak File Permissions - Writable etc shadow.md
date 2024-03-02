The /etc/shadow file contains user password hashes and is usually readable only by the root user.

Note that the /etc/shadow file on the VM is world-writable:

```
ls -l /etc/shadow
```

![[Pasted image 20240219195800.png]]

Generate a new password hash with a password of your choice:

```
mkpasswd -m sha-512 newpasswordhere
```  

![[Pasted image 20240219195912.png]]

Edit the /etc/shadow file and replace the original root user's password hash with the one you just generated.

![[Pasted image 20240219200148.png]]

Switch to the root user, using the new password:

```
su root
```  

![[Pasted image 20240219200226.png]]

Remember to exit out of the root shell before continuing!

Answer the questions below

Read and follow along with the above.
