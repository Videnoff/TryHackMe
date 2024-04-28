![](https://i.imgur.com/uwXqDdH.png)  

This task will be focusing on injection vulnerabilities. Injection vulnerabilities are quite dangerous to a company as they can potentially cause downtime and/or loss of data. Identifying injection points within a web application is usually quite simple, as most of them will return an error. There are many types of injection attacks, some of them are:

|   |   |
|---|---|
|SQL Injection|SQL Injection is when an attacker enters a malicious or malformed query to either retrieve or tamper data from a database. And in some cases, log into accounts.|
|Command Injection|Command Injection is when web applications take input or user-controlled data and run them as system commands. An attacker may tamper with this data to execute their own system commands. This can be seen in applications that perform misconfigured ping tests.|
|Email Injection|Email injection is a security vulnerability that allows malicious users to send email messages without prior authorization by the email server. These occur when the attacker adds extra data to fields, which are not interpreted by the server correctly.|

  

But in our case, we will be using **SQL Injection**.

For more information: [Injection](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A1-Injection)

Answer the questions below


| Question #1:                        | Answer                                   |
| ----------------------------------- | ---------------------------------------- |
| Log into the administrator account! | 32a5e0f21372bcc1000a6088b93b458e41f0e02a |


After we navigate to the login page, enter some data into the email and password fields.

![](https://i.imgur.com/4XHHSof.png)

 Before clicking submit, make sure Intercept mode is on.

This will allow us to see the data been sent to the server!

  

![](https://i.imgur.com/6gyZ7Vr.png)  



![[Pasted image 20240417200727.png]]



We will now change the "**a**" next to the email to: ' or 1=1-- and forward it to the server.

![](https://i.imgur.com/tPFJnmC.png)


![[Pasted image 20240417200841.png]]


![[Pasted image 20240417201140.png]]


**Why does this work?**

1. The character **'** will close the brackets in the SQL query
2. '**OR**' in a SQL statement will return true if either side of it is true. As 1=1 is always true, the whole statement is true. Thus it will tell the server that the email is valid, and log us into user id 0, which happens to be the administrator account.
3. The -- character is used in SQL to comment out data, any restrictions on the login will no longer work as they are interpreted as a comment. This is like the # and // comment in python and javascript respectively.
                      ![](https://i.imgur.com/Y7xYGjp.png)

| Question #2:                 | Answer                                   |
| ---------------------------- | ---------------------------------------- |
| Log into the Bender account! | fb364762a3c102b2db932069c0e6b78e738d4066 |


![[Pasted image 20240417201850.png]]


![[Pasted image 20240417201759.png]]



Similar to what we did in Question #1, we will now log into Bender's account! Capture the login request again, but this time we will put: bender@juice-sh.op'-- as the email. 

![](https://i.imgur.com/1F1ufc3.png)

Now, forward that to the server!  

But why don't we put the 1=1?

Well, as the email address is valid (which will return true), we do not need to force it to be true. Thus we are able to use **'--** to bypass the login system. Note the **1=1** can be used when the email or username is not known or invalid.
                     ![](https://i.imgur.com/Rznz31B.png)