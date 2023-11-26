What is a **firewall**?

Per Microsoft, "_Traffic flows into and out of devices via what we call ports. A firewall is what controls what is - and more importantly isn't - allowed to pass through those ports. You can think of it like a security guard standing at the door, checking the ID of everything that tries to enter or exit_".

The below image will reflect what you will see when you navigate to **Firewall & network protection**.  

![](https://assets.tryhackme.com/additional/win-fun3/windows-firewall.png)  

**Note**: Each network may have different status icons for you.

What is the difference between the 3 (**Domain**, **Private**, and **Public**)?

Per Microsoft, "_Windows Firewall offers three firewall profiles: domain, private and public"._

- **Domain** - _The domain profile applies to networks where the host system can authenticate to a domain controller._ 
- **Private** - _The private profile is a user-assigned profile and is used to designate private or home networks._
- **Public** - _The default profile is the public profile, used to designate public networks such as Wi-Fi hotspots at coffee shops, airports, and other locations._

If you click on any firewall profile, another screen will appear with two options: **turn the firewall on/off** and **block all incoming connections**. 

![](https://assets.tryhackme.com/additional/win-fun3/windows-firewall2.png)  

**Warning**: Unless you are **100%** confident in what you are doing, it is recommended that you leave your Windows Defender Firewall enabled. 

**Allow an app through firewall**  

![](https://assets.tryhackme.com/additional/win-fun3/windows-firewall3.png)

You can view what the current settings for any firewall profile are. In the above image, several apps have access in the Private and/or Public firewall profile. Some of the apps will provide additional information if it's available via the `Details` button. 

**Advanced Settings**

![](https://assets.tryhackme.com/additional/win-fun3/windows-firewall4.png)

Configuring the **Windows Defender Firewall** is for advanced Windows users. Refer to the following Microsoft documentation on best practices [here](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/best-practices-configuring). 

**Tip:** Command to open the Windows Defender Firewall is `WF.msc`. 

Answer the questions below

| Question                                                                                      | Answer |
| --------------------------------------------------------------------------------------------- | ------ |
| If you were connected to airport Wi-Fi, what most likely will be the active firewall profile? | Public network       |
