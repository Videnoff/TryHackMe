
![](https://i.imgur.com/OM71q2D.png)  


In this task, we will look at exploiting authentication through different flaws. When talking about flaws within authentication, we include mechanisms that are vulnerable to manipulation. These mechanisms, listed below, are what we will be exploiting. 

Weak passwords in high privileged accounts

Forgotten password pages

 More information: [Broken Authentication](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A2-Broken_Authentication)

Answer the questions below


| Question #1:                                     | Answer                                   |
| ------------------------------------------------ | ---------------------------------------- |
| Bruteforce the Administrator account's password! | c2110d06dc6f81c67cd8099ff0ba601241f1ac0e |


We have used SQL Injection to log into the Administrator account but we still don't know the password. Let's try a brute-force attack! We will once again capture a login request, but instead of sending it through the proxy, we will send it to Intruder.

Go to Positions and then select the Clear § button. In the password field place two § inside the quotes. To clarify, the § § is not two sperate inputs but rather Burp's implementation of quotations e.g. "". The request should look like the image below. 

![](https://i.imgur.com/I96sO28.png)  

For the payload, we will be using the best1050.txt from Seclists. (Which can be installed via: **apt-get install seclists**)

_You can load the list from:_ _/usr/share/wordlists/SecLists/Passwords/Common-Credentials/best1050.txt_

Once the file is loaded into Burp, start the attack. You will want to filter for the request by status.

A failed request will receive a 401 Unauthorized   ![](https://i.imgur.com/HcUs6eW.png)

Whereas a successful request will return a 200 OK. ![](https://i.imgur.com/q5jcfIA.png)

![[Pasted image 20240418225938.png]]


Once completed, login to the account with the password.

![[Pasted image 20240418230124.png]]


| Question #2:          | Answer                                   |
| --------------------- | ---------------------------------------- |
| Reset Jim's password! | 094fbc9b48e525150ba97d05b942bbf114987257 |


Believe it or not, the reset password mechanism can also be exploited! When inputted into the email field in the Forgot Password page, Jim's security question is set to _"Your eldest siblings middle name?"_.


![[Pasted image 20240419195339.png]]



In Task 2, we found that Jim might have something to do with Star Trek. Googling "Jim Star Trek" gives us a wiki page for Jame T. Kirk from Star Trek. 
       ![](https://i.imgur.com/axsRMp2.png)  

  

Looking through the wiki page we find that he has a brother.

![](https://i.imgur.com/PfHXA1h.png)

  

Looks like his brother's middle name is **Samuel**

Inputting that into the Forgot Password page allows you to successfully change his password.

![[Pasted image 20240419195719.png]]



You can change it to anything you want!

  

![](https://i.imgur.com/uRS3kJr.png)