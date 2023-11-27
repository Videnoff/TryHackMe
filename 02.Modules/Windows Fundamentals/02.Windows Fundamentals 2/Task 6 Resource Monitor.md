We're continuing with Tools that are available through the System Configuration panel.  

What is **Resource Monitor** (`resmon`)?

Per Microsoft, "_Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data._"

As some of the other tools mentioned in this room, this utility is geared primarily to advanced users who need to perform advanced troubleshooting on the computer system.  

In the Overview tab, Resmon has four sections:

- **CPU**
- **Disk**
- **Network**
- **Memory**

![](https://assets.tryhackme.com/additional/win-fun2/resmon1.png)  

The same four sections have corresponding tabs across the top. See below.

![](https://assets.tryhackme.com/additional/win-fun2/resmon2.png)  

Note that each tab has additional information for each. An image is shown below for each tab. 

**CPU**

![](https://assets.tryhackme.com/additional/win-fun2/resmon-cpu.png)  

**Memory**

![](https://assets.tryhackme.com/additional/win-fun2/resmon-mem.png)  

**Disk**

![](https://assets.tryhackme.com/additional/win-fun2/resmon-disk.png)  

**Network**

![](https://assets.tryhackme.com/additional/win-fun2/resmon-network.png)  

Although not captured in any of the images above, Resource Monitor has a pane at the far right. This pane shows a graphical view in real-time for each section. 

**Note**: The information displayed in Resource Monitor will be different for you compared to the images above.  

Answer the questions below

| Question                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------- | ------ |
| What is the command to open Resource Monitor? (The answer is the name of the .exe file, not the full path) | resmon.exe       |
