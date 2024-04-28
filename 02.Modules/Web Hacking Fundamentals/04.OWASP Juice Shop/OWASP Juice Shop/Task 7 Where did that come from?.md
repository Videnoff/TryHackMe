   ![](https://i.imgur.com/qBdgNKC.png)  

XSS or Cross-site scripting is a vulnerability that allows attackers to run javascript in web applications. These are one of the most found bugs in web applications. Their complexity ranges from easy to extremely hard, as each web application parses the queries in a different way. 

**There are three major types of XSS attacks:**

| DOM (Special)            | DOM XSS _(Document Object Model-based Cross-site Scripting)_ uses the HTML environment to execute malicious javascript. This type of attack commonly uses the _<script></script>_ HTML tag.                                       |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Persistent (Server-side) | Persistent XSS is javascript that is run when the server loads the page containing it. These can occur when the server does not sanitise the user data when it is **uploaded** to a page. These are commonly found on blog posts. |
| Reflected (Client-side)  | Reflected XSS is javascript that is run on the client-side end of the web application. These are most commonly found when the server doesn't sanitise **search** data.                                                            |

More information: [Cross-Site Scripting XSS](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A7-Cross-Site_Scripting_(XSS))

Answer the questions below

==Question #1: Perform a DOM XSS!  ==

![](https://i.imgur.com/AMz9jps.png)

We will be using the iframe element with a javascript alert tag: 

```
_<iframe src="javascript:alert(`xss`)">_
```

Inputting this into the **search bar** will trigger the alert.


![](https://i.imgur.com/rKEx3aR.png)


![[Pasted image 20240420194136.png]]


Note that we are using **iframe** which is a common HTML element found in many web applications, there are others which also produce the same result. 

This type of XSS is also called XFS (Cross-Frame Scripting), is one of the most common forms of detecting XSS within web applications.

Websites that allow the user to modify the iframe or other DOM elements will most likely be vulnerable to XSS.   

**Why does this work?**

It is common practice that the search bar will send a request to the server in which it will then send back the related information, but this is where the flaw lies. Without correct input sanitation, we are able to perform an XSS attack against the search bar. 

![[Pasted image 20240420194233.png]]

| Answer | 9aaf4bbea5c30d00a1f5bbcfce4db6d4b0efe0bf |
| ------ | ---------------------------------------- |

==Question #2: Perform a persistent XSS!  ==

First, login to the **admin** account.

We are going to navigate to the "**Last Login IP**" page for this attack.  

 ![](https://i.imgur.com/YTIzhh0.png)

It should say the last IP Address is 0.0.0.0 or 10.x.x.x 

As it logs the 'last' login IP we will now logout so that it logs the 'new' IP.

![](https://i.imgur.com/4XHHSof.png)

Make sure that Burp **intercept is on**, so it will catch the logout request.

![[Pasted image 20240420194728.png]]


We will then head over to the Headers tab where we will add a new header:


```
True-Client-IP: <iframe src="javascript:alert(`xss`)">
```


![](https://i.imgur.com/VLd2Fga.png)


![[Pasted image 20240420200106.png]]


Then forward the request to the server!  
When **signing back into the admin account** and navigating to the Last Login IP page again, we will see the XSS alert!

![](https://i.imgur.com/rKEx3aR.png)


![[Pasted image 20240420200509.png]]



**Why do we have to send this Header?**

The _True-Client-IP_  header is similar to the _X-Forwarded-For_ header, both tell the server or proxy what the IP of the client is. Due to there being no sanitation in the header we are able to perform an XSS attack. 

| Answer | 149aa8ce13d7a4a8a931472308e269c94dc5f156 |
| ------ | ---------------------------------------- |

==Question #3: Perform a reflected XSS!  ==

First, we are going to need to be on the right page to perform the reflected XSS!

**Login** into the **admin account** and navigate to the 'Order History' page. 
                            ![](https://i.imgur.com/hBy4O1L.png)  

From there you will see a "Truck" icon, clicking on that will bring you to the track result page. You will also see that there is an id paired with the order.   

![](https://i.imgur.com/kQdIKyL.png)

We will use the iframe XSS, 

```
<iframe src="javascript:alert(`xss`)">
```

 in the place of the _5267-f73dcd000abcc353_

After submitting the URL, refresh the page and you will then get an alert saying XSS!

![[Pasted image 20240420201002.png]]


![](https://i.imgur.com/rKEx3aR.png)

**Why does this work?**

The server will have a lookup table or database (depending on the type of server) for each tracking ID. As the 'id' parameter is not sanitised before it is sent to the server, we are able to perform an XSS attack.

![[Pasted image 20240420201112.png]]

| Answer | 23cefee1527bde039295b2616eeb29e1edc660a0 |
| ------ | ---------------------------------------- |
