As you would have already found out by now, certain users cannot access certain files or folders. We've previously explored some commands that can be used to determine what access we have and where it leads us. 

In our previous tasks, we learned how to extend the use of commands through flags and switches. Take, for example, the `ls` command, which lists the contents of the current directory. When using the `-l` switch, we can see ten columns such as in the screenshot below. However, we're only interested in the first three columns:

Using ls -lh to list the permissions of all files in the directory

![[Pasted image 20231127212718.png]]


Although intimidating, these three columns are very important in determining certain characteristics of a file or folder and whether or not we have access to it. A file or folder can have a couple of characteristics that determine both what actions are allowed and what user or group has the ability to perform the given action -- such as the following:

- Read
- Write
- Execute 

Using su to switch to user2  

![[Pasted image 20231127212740.png]]



Let's use the "cmnatic.pem" file in our initial screenshot at the top of this task. It has the "-" indicator highlighting that it is a file and then "rw" followed after. This means that only the owner of the file can read and write to this"cmnatic.pem" file but cannot execute it.

**Briefly: The Differences Between Users & Groups**

We briefly explored this in Linux fundamentals part 1 (namely, the differences between a regular user and a system user). The great thing about Linux is that permissions can be so granular, that whilst a user technically owns a file, if the permissions have been set, then a group of users can also have either the same or a different set of permissions to the exact same file without affecting the file owner itself.

Let's put this into a real-world context; the system user that runs a web server must have permissions to read and write files for an effective web application. However, companies such as web hosting companies will have to want to allow their customers to upload their own files for their website without being the webserver system user -- compromising the security of every other customer. 

We'll learn the commands necessary to switch between users below.

  

**Switching Between Users**

Switching between users on a Linux install is easy work thanks to the `su` command. Unless you are the root user (or using root permissions through sudo), then you are required to know two things to facilitate this transition of user accounts:

- The user we wish to switch to
- The user's password

The `su` command takes a couple of switches that may be of relevance to you. For example, executing a command once you log in or specifying a specific shell to use. I encourage you to read the man page for `su` to find out more. However, I will cover the `-l` or `--login` switch.

Simply, by providing the `-l` switch to `su`, we start a shell that is much more similar to the actual user logging into the system - we inherit a lot more properties of the new user, i.e., environment variables and the likes. 

Using su to switch to user2 interactively

![[Pasted image 20231127212809.png]]



For example, when using `su` to switch to "user2", our new session drops us into our previous user's home directory. 

Using su to switch to user2 interactively

![[Pasted image 20231127212835.png]]


Where now, after using `-l`, our new session has dropped us into the home directory of "user" automatically. 

Answer the questions below

| Question                                                    | Answer   |
| ----------------------------------------------------------- | -------- |
| On the deployable machine, who is the owner of "important"? | user2    |
| What would the command be to switch to the user "user2"?    | su user2 |
| Now switch to this user "user2" using the password "user2"  |          |
| Output the contents of "important", what is the flag?       | THM{SU_USER2}         |
