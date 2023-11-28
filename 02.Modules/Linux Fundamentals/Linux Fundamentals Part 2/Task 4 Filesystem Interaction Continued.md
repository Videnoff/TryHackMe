We covered some of the most fundamental commands when interacting with the filesystem on the Linux machine. For example, we covered how to list and find the contents of folders using `ls` and `find` and navigating the filesystem using `cd`. 

In this task, we're going to learn some more commands for interacting with the filesystem to allow us to:

- create files and folders
- move files and folders
- delete files and folders

More specifically, the following commands:

| Command | Full Name      | Purpose                      |
| ------- | -------------- | ---------------------------- |
| touch   | touch          | Create file                  |
| mkdir   | make directory | Create a folder              |
| cp      | copy           | Copy a file or folder        |
| mv      | move           | Move a file or folder        |
| rm      | remove         | Remove a file or folder      |
| file    | file           | Determine the type of a file |

_Protip: Similarly to using cat, we can provide full file paths, i.e. directory1/directory2/note for all of these commands_

  

**Creating Files and Folders (touch, mkdir)**

Creating files and folders on Linux is a simple process. First, we'll cover creating a file. The touch command takes exactly one argument -- the name we want to give the file we create. For example, we can create the file "note" by using `touch note`. It's worth noting that touch simply creates a blank file. You would need to use commands like echo or text editors such as nano to add content to the blank file.

Using touch to create a new file

![[Pasted image 20231127211526.png]]


This is a similar process for making a folder, which just involves using the `mkdir` command and again providing the name that we want to assign to the directory. For example, creating the directory "mydirectory" using `mkdir mydirectory`.

Creating a new directory with mkdir

![[Pasted image 20231127211606.png]]


  

**Removing Files and Folders (rm)**

`rm` is extraordinary out of the commands that we've covered so far. You can simply remove files by using `rm`. However, you need to provide the `-R` switch alongside the name of the directory you wish to remove.

Using rm to remove a file

![[Pasted image 20231127211636.png]]



Using rm recursively to remove a directory

![[Pasted image 20231127211655.png]]



**Copying and Moving Files and Folders (cp, mv)**

Copying and moving files is an important functionality on a Linux machine. Starting with `cp`, this command takes two arguments:

1. the name of the existing file

2. the name we wish to assign to the new file when copying

`cp` copies the entire contents of the existing file into the new file. In the screenshot below, we are copying "note" to "note2".

Using cp to copy a file

![[Pasted image 20231127211732.png]]



Moving a file takes two arguments, just like the cp command. However, rather than copying and/or creating a new file, `mv` will merge or modify the second file that we provide as an argument. Not only can you use `mv` to move a file to a new folder, but you can also use `mv` to rename a file or folder. For example, in the screenshot below, we are renaming the file "note2" to be named "note3". "note3" will now have the contents of "note2". 

Using mv to move a file

![[Pasted image 20231127211751.png]]

  

**Determining File Type**

What is often misleading and often catches people out is making presumptions from files as to what their purpose or contents may be. Files usually have what's known as an extension to make this easier. For example, text files usually have an extension of ".txt". But this is not necessary.

So far, the files we have used in our examples haven't had an extension. Without knowing the context of why the file is there -- we don't really know its purpose. Enter the `file` command. This command takes one argument. For example, we'll use `file` to confirm whether or not the "note" file in our examples is indeed a text file, like so `file note`.

Using file to determine the contents of a file

![[Pasted image 20231127211815.png]]


Answer the questions below

| Question                                                                                        | Answer              |
| ----------------------------------------------------------------------------------------------- | ------------------- |
| How would you create the file named "newnote"?                                                  | touch newnote       |
| On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory? | ASCII text          |
| How would we move the file "myfile" to the directory "myfolder"                                 | mv myfile /myfolder |
| What are the contents of this file?                                                             | THM{FILESYSTEM}                    |
| Continue to apply your knowledge and practice the commands from this task.                      |                     |
