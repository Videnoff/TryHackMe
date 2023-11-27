We're continuing with Tools that are available through the System Configuration panel.  

The command prompt (`cmd`) can seem daunting at first, but it's really not that bad once you understand how to interact with it. 

In early operating systems, the command line was the sole way to interact with the operating system.

When the GUI (graphical user interface) was introduced, it allowed users to perform complex tasks with a few clicks of a button instead of entering commands in the command prompt. 

Even though the GUI is the primary way to interact with the operating system, a computer user can still interact via the command prompt. 

In this task, we'll only cover a few commands that a computer user can run in the command prompt to obtain information about the computer system.

Let's start with a few simple commands, such as `hostname` and `whoami`.

The command **hostname** will output the computer name.

![](https://assets.tryhackme.com/additional/win-fun2/hostname.png)  

The command **whoami** will output the name of the logged-in user.

![](https://assets.tryhackme.com/additional/win-fun2/whoami.png)  

Next, let's look at some commands that are useful when troubleshooting.

A command used often is `ipconfig`. This command will show the network address settings for the computer.

![](https://assets.tryhackme.com/additional/win-fun2/ipconfig.png)  

Each command will have a help manual to explain the expected syntax to execute the command properly, along with any additional parameters that can be added to the command to expand its execution.

A  command to retrieve the help manual for a command is `/?`.

For example, to see the help manual for **ipconfig**, you can use the following command: `ipconfig /?`

![](https://assets.tryhackme.com/additional/win-fun2/ipconfig-help.png)  

**Note**: To clear the command prompt screen, the command is `cls`. 

The next command is `netstat`. Per the help manual, this command will display protocol statistics and current TCP/IP network connections. 

![](https://assets.tryhackme.com/additional/win-fun2/netstat.png)  

In the above image, the line within the red box shows us an example syntax for the command. 

The structure tells us the **netstat** command can be run alone or with parameters, such as `-a`,  `-b`,  `-e`, etc. 

When any of the parameters are appended to the root command, **netstat** in this case, the output changes. Play with a few to see for yourself. 

The `net` command is primarily used to manage network resources. This command supports sub-commands.

If you type **net** without a sub-command, the output will show the syntax for the root command showing a few of the sub-commands you can use.

![](https://assets.tryhackme.com/additional/win-fun2/net.png)  

For the net command, to display the help manual `/?` will not work. In this case, you need to use different syntax, which is `net help`.

![](https://assets.tryhackme.com/additional/win-fun2/net-help.png)  

So, if you wish to see the help information for `net user` , the command is `net help user`. 

![](https://assets.tryhackme.com/additional/win-fun2/net-help-user2.png)

You can use the same command to view the help information for other useful **net** sub-commands, such as **localgroup**, **use**, **share**, and **session**. 

Refer to the following link to see a comprehensive list of commands you can execute in the command prompt [here](https://ss64.com/nt/).   

Answer the questions below

| Question                                                                               | Answer                                                        |
| -------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| In System Configuration, what is the full command for Internet Protocol Configuration? | C:\Windows\System32\cmd.exe /k %windir%\system32\ipconfig.exe |
| For the ipconfig command, how do you show detailed information?                        | ipconfig /all                                                              |
