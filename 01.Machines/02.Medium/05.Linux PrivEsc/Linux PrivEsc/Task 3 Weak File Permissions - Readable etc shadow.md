The /etc/shadow file contains user password hashes and is usually readable only by the root user.

Note that the /etc/shadow file on the VM is world-readable:

```
ls -l /etc/shadow
```

![[Pasted image 20240219194345.png]]

View the contents of the /etc/shadow file:

```
cat /etc/shadow
```

![[Pasted image 20240219194445.png]]

Each line of the file represents a user. A user's password hash (if they have one) can be found between the first and second colons (:) of each line.

Save the root user's hash to a file called hash.txt on your Kali VM and use john the ripper to crack it. You may have to unzip /usr/share/wordlists/rockyou.txt.gz first and run the command using sudo depending on your version of Kali:

```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![[Pasted image 20240219194720.png]]

Switch to the root user, using the cracked password:

```
su root
```

![[Pasted image 20240219194858.png]]

**Remember to exit out of the root shell before continuing!**

Answer the questions below

| Question                               | Answer |
| -------------------------------------- | ------ |
| What is the root user's password hash? | $6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0<br>       |
| What hashing algorithm was used to produce the root user's password hash?                                         | sha512crypt       |
| What is the root user's password?                                       | password123       |
