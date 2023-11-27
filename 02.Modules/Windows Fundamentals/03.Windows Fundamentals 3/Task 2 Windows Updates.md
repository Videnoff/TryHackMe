Let's start things off with **Windows** **Update**. 

Windows Update is a service provided by Microsoft to provide security updates, feature enhancements, and patches for the Windows operating system and other Microsoft products, such as Microsoft Defender. 

Updates are typically released on the 2nd Tuesday of each month. This day is called **Patch Tuesday**. That doesn't necessarily mean that a critical update/patch has to wait for the next Patch Tuesday to be released. If the update is urgent, then Microsoft will push the update via the Windows Update service to the Windows devices.  

Refer to the following link to see the **Microsoft Security Update** **Guide** [here](https://msrc.microsoft.com/update-guide)**.**  

Windows Update is located in Settings. See below.

**Tip**: Another way to access Windows Update is from the Run dialog box, or CMD, by running the command `control /name Microsoft.WindowsUpdate`.

![](https://assets.tryhackme.com/additional/win-fun3/windows-update2.png)  

In the attached VM, there are a few things to highlight. 

1. The Windows Update settings are 'managed'. (Typically, home users will not see this type of message) 
2. There are no available updates available for the virtual machine. (The attached virtual machine does not have Internet access to communicate with Microsoft to obtain new updates)

![](https://assets.tryhackme.com/additional/win-fun3/windows-update2b.png)  

Throughout the years, Windows users have grown accustomed to pushing Windows Updates off to a later date or not installing the updates at all. Various reasons caused this action, one being the fact that a reboot is typically required after a Windows update.  

Microsoft notably addressed this issue with Windows 10. The updates can no longer be ignored or pushed to the side until forgotten. Windows updates can only be postponed, but eventually, the update will happen, and your computer will reboot. Microsoft provides these updates to keep the device safe and secure. 

Below is an image showing how a **Restart required** looks and the several options available regarding scheduling the restart.

![](https://assets.tryhackme.com/additional/win-fun3/windows-update3.png)  

Refer to the Windows Updates [FAQ](https://support.microsoft.com/en-us/windows/windows-update-faq-8a903416-6f45-0718-f5c7-375e92dddeb2) for more information.

Answer the questions below

| Question                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------- | ------ |
| There were two definition updates installed in the attached VM. On what date were these updates installed? | 5/3/2021       |
