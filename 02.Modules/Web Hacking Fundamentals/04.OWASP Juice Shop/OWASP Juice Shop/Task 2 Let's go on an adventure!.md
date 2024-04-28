             ![[Pasted image 20240416222827.png]]
             
Before we get into the actual hacking part, it's good to have a look around. In Burp, set the Intercept mode to off and then browse around the site. This allows Burp to log different requests from the server that may be helpful later. 

This is called **walking through** the application, which is also a form of **reconnaissance**!

Answer the questions below

| Question #1:                              | Answer            |
| ----------------------------------------- | ----------------- |
| What's the Administrator's email address? | admin@juice-sh.op |


![](https://i.imgur.com/hPXolAn.png)

The reviews show each user's email address. Which, by clicking on the Apple Juice product, shows us the Admin email!

![](https://i.imgur.com/YFWDP5v.png)

| Question #2:                          | Answer |
| ------------------------------------- | ------ |
| What parameter is used for searching? | q      |


![](https://i.imgur.com/pZLtWQl.png)

Click on the magnifying glass in the top right of the application will pop out a search bar.

![](https://i.imgur.com/bFgw6uS.png)

We can then input some text and by pressing **Enter** will search for the text which was just inputted.

Now pay attention to the URL which will now update with the text we just entered.

![](https://i.imgur.com/AzJ3FAM.png)

We can now see the search parameter after the **/#/search?** the letter **q**

| Question #3:                                | Answer    |
| ------------------------------------------- | --------- |
| What show does Jim reference in his review? | Star Trek |


Jim did a review on the Green Smoothie product. We can see that he mentions a replicator. 

![](https://i.imgur.com/RCFw2tB.png)

If we google "**replicator**" we will get the results indicating that it is from a TV show called Star Trek

![](https://i.imgur.com/Sp8ymGR.png)