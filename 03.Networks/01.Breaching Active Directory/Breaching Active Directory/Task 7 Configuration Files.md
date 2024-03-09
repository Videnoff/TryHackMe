The last enumeration avenue we will explore in this network is configuration files. Suppose you were lucky enough to cause a breach that gave you access to a host on the organisation's network. In that case, configuration files are an excellent avenue to explore in an attempt to recover AD credentials. Depending on the host that was breached, various configuration files may be of value for enumeration: 

- Web application config files  
    
- Service configuration files
- Registry keys
- Centrally deployed applications  
    

Several enumeration scripts, such as [Seatbelt](https://github.com/GhostPack/Seatbelt), can be used to automate this process.

**Configuration File Credentials**  

However, we will focus on recovering credentials from a centrally deployed application in this task. Usually, these applications need a method to authenticate to the domain during both the installation and execution phases. An example of such as application is McAfee Enterprise Endpoint Security, which organisations can use as the endpoint detection and response tool for security.  

McAfee embeds the credentials used during installation to connect back to the orchestrator in a file called ma.db. This database file can be retrieved and read with local access to the host to recover the associated AD service account. We will be using the SSH access on THMJMP1 again for this exercise.

The ma.db file is stored in a fixed location:

```
cd C:\ProgramData\McAfee\Agent\DB
```

![[Pasted image 20240304204910.png]]

We can use SCP to copy the ma.db to our AttackBox:

```
scp thm@THMJMP1.za.tryhackme.com:C:/ProgramData/McAfee/Agent/DB/ma.db .
```

![[Pasted image 20240304204943.png]]

![[Pasted image 20240304224053.png]]


To read the database file, we will use a tool called sqlitebrowser. We can open the database using the following command:

```
sqlitebrowser ma.db
```

![[Pasted image 20240304205022.png]]

Using sqlitebrowser, we will select the Browse Data option and focus on the AGENT_REPOSITORIES table:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/aeda85be24462cc6a3f0c03cd899053a.png)  


![[Pasted image 20240304224218.png]]

We are particularly interested in the second entry focusing on the DOMAIN, AUTH_USER, and AUTH_PASSWD field entries. Make a note of the values stored in these entries. However, the AUTH_PASSWD field is encrypted. Luckily, McAfee encrypts this field with a known key. Therefore, we will use the following old python2 script to decrypt the password. The script has been provided as a downloadable task file or on the AttackBox, it can be found in the `/root/Rooms/BreachingAD/task7/` directory.

**Note: The tool we will use here is quite old. It uses Python v2 and relies on an old crypto library. If you cannot get the script to work on your own VM, please make use of the AttackBox. However, there has been a recent update to the application to ensure that it works on Python3 as well, you can download the latest version here: [https://github.com/funoverip/mcafee-sitelist-pwd-decryption](https://github.com/funoverip/mcafee-sitelist-pwd-decryption)**  

You will have to unzip the mcafee-sitelist-pwd-decryption.zip file:

```
unzip mcafeesitelistpwddecryption.zip
```

![[Pasted image 20240304205059.png]]

By providing the script with our base64 encoded and encrypted password, the script will provide the decrypted password:

```
python2 mcafee_sitelist_pwd_decrypt.py <AUTH PASSWD VALUE>
```

![[Pasted image 20240304205144.png]]

![[Pasted image 20240304225843.png]]


We now once again have a set of AD credentials that we can use for further enumeration! This is just one example of recovering credentials from configuration files. If you are ever able to gain a foothold on a host, make sure to follow a detailed and refined methodology to ensure that you recover all loot from the host, including credentials and other sensitive information that can be stored in configuration files.  

Answer the questions below

| Question                                                                                                                     | Answer              |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| What type of files often contain stored credentials on hosts?                                                                | Configuration Files |
| What is the name of the McAfee database that stores configuration including credentials used to connect to the orchestrator? | ma.db               |
| What table in this database stores the credentials of the orchestrator?                                                      | AGENT_REPOSITORIES  |
| What is the username of the AD account associated with the McAfee service?                                                   | svcAV               |
| What is the password of the AD account associated with the McAfee service?                                                   | MyStrongPassword!   |
