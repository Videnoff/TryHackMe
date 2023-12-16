By now you have a fairly good understanding of the main privilege escalation vectors on Linux and this challenge should be fairly easy.

You have gained SSH access to a large scientific facility. Try to elevate your privileges until you are Root.  
We designed this room to help you build a thorough methodology for Linux privilege escalation that will be very useful in exams such as OSCP and your penetration testing engagements.

Leave no privilege escalation vector unexplored, privilege escalation is often more an art than a science.

You can access the target machine over your browser or use the SSH credentials below.

- Username: leonard
- Password: Penny123

Answer the questions below

| Question                                   | Answer             |
| ------------------------------------------ | ------------------ |
| What is the content of the flag1.txt file? | THM-42828719920544 | 

Search for binaries, that have SUID bit set:

```
find / -type f -perm -04000 -ls 2>/dev/null
```

![[Pasted image 20231217002629.png]]

We will use `base64`.

![[Pasted image 20231217003928.png]]


`ls`:

![[Pasted image 20231217004614.png]]

Use LFILE to esacalate privileges:

![[Pasted image 20231217005129.png]]
![[Pasted image 20231217005228.png]]
![[Pasted image 20231217005300.png]]

Crack missy's password:

![[Pasted image 20231217005519.png]]

And find the flag:

![[Pasted image 20231217005712.png]]


| Question                                   | Answer              |
| ------------------------------------------ | ------------------- |
| What is the content of the flag2.txt file? | THM-168824782390238 | 

Set LFILE to /rootflag/flag2.txt:

![[Pasted image 20231217010302.png]]

and read the content:

![[Pasted image 20231217010328.png]]
