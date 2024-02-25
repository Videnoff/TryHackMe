Ok now that we have had a brief introduction to what bash is and what it is used for let's jump right into some examples!

  

First of all let’s lay out our structure.

A bash script always starts with the following line of code at the top of the script.
                                                                        ![](https://i.ibb.co/7W5mn0c/carbon-8.png)  

  

  

This is so your shell (whatever type of it) knows that it needs to run your file using bash in the terminal.

  
  

Lets get into some basic examples.
                                                                         ![](https://i.ibb.co/Hz1VQ1D/carbon-9.png)

  

  

This will return the string “Hello World”. The command “`echo`” is used to output text to the screen, the same way as “`print`” in python. I suggest you test this out in your terminal to get to grips with bash!

You can also perform normal Linux commands inside your bash script and it will be executed if formatted right. For example we can run the command “`ls`” inside our bash script and we will see the output when we run the file. So lets make it do this!
                                                                        ![](https://i.ibb.co/HX85VzF/carbon-10.png)  

  

  

Now from here on I am going to assume that you have a basic understanding of Linux and its commands, if you don't please go make sure to check out the Linux fundamentals 1 and then come back and try again. [https://tryhackme.com/room/linux1](https://tryhackme.com/room/linux1)

I'm also not going to include the `#!/bin/bash` at the start of my code snippets otherwise it will take up a lot of room so be aware that you need it always at the start of your files!

Now to run our bash script we must first give it executable permissions

`Chmod +x yourfile.sh`

And then we run it using `./`
                                                                        ![](https://i.ibb.co/ccWWddT/carbon-11.png)

  

  

Please run this for yourself and see what you get.

We can see it has outputted the results of the commands “`whoami`” and “`id`”.

  

  

Answer the questions below

| Question                                                                         | Answer |
| -------------------------------------------------------------------------------- | ------ |
| What piece of code can we insert at the start of a line to comment out our code? | #       |
| What will the following script output to the screen, echo “BishBashBosh”         | BishBashBosh       |
