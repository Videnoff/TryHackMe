The Windows folder (`C:\Windows`) is traditionally known as the folder which contains the Windows operating system. 

The folder doesn't have to reside in the C drive necessarily. It can reside in any other drive and technically can reside in a different folder.

This is where environment variables, more specifically system environment variables, come into play. Even though not discussed yet, the system  environment variable for the Windows directory is `%windir%`.

Per [Microsoft](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1), "_Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders_".

There are many folders within the 'Windows' folder. See below.

![](https://assets.tryhackme.com/additional/win-fun1/windows-folder.png)  

One of the many folders is **System32**. 

![](https://assets.tryhackme.com/additional/win-fun1/windows-system32.png)  

The System32 folder holds the important files that are critical for the operating system.

You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational. Read more about this action [here](https://www.howtogeek.com/346997/what-is-the-system32-directory-and-why-you-shouldnt-delete-it/). 

**Note**: Many of the tools that will be covered in the Windows Fundamentals series reside within the System32 folder. 

Answer the questions below

| Question                                            | Answer |
| --------------------------------------------------- | ------ |
| What is the system variable for the Windows folder? | %windir%       |
