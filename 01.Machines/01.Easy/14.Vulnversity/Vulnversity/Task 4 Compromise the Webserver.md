Now that you have found a form to upload files, we can leverage this to upload and execute our payload, which will lead to compromising the web server.

Answer the questions below

| Question                                                                                               | Answer |
| ------------------------------------------------------------------------------------------------------ | ------ |
| What common file type you'd want to upload to exploit the server is blocked? Try a couple to find out. | .php   |



We will fuzz the upload form to identify which extensions are not blocked.

To do this, we're going to use BurpSuite. If you need clarification on what BurpSuite is or how to set it up, please complete our [BurpSuite module](https://tryhackme.com/module/learn-burp-suite) first.

We're going to use Intruder (used for automating customised attacks).

To begin, make a wordlist with the following extensions:

- .php
- .php3
- .php4
- .php5
- .phtml

![](https://i.imgur.com/ED153Nx.png)

Now make sure BurpSuite is configured to intercept all your browser traffic. Upload a file; once this request is captured, send it to the Intruder. Click on "Payloads" and select the "Sniper" attack type.

![[Pasted image 20240302121719.png]]


![[Pasted image 20240302121928.png]]


Click the "Positions" tab now, find the filename and "Add §" to the extension. It should look like so:

![](https://i.imgur.com/6dxnzq6.png)


![[Pasted image 20240302122439.png]]

![[Pasted image 20240302122959.png]]

![[Pasted image 20240302123455.png]]

| Question                                    | Answer |
| ------------------------------------------- | ------ |
| Run this attack, what extension is allowed? | .phtml |


Now that we know what extension we can use for our payload, we can progress.

We are going to use a PHP reverse shell as our payload. A reverse shell works by being called on the remote host and forcing this host to make a connection to you. So you'll listen for incoming connections, upload and execute your shell, which will beacon out to you to control!

Download the following reverse PHP shell [here](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php).

To gain remote access to this machine, follow these steps:  

1. Edit the php-reverse-shell.php file and edit the ip to be your tun0 ip (you can get this by going to [http://10.10.10.10](http://10.10.10.10) in the browser of your TryHackMe connected device).  
      
    ![[Pasted image 20240302123948.png]]
    
1. Rename this file to php-reverse-shell.phtml  

	  ![[Pasted image 20240302124104.png]]
	  
    
3. We're now going to listen to incoming connections using netcat. Run the following command: 
   
```
nc -lvnp 1234
```

![[Pasted image 20240302124230.png]]


4. Upload your shell and navigate to **http://**10.10.227.251:3333/internal/uploads/php-reverse-shell.phtml** - This will execute your payload  

![[Pasted image 20240302124415.png]]


    
5. You should see a connection on your Netcat session

![](https://i.imgur.com/FGcvTCp.png)


![[Pasted image 20240302124518.png]]


*Stabilize shell*:

```
python -c "import pty; pty.spawn('/bin/bash')"
```

![[Pasted image 20240302233015.png]]

```
Ctrl+Z
```

![[Pasted image 20240302233654.png]]

```
stty raw -echo
```

```
fd
```

```
export TERM=xterm
```

![[Pasted image 20240302233742.png]]

| Question                                                | Answer |
| ------------------------------------------------------- | ------ |
| What is the name of the user who manages the webserver? | bill   |

![[Pasted image 20240302124717.png]]


| Question               | Answer                           |
| ---------------------- | -------------------------------- |
| What is the user flag? | 8bd7992fbe8a6ad22a63361004cfcedb |


![[Pasted image 20240302124749.png]]
