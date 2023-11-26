Virus & threat protection is divided into two parts:  

- **Current threats**
- **Virus & threat protection settings**

The image below only focuses on **Current threats**. 

![](https://assets.tryhackme.com/additional/win-fun3/windows-security3.png)  

**Current threats**

**Scan options**

- **Quick scan** - Checks folders in your system where threats are commonly found.
- **Full scan** - Checks all files and running programs on your hard disk. This scan could take longer than one hour.
- **Custom scan** - Choose which files and locations you want to check.

**Threat history**

- **Last scan** - Windows Defender Antivirus automatically scans your device for viruses and other threats to help keep it safe.
- **Quarantined threats** - Quarantined threats have been isolated and prevented from running on your device. They will be periodically removed.
- **Allowed threats** - Allowed threats are items identified as threats, which you allowed to run on your device. 

**Warning**: Allow an item to run that has been identified as a threat only if you are **100%** sure of what you are doing. 

Next is **Virus & threat protection settings**.

![](https://assets.tryhackme.com/additional/win-fun3/windows-security4.png)  

**Virus & threat protection settings**

**Manage settings** 

- **Real-time protection** - Locates and stops malware from installing or running on your device.
- **Cloud-delivered protection** - Provides increased and faster protection with access to the latest protection data in the cloud.
- **Automatic sample submission** - Send sample files to Microsoft to help protect you and others from potential threats. 
- **Controlled folder access** - Protect files, folders, and memory areas on your device from unauthorized changes by unfriendly applications.
- **Exclusions** - Windows Defender Antivirus won't scan items that you've excluded.
- **Notifications** - Windows Defender Antivirus will send notifications with critical information about the health and security of your device. 

Warning: Excluded items could contain threats that make your device vulnerable. Only use this option if you are **100%** sure of what you are doing.   

**Virus & threat protection updates**

- **Check for updates** - Manually check for updates to update Windows Defender Antivirus definitions.  

**Ransomware protection**

- **Controlled folder access** - Ransomware protection requires this feature to be enabled, which in turn requires Real-time protection to be enabled.

**Note**: Real-time protection is turned off in the attached VM to decrease the chances of performance issues. Since the VM can't reach the Internet and there aren't any threats in the VM, this is safe to do. Real-time protection should definitely be enabled in your personal Windows devices unless you have a 3rd party product that provides the same protection. Ensure it's always up-to-date and enabled.  

**Tip**: You can perform on-demand scans on any file/folder by right-clicking the item and selecting 'Scan with Microsoft Defender'.

The below image was taken from another Windows device to show this feature.

![](https://assets.tryhackme.com/additional/win-fun3/windows-defender-scan.png)  

Answer the questions below

| Question                                                                   | Answer |
| -------------------------------------------------------------------------- | ------ |
| Specifically, what is turned off that Windows is notifying you to turn on? | Real-time protection       |
