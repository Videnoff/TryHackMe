Before jumping into AD objects and enumeration, let's first talk about credential injection methods. From the Breaching AD network, you would have seen that credentials are often found without compromising a domain-joined machine. Specific enumeration techniques may require a particular setup to work.  

**Windows vs Linux**

_"If you know the enemy and know yourself, you need not fear the results of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer defeat."_ - Sun Tzu, Art of War.  

You can get incredibly far doing AD enumeration from a Kali machine. Still, if you genuinely want to do in-depth enumeration and even exploitation, you need to understand and mimic your enemy. Thus, you need a Windows machine. This will allow us to use several built-in methods to stage our enumeration and exploits. In this network, we will explore one of these built-in tools, called the `runas.exe` binary.

**Runas Explained**

Have you ever found AD credentials but nowhere to log in with them? Runas may be the answer you've been looking for!

In security assessments, you will often have network access and have just discovered AD credentials but have no means or privileges to create a new domain-joined machine. So we need the ability to use those credentials on a Windows machine we control.

If we have the AD credentials in the format of :, we can use Runas, a legitimate Windows binary, to inject the credentials into memory. The usual Runas command would look something like this:

```
runas.exe /netonly /user:<domain>\<username> cmd.exe
```

Let's look at the parameters:

- **/netonly** - Since we are not domain-joined, we want to load the credentials for network authentication but not authenticate against a domain controller. So commands executed locally on the computer will run in the context of your standard Windows account, but any network connections will occur using the account specified here.
- **/user** - Here, we provide the details of the domain and the username. It is always a safe bet to use the Fully Qualified Domain Name (FQDN) instead of just the NetBIOS name of the domain since this will help with resolution.
- **cmd.exe** - This is the program we want to execute once the credentials are injected. This can be changed to anything, but the safest bet is cmd.exe since you can then use that to launch whatever you want, with the credentials injected.

Once you run this command, you will be prompted to supply a password. Note that since we added the /netonly parameter, the credentials will not be verified directly by a domain controller so that it will accept any password. We still need to confirm that the network credentials are loaded successfully and correctly.

**Note:** If you use your own Windows machine, you should make sure that you run your first Command Prompt as Administrator. This will inject an Administrator token into CMD. If you run tools that require local Administrative privileges from your Runas spawned CMD, the token will already be available. This does not give you administrative privileges on the network, but will ensure that any local commands you execute, will execute with administrative privileges.  

**It's Always DNS**

*Note:* These next steps you only need to perform if you use your own Windows machine for the exercise. However, it is good knowledge to learn how to perform since it may be helpful on red team exercises.

After providing the password, a new command prompt window will open. Now we still need to verify that our credentials are working. The most surefire way to do this is to list SYSVOL. Any AD account, no matter how low-privileged, can read the contents of the SYSVOL directory.

SYSVOL is a folder that exists on all domain controllers. It is a shared folder storing the Group Policy Objects (GPOs) and information along with any other domain related scripts. It is an essential component for Active Directory since it delivers these GPOs to all computers on the domain. Domain-joined computers can then read these GPOs and apply the applicable ones, making domain-wide configuration changes from a central location.

Before we can list SYSVOL, we need to configure our DNS. Sometimes you are lucky, and internal DNS will be configured for you automatically through DHCP or the VPN connection, but not always (like this TryHackMe network). It is good to understand how to do it manually. Your safest bet for a DNS server is usually a domain controller. Using the IP of the domain controller, we can execute the following commands in a PowerShell window:

```powershell
$dnsip = "<DC IP>"
$index = Get-NetAdapter -Name 'Ethernet' | Select-Object -ExpandProperty 'ifIndex'
Set-DnsClientServerAddress -InterfaceIndex $index -ServerAddresses $dnsip
```

Of course, 'Ethernet' will be whatever interface is connected to the TryHackMe network. We can verify that DNS is working by running the following:

```
nslookup za.tryhackme.com
```

![[Pasted image 20240305230541.png]]


```
dir \\za.tryhackme.com\SYSVOL\
```

![[Pasted image 20240305230553.png]]

We won't go too much in-depth now into the contents of SYSVOL, but note that it is also good to enumerate its contents since there may be some additional AD credentials lurking there.  

**IP vs Hostnames**

*Question:* _Is there a difference between_ _`dir \\za.tryhackme.com\SYSVOL` and `dir \\<DC IP>\SYSVOL`_ _and why the big fuss about DNS?_

There is quite a difference, and it boils down to the authentication method being used. When we provide the hostname, network authentication will attempt first to perform Kerberos authentication. Since Kerberos authentication uses hostnames embedded in the tickets, if we provide the IP instead, we can force the authentication type to be NTLM. While on the surface, this does not matter to us right now, it is good to understand these slight differences since they can allow you to remain more stealthy during a Red team assessment. In some instances, organisations will be monitoring for OverPass- and Pass-The-Hash Attacks. Forcing NTLM authentication is a good trick to have in the book to avoid detection in these cases.

**Using Injected Credentials**

Now that we have injected our AD credentials into memory, this is where the fun begins. With the /netonly option, all network communication will use these injected credentials for authentication. This includes all network communications of applications executed from that command prompt window.

This is where it becomes potent. Have you ever had a case where an MS SQL database used Windows Authentication, and you were not domain-joined? Start MS SQL Studio from that command prompt; even though it shows your local username, click Log In, and it will use the AD credentials in the background to authenticate! We can even use this to [authenticate to web applications that use NTLM Authentication](https://labs.f-secure.com/blog/pth-attacks-against-ntlm-authenticated-web-applications/).  

We will be using that in the next task for our first AD enumeration technique.  

Answer the questions below


| Question                                                                                                                  | Answer                  |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| What native Windows binary allows us to inject credentials legitimately into memory?                                      | runas.exe               |
| What parameter option of the runas binary will ensure that the injected credentials are used for all network connections? | /netonly                |
| What network folder on a domain controller is accessible by any authenticated AD account and stores GPO information?      | SYSVOL                  |
| When performing dir \\za.tryhackme.com\SYSVOL, what type of authentication is performed by default?                       | Kerberos authentication |
