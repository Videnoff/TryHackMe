If a user accidentally types their password on the command line instead of into a password prompt, it may get recorded in a history file.

View the contents of all the hidden history files in the user's home directory:

`cat ~/.*history | less`

![[Pasted image 20240224095353.png]]
![[Pasted image 20240224095431.png]]

Note that the user has tried to connect to a MySQL server at some point, using the "root" username and a password submitted via the command line. Note that there is no space between the -p option and the password!

Switch to the root user, using the password:

`su root`  

![[Pasted image 20240224095603.png]]

Remember to exit out of the root shell before continuing!  

Answer the questions below

| Question                                          | Answer                                       |
| ------------------------------------------------- | -------------------------------------------- |
| What is the full mysql command the user executed? | mysql -h somehost.local -uroot -ppassword123 |
