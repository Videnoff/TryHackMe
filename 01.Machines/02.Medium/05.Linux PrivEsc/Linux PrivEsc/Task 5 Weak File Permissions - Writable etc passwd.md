The /etc/passwd file contains information about user accounts. It is world-readable, but usually only writable by the root user. Historically, the /etc/passwd file contained user password hashes, and some versions of Linux will still allow password hashes to be stored there.

Note that the /etc/passwd file is world-writable:

```
ls -l /etc/passwd
```

![[Pasted image 20240219200635.png]]

Generate a new password hash with a password of your choice:

```
openssl passwd newpasswordhere
```

![[Pasted image 20240219200738.png]]

Edit the /etc/passwd file and place the generated password hash between the first and second colon (:) of the root user's row (replacing the "x").

![[Pasted image 20240219200945.png]]

Switch to the root user, using the new password:

```
su root
```

![[Pasted image 20240219201058.png]]

Alternatively, copy the root user's row and append it to the bottom of the file, changing the first instance of the word "root" to "newroot" and placing the generated password hash between the first and second colon (replacing the "x").  

![[Pasted image 20240219201335.png]]

Now switch to the newroot user, using the new password:

```
su newroot
```

![[Pasted image 20240219201406.png]]

Remember to exit out of the root shell before continuing!

Answer the questions below

| Question | Answer    |
| -------- | --- |
| Run the "id" command as the newroot user. What is the result?         | uid=0(root) gid=0(root) groups=0(root)    |

![[Pasted image 20240219201444.png]]
