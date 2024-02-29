You can launch the target machine attached to this room to replicate the examples shown below. Any Metasploit version 5 or 6 will have menus and screens similar to those shown here so you can use the AttackBox or any operating system installed on your local computer.  

Once you have entered the context of a module using the `use` command followed by the module name, as seen earlier, you will need to set parameters. The most common parameters you will use are listed below. Remember, based on the module you use, additional or different parameters may need to be set. It is good practice to use the `show options` command to list the required parameters.

All parameters are set using the same command syntax:  
`set PARAMETER_NAME VALUE`  

Before we proceed, remember always to check the msfconsole prompt to ensure you are in the right context. When dealing with Metasploit, you may see five different prompts:

- **The regular command prompt:** You can not use Metasploit commands here.

![[Pasted image 20240226193518.png]]


- **The msfconsole prompt:** msf6 (or msf5 depending on your installed version) is the msfconsole prompt. As you can see, no context is set here, so context-specific commands to set parameters and run modules can not be used here.

![[Pasted image 20240226193644.png]]

  
- **A context prompt:** Once you have decided to use a module and used the set command to chose it, the msfconsole will show the context. You can use context-specific commands (e.g. set RHOSTS 10.10.x.x) here.

![[Pasted image 20240226193947.png]]



- **The Meterpreter prompt:** Meterpreter is an important payload we will see in detail later in this module. This means a Meterpreter agent was loaded to the target system and connected back to you. You can use Meterpreter specific commands here.

![[Pasted image 20240226194022.png]]


- **A shell on the target system:** Once the exploit is completed, you may have access to a command shell on the target system. This is a regular command line, and all commands typed here run on the target system.

![[Pasted image 20240226194050.png]]

As mentioned earlier, the `show options` command will list all available parameters.

![[Pasted image 20240226194152.png]]

As you can see in the screenshot above, some of these parameters require a value for the exploit to work. Some required parameter values will be pre-populated, make sure you check if these should remain the same for your target. For example, a web exploit could have an RPORT (remote port: the port on the target system Metasploit will try to connect to and run the exploit) value preset to 80, but your target web application could be using port 8080.

In this example, we will set the RHOSTS parameter to the IP address of our target system using the `set` command.

![[Pasted image 20240226194238.png]]


Once you have set a parameter, you can use the `show options` command to check the value was set correctly.

Parameters you will often use are:

- **RHOSTS:** “Remote host”, the IP address of the target system. A single IP address or a network range can be set. This will support the CIDR (Classless Inter-Domain Routing) notation (/24, /16, etc.) or a network range (10.10.10.x – 10.10.10.y). You can also use a file where targets are listed, one target per line using file:/path/of/the/target_file.txt, as you can see below.

![[Pasted image 20240226194306.png]]

- **RPORT:** “Remote port”, the port on the target system the vulnerable application is running on.
- **PAYLOAD:** The payload you will use with the exploit.
- **LHOST:** “Localhost”, the attacking machine (your AttackBox or Kali Linux) IP address.
- **LPORT:** “Local port”, the port you will use for the reverse shell to connect back to. This is a port on your attacking machine, and you can set it to any port not used by any other application.
- **SESSION:** Each connection established to the target system using Metasploit will have a session ID. You will use this with post-exploitation modules that will connect to the target system using an existing connection.

  

You can override any set parameter using the set command again with a different value. You can also clear any parameter value using the `unset` command or clear all set parameters with the `unset all` command.

![[Pasted image 20240226194336.png]]

You can use the `setg` command to set values that will be used for all modules. The `setg` command is used like the set command. The difference is that if you use the `set` command to set a value using a module and you switch to another module, you will need to set the value again. The `setg` command allows you to set the value so it can be used by default across different modules. You can clear any value set with `setg` using `unsetg`.

  

The example below uses the following flow;

1. We use the ms17_010_eternalblue exploitable
2. We set the RHOSTS variable using the `setg` command instead of the set command
3. We use the `back` command to leave the exploit context
4. We use an auxiliary (this module is a scanner to discover MS17-010 vulnerabilities)
5. The `show options` command shows the RHOSTS parameter is already populated with the IP address of the target system.

![[Pasted image 20240226194400.png]]

The `setg` command sets a global value that will be used until you exit Metasploit or clear it using the `unsetg` command.

  

**Using modules**

Once all module parameters are set, you can launch the module using the `exploit` command. Metasploit also supports the `run` command, which is an alias created for the `exploit` command as the word exploit did not make sense when using modules that were not exploits (port scanners, vulnerability scanners, etc.).

  
The `exploit` command can be used without any parameters or using the “`-z`” parameter.

The `exploit -z` command will run the exploit and background the session as soon as it opens.

![[Pasted image 20240226194422.png]]

This will return you the context prompt from which you have run the exploit.

Some modules support the `check` option. This will check if the target system is vulnerable without exploiting it.

  

**Sessions**  
Once a vulnerability has been successfully exploited, a session will be created. This is the communication channel established between the target system and Metasploit.

  

You can use the `background` command to background the session prompt and go back to the msfconsole prompt.

![[Pasted image 20240226194445.png]]

Alternatively, `CTRL+Z` can be used to background sessions.

The `sessions` command can be used from the msfconsole prompt or any context to see the existing sessions.

![[Pasted image 20240226194504.png]]

To interact with any session, you can use the `sessions -i` command followed by the desired session number.

![[Pasted image 20240226194524.png]]

Answer the questions below

| Question                                                        | Answer                  |
| --------------------------------------------------------------- | ----------------------- |
| How would you set the LPORT value to 6666?                      | set LPORT 6666          |
| How would you set the global value for RHOSTS  to 10.10.19.23 ? | setg RHOSTS 10.10.19.23 |
| What command would you use to clear a set payload?              | unset payload           |
| What command do you use to proceed with the exploitation phase? | exploit                 |
