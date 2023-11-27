We're continuing with Tools that are available through the System Configuration panel.  

What is the **System Information** (`msinfo32`) tool?

Per Microsoft, "_Windows includes a tool called Microsoft System Information (Msinfo32.exe).  This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues._"

The  information in **System Summary** is divided into three sections:

- **Hardware Resources**
- **Components**
- **Software Environment**

System Summary will display general technical specifications for the computer, such as processor brand and model.

![](https://assets.tryhackme.com/additional/win-fun2/system-summary.png)  

The information displayed in **Hardware Resources** is not for the average computer user. If you want to learn more about this section, refer to the official Microsoft [page](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/hardware-resources#:~:text=Hardware%20resources%20are%20the%20assignable,of%20bus%2Drelative%20memory%20addresses.).

![](https://assets.tryhackme.com/additional/win-fun2/hardware-resources.png)  

Under **Components**, you can see specific information about the hardware devices installed on the computer. Some sections don't show any information, but some sections do, such as **Display** and **Input**.

![](https://assets.tryhackme.com/additional/win-fun2/components.png)  

In the **Software Environmen**t section, you can see information about software baked into the operating system and software you have installed. Other details are visible in this section as well, such as the **Environment Variables** and **Network Connections**. 

![](https://assets.tryhackme.com/additional/win-fun2/software-env.png)

Recall from the [Windows Fundamentals 1 room](https://tryhackme.com/room/windowsfundamentals1xbx) (The Windows\System32 Folder task) where **Environment Variables** was briefly touched on. 

Per [Microsoft](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1), "_Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders._

_The environment variables store data that is used by the operating system and other programs. For example, the WINDIR environment variable contains the location of the Windows installation directory. Programs can query the value of this variable to determine where Windows operating system files are located_".

Click on `Environment Variables` to see the assigned values for the virtual machine.

![](https://assets.tryhackme.com/additional/win-fun2/env-variables.png)  

Another method to view environment variables is `Control Panel > System and Security > System > Advanced system settings > Environment Variables` **OR** `Settings > System > About > system info > Advanced system settings > Environment Variables`.

![](https://assets.tryhackme.com/additional/win-fun2/env-variables2.png)  

The detour is over. Let's redirect our attention back to `msinfo32` and pick up where we left off.

Towards the very bottom of this utility, there is a search bar. Please give it a go. Select Components and search for `IP address`.

![](https://assets.tryhackme.com/additional/win-fun2/msinfo32-search.png)  

Answer the questions below

| Question                                                                                                     | Answer       |
| ------------------------------------------------------------------------------------------------------------ | ------------ |
| What is the command to open System Information? (The answer is the name of the .exe file, not the full path) | msinfo32.exe |
| What is listed under System Name?                                                                            | THM-WINFUN2  |
| Under Environment Variables, what is the value for ComSpec?                                                  | %SystemRoot%\system32\cmd.exe             |
