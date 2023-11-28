A majority of commands allow for arguments to be provided. These arguments are identified by a hyphen and a certain keyword known as flags or switches.

We'll later discuss how we can identify what commands allow for arguments to be provided and understanding what these do exactly.

When using a command, unless otherwise specified, it will perform its default behaviour. For example, `ls` lists the contents of the working directory. However, hidden files are not shown. We can use flags and switches to extend the behaviour of commands.

Using our `ls` example, `ls` informs us that there is only one folder named "folder1" as highlighted in the screenshot below. Note that the contents in the screenshots below are only examples.

Using ls to view the contents of a directory

![[Pasted image 20231127210624.png]]


However, after using the `-a` argument (short for `--all`), we now suddenly have an output with a few more files and folders such as ".hiddenfolder". Files and folders with "**.**" are hidden files.

Using ls to view hidden folders

![[Pasted image 20231127210703.png]]


Commands that accept these will also have a `--help` option. This option will list the possible options that the command accepts, provide a brief description and example of how to use it.

Listing the options we can use with ls

![[Pasted image 20231127210555.png]]


This option is, in fact, a formatted output of what is called the man page (short for manual), which contains documentation for Linux commands and applications.

**The Man(ual) Page**

The manual pages are a great source of information for both system commands and applications available on both a Linux machine, which is accessible on the machine itself and [online](https://linux.die.net/man/).

To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for. Using our ls example, we would use `man ls` to view the manual pages for `ls` like so:

Listing the options we can use with ls

![[Pasted image 20231127210425.png]]


Answer the questions below

| Question                                                                  | Answer |
| ------------------------------------------------------------------------- | ------ |
| Explore the manual page of the ls command                                 |        |
| What directional arrow key would we use to navigate down the manual page? | down   |
| What flag would we use to display the output in a "human-readable" way?   | -h       |
