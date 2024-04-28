![](https://i.imgur.com/r2qq6de.png)

Modern-day systems will allow for multiple users to have access to different pages. Administrators most commonly use an administration page to edit, add and remove different elements of a website. You might use these when you are building a website with programs such as Weebly or Wix.  

When Broken Access Control exploits or bugs are found, it will be categorised into one of **two types**:

| **Horizontal** Privilege Escalation | Occurs when a user can perform an action or access data of another user with the **same** level of permissions. |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Vertical** Privilege Escalation   | Occurs when a user can perform an action or access data of another user with a higher level of permissions.     |

  

![](https://i.imgur.com/bJ9WKY4.png)

_Credits: Packetlabs.net_

More information: [Broken Access Control](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A5-Broken_Access_Control)  

Answer the questions below

==Question #1: Access the administration page!  ==

First, we are going to open the **Debugger** on Firefox. 

(Or **Sources** on **Chrome**.)

This can be done by navigating to it in the Web Developers menu. 

![](https://i.imgur.com/rvhCm6V.png)![](https://i.imgur.com/oWJI6Yi.png)  

We are then going to refresh the page and look for a javascript file for main-es2015.js

We will then go to that page at: [http://10.10.227.49](http://machine_ip/)/main-es2015.js

![](https://i.imgur.com/wF55kiO.png)  

To get this into a format we can read, click the { } button at the bottom  ![](https://i.imgur.com/93xvM6I.png)

Now search for the term "admin" 

You will come across a couple of different words containing "admin" but the one we are looking for is "path: administration"

![](https://i.imgur.com/AS1YVjU.png)  

This hints towards a page called "**/#/administration**" as can be seen by the **about** path a couple lines below, but going there while not logged in doesn't work. 

As this is an Administrator page, it makes sense that we need to be in the **Admin account** in order to view it.

A good way to stop users from accessing this is to only load parts of the application that need to be used by them. This stops sensitive information such as an admin page from been leaked or viewed.  

| Answer | 946a799363226a24822008503f5d1324536629a0 |
| ------ | ---------------------------------------- |

![[Pasted image 20240419221951.png]]



==Question #2: View another user's shopping basket!  ==

Login to the Admin account and click on 'Your Basket'. Make sure Burp is running so you can capture the request!

Forward each request until you see: _GET /rest/basket/1 HTTP/1.1_

![](https://i.imgur.com/wlS88AU.png)  


![[Pasted image 20240420123627.png]]


Now, we are going to change the number **1** after /basket/ to **2**

![](https://i.imgur.com/ugsRunL.png)

It will now show you the basket of UserID 2. You can do this for other UserIDs as well, provided that they have one!

![](https://i.imgur.com/yR4xFo3.png)


![[Pasted image 20240420124004.png]]


| Answer | 41b997a36cc33fbe4f0ba018474e19ae5ce52121 |
| ------ | ---------------------------------------- |


==Question #3: Remove all 5-star reviews!==  

Navigate to the  [](http://machine_ip/#/administration)[http://10.10.227.49](http://machine_ip/#/administration)[/#/administration](http://machine_ip/#/administration) page again and click the bin icon next to the review with 5 stars!

  

![](https://i.imgur.com/cI2sSyx.png)

![[Pasted image 20240420125400.png]]


| Answer | 50c97bcce0b895e446d61c83a21df371ac2266ef |
| ------ | ---------------------------------------- |
