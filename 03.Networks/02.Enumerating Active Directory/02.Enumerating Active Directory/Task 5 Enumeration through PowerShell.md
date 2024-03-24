**PowerShell**

PowerShell is the upgrade of Command Prompt. Microsoft first released it in 2006. While PowerShell has all the standard functionality Command Prompt provides, it also provides access to cmdlets (pronounced command-lets), which are .NET classes to perform specific functions. While we can write our own cmdlets, like the creators of [PowerView](https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerView) did, we can already get very far using the built-in ones.

Since we installed the AD-RSAT tooling in Task 3, it automatically installed the associated cmdlets for us. There are 50+ cmdlets installed. We will be looking at some of these, but refer to [this list for the complete list of cmdlets.](https://docs.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps)

Using our SSH terminal, we can upgrade it to a PowerShell terminal using the following command: `powershell`

![[Pasted image 20240308224150.png]]

**Users**

We can use the `Get-ADUser` cmdlet to enumerate AD users:

```
Get-ADUser -Identity gordon.stevens -Server za.tryhackme.com -Properties *
```

![[Pasted image 20240308221817.png]]

The parameters are used for the following:

- -Identity - The account name that we are enumerating
- -Properties - Which properties associated with the account will be shown, * will show all properties
- -Server - Since we are not domain-joined, we have to use this parameter to point it to our domain controller

For most of these cmdlets, we can also use the `-Filter` parameter that allows more control over enumeration and use the `Format-Table` cmdlet to display the results such as the following neatly:


```
Get-ADUser -Filter 'Name -like "*stevens"' -Server za.tryhackme.com | Format-Table Name,SamAccountName -A
```

![[Pasted image 20240308221854.png]]


**Groups**

We can use the `Get-ADGroup` cmdlet to enumerate AD groups:

```
Get-ADGroup -Identity Administrators -Server za.tryhackme.com
```

![[Pasted image 20240308221926.png]]

We can also enumerate group membership using the `Get-ADGroupMember` cmdlet:

```
Get-ADGroupMember -Identity Administrators -Server za.tryhackme.com
```

![[Pasted image 20240308221956.png]]

**AD Objects**

A more generic search for any AD objects can be performed using the `Get-ADObject` cmdlet. For example, if we are looking for all AD objects that were changed after a specific date:

```
$ChangeDate = New-Object DateTime(2022, 02, 28, 12, 00, 00)
```

![[Pasted image 20240308222028.png]]

If we wanted to, for example, perform a password spraying attack without locking out accounts, we can use this to enumerate accounts that have a badPwdCount that is greater than 0, to avoid these accounts in our attack:

```
Get-ADObject -Filter 'badPwdCount -gt 0' -Server za.tryhackme.com
```

![[Pasted image 20240308222120.png]]

This will only show results if one of the users in the network mistyped their password a couple of times.  

**Domains**  

We can use `Get-ADDomain` to retrieve additional information about the specific domain:

```
Get-ADDomain -Server za.tryhackme.com
```

![[Pasted image 20240308222146.png]]

**Altering AD Objects**  

The great thing about the AD-RSAT cmdlets is that some even allow you to create new or alter existing AD objects. However, our focus for this network is on enumeration. Creating new objects or altering existing ones would be considered AD exploitation, which is covered later in the AD module.

However, we will show an example of this by force changing the password of our AD user by using the `Set-ADAccountPassword` cmdlet:

```
Set-ADAccountPassword -Identity gordon.stevens -Server za.tryhackme.com -OldPassword (ConvertTo-SecureString -AsPlaintext "old" -force) -NewPassword (ConvertTo-SecureString -AsPlainText "new" -Force) 
```

![[Pasted image 20240308222323.png]]

Remember to change the identity value and password for the account you were provided with for enumeration on the distributor webpage in Task 1.  

**Benefits**  

- The PowerShell cmdlets can enumerate significantly more information than the net commands from Command Prompt.
- We can specify the server and domain to execute these commands using runas from a non-domain-joined machine.  
    
- We can create our own cmdlets to enumerate specific information.
- We can use the AD-RSAT cmdlets to directly change AD objects, such as resetting passwords or adding a user to a specific group.  
    

**Drawbacks**

- PowerShell is often monitored more by the blue teams than Command Prompt.
- We have to install the AD-RSAT tooling or use other, potentially detectable, scripts for PowerShell enumeration.  
    

Answer the questions below

| Question                                                             | Answer |
| -------------------------------------------------------------------- | ------ |
| What is the value of the Title attribute of Beth Nolan (beth.nolan)? | Senior |

![[Pasted image 20240308225213.png]]
![[Pasted image 20240308225242.png]]


| Question                                                                                   | Answer                                                              |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| What is the value of the DistinguishedName attribute of Annette Manning (annette.manning)? | CN=annette.manning,OU=Marketing,OU=People,DC=za,DC=tryhackme,DC=com |

![[Pasted image 20240308225425.png]]


| Question                                  | Answer                |
| ----------------------------------------- | --------------------- |
| When was the Tier 2 Admins group created? | 2/24/2022 10:04:41 PM |

![[Pasted image 20240308230534.png]]



| Question                                                               | Andwer                                       |
| ---------------------------------------------------------------------- | -------------------------------------------- |
| What is the value of the SID attribute of the Enterprise Admins group? | S-1-5-21-3330634377-1326264276-632209373-519 |

![[Pasted image 20240308230833.png]]



| Question                                             | Answer                                       |
| ---------------------------------------------------- | -------------------------------------------- |
| Which container is used to store deleted AD objects? | CN=Deleted Objects,DC=za,DC=tryhackme,DC=com |

![[Pasted image 20240308231623.png]]
