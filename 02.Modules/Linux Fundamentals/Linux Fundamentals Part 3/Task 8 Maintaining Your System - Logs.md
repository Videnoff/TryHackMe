We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let's quickly recap. Located in the /var/log directory, these files and folders contain logging information for applications and services running on your system. The Operating System  (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating".

I have highlighted some logs from three services running on a Ubuntu machine:

- An Apache2 web server
- Logs for the fail2ban service, which is used to monitor attempted brute forces, for example
- The UFW service which is used as a firewall

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log1.png)

These services and logs are a great way in monitoring the health of your system and protecting it. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:

- access log
- error log

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log2.png)

There are, of course, logs that store information about how the OS is running itself and actions that are performed by users, such as authentication attempts.

Answer the questions below

| Question                                                  | Answer       |
| --------------------------------------------------------- | ------------ |
| Look for the apache2 logs on the deployable Linux machine |              |
| What is the IP address of the user who visited the site?  | 10.9.232.111 |
| What file did they access?                                | catsanddogs.jpg             |
