The **System Configuration** utility (`MSConfig`) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues. 

Reference the following document [here](https://docs.microsoft.com/en-us/troubleshoot/windows-client/performance/system-configuration-utility-troubleshoot-configuration-errors) for more information on the System Configuration utility. 

There are several methods to launch System Configuration. One method is from the Start Menu.

![](https://assets.tryhackme.com/additional/win-fun2/msconfig-start.png)  

**Note**: You need local administrator rights to open this utility. 

The utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task. 

1. General
2. Boot
3. Services
4. Startup
5. Tools

![](https://assets.tryhackme.com/additional/win-fun2/msconfig1.png)  

In the **General** tab, we can select what devices and services for Windows to load upon boot. The options are: **Normal**, **Diagnostic**, or **Selective**. 

In the **Boot** tab, we can define various boot options for the Operating System. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig2.png)  

The **Services** tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application that runs in the background.  

![](https://assets.tryhackme.com/additional/win-fun2/msconfig3.png)  

In the **Startup** tab, you won't see anything interesting in the attached VM.  Below is a screenshot of the Startup tab for **MSConfig** from my local machine. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig4.png)  

As you can see, Microsoft advises using **Task Manager (**`taskmgr`**)** to manage (enable/disable) startup items. The System Configuration utility is **NOT** a startup management program. 

**Note**: If you open Task Manager for the attached VM, you will notice that Task Manager doesn't show a Startup tab. 

There is a list of various utilities (tools) in the Tools tab that we can run to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig5.png)  

Notice the **Selected command** section. The information in this textbox will change per tool.

To run a tool, we can use the command to launch the tool via the run prompt, command prompt, or by clicking the `Launch` button. 

Answer the questions below

| Question                                                                                       | Answer                                                          |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| What is the name of the service that lists Systems Internals as the manufacturer?              | PsShutdown                                                      |
| Whom is the Windows license registered to?                                                     | Windows User                                                    |
| What is the command for Windows Troubleshooting?                                               | C:\Windows\System32\control.exe /name Microsoft.Troubleshooting |
| What command will open the Control Panel? (The answer is  the name of .exe, not the full path) | control.exe                                                                |
