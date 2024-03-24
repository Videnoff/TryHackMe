This network is the continuation of the [Breaching AD](https://tryhackme.com/jr/breachingad) network. Please make sure to complete this network before continuing with this one. Also, note that we will discuss AD objects extensively. If you need a refresher, have a quick reskim of [this room.](https://tryhackme.com/jr/activedirectorybasics) Now that we have our very first set of valid Active Directory (AD) credentials, we will explore the different methods that can be used to enumerate AD.  

**AD Enumeration**

Once we have that first set of AD credentials and the means to authenticate with them on the network, a whole new world of possibilities opens up! We can start enumerating various details about the AD setup and structure with authenticated access, even super low-privileged access.

During a red team engagement, this will usually lead to us being able to perform some form of privilege escalation or lateral movement to gain additional access until we have sufficient privileges to execute and reach our goals. In most cases, enumeration and exploitation are heavily entwined. Once an attack path shown by the enumeration phase has been exploited, enumeration is again performed from this new privileged position, as shown in the diagram below.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/ddd4bddb2db2285c3e42eef4c35b6211.png)  

  

**Learning Objectives**

In this network, we will cover several methods that can be used to enumerate AD. This is by no means a complete list as available methods are usually highly situational and dependent on the acquired breach. However, we will cover the following techniques for enumerating AD:

- The AD snap-ins of the Microsoft Management Console.  
    
- The net commands of Command Prompt.
- The AD-RSAT cmdlets of PowerShell.
- Bloodhound.  
    

**Connecting to the Network**  

*AttackBox*  

If you are using the Web-based AttackBox, you will be connected to the network automatically if you start the AttackBox from the room's page. You can verify this by running the ping command against the IP of the THMDC.za.tryhackme.com host. We do still need to configure DNS, however. Windows Networks use the Domain Name Service (DNS) to resolve hostnames to IPs. Throughout this network, DNS will be used for the tasks. You will have to configure DNS on the host on which you are running the VPN connection. In order to configure our DNS, run the following command:

```
systemd-resolve --interface enumad --set-dns $THMDCIP --set-domain za.tryhackme.com
```

![[Pasted image 20240305222756.png]]

Remember to replace $THMDCIP with the IP of THMDC in your network diagram. You can test that DNS is working by running:

`nslookup thmdc.za.tryhackme.com`

This should resolve to the IP of your DC.

**Note: DNS may be reset on the AttackBox roughly every 3 hours. If this occurs, you will have to restart the systemd-resolved service. If your AttackBox terminates and you continue with the room at a later stage, you will have to redo all the DNS steps.**  

You should also take the time to make note of your VPN IP. Using `ifconfig` or `ip a`, make note of the IP of the **enumad** network adapter. This is your IP and the associated interface that you should use when performing the attacks in the tasks.

**Other Hosts**  

If you are going to use your own attack machine, an OpenVPN configuration file will have been generated for you once you join the room. Go to your [access](https://tryhackme.com/access) page. Select 'EnumeratingAD' from the VPN servers (under the network tab) and download your configuration file.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/6712a0d8bbc1e985a1beed2e191782cf.png)  

Use an OpenVPN client to connect. This example is shown on a Linux machine; similar guides to connect using Windows or macOS can be found at your [access](https://tryhackme.com/r/access) page.

```
sudo openvpn adenumeration.ovpn
```

![[Pasted image 20240305222837.png]]

The message "Initialization Sequence Completed" tells you that you are now connected to the network. Return to your access page. You can verify you are connected by looking on your access page. Refresh the page, and you should see a green tick next to Connected. It will also show you your internal IP address.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/4adcdaa110dfcdba0d5c62ee47f45d67.png)  

**Note:** You still have to configure DNS similar to what was shown above. It is important to note that although not used, the DC does log DNS requests. If you are using your machine, these logs may include the hostname of your device.

**Kali**

If you are using a Kali VM, Network Manager is most likely used as DNS manager. You can use GUI Menu to configure DNS:

- Network Manager -> Advanced Network Configuration -> Your Connection -> IPv4 Settings
- Set your DNS IP here to the IP for THMDC in the network diagram above  
    
- Add another DNS such as 1.1.1.1 or similar to ensure you still have internet access
- Run `sudo systemctl restart NetworkManager` and test your DNS similar to the steps above.

Requesting Your Credentials

To simulate an AD breach, you will be provided with your first set of AD credentials. Once your networking setup has been completed, on your Attack Box, navigate to [http://distributor.za.tryhackme.com/creds](http://distributor.za.tryhackme.com/creds) to request your credential pair. Click the "Get Credentials" button to receive your credential pair that can be used for initial access.

This credential pair will provide you RDP and SSH access to THMJMP1.za.tryhackme.com. THMJMP1 can be seen as a jump host into this environment, simulating a foothold that you have achieved. Jump hosts are often targeted by the red team since they provide access to a new network segment. You can use Remmina or any other similar Remote Desktop client to connect to this host for RDP. Remember to specify the domain of za.tryhackme.com when connecting. Task 2 and 3 will require RDP access.

![[Pasted image 20240305225142.png]]

For SSH access, you can use the following SSH command:

`ssh za.tryhackme.com\\<AD Username>@thmjmp1.za.tryhackme.com`

When prompted, provide your account's associated password. Although RDP can be used for all tasks, SSH is faster and can be used for Task 4, 5, and 6.  

SSH:

![[Pasted image 20240305225629.png]]

RDP:

![[Pasted image 20240305230251.png]]

Answer the questions below

| Question                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------- | ------ |
| I have completed the Breaching AD network and am ready to learn about AD enumeration techniques.           |        |
| I have connected to the network and configured DNS.                                                        |        |
| I have requested my credential pair from the distributor and verified that I can RDP and SSH into THMJMP1. |        |
