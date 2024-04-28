   ![](https://i.imgur.com/XlbJl1E.png)  

A web application should store and transmit sensitive data safely and securely. But in some cases, the developer may not correctly protect their sensitive data, making it vulnerable.

Most of the time, data protection is not applied consistently across the web application making certain pages accessible to the public. Other times information is leaked to the public without the knowledge of the developer, making the web application vulnerable to an attack. 

More information: [Sensitive Data Exposure](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A3-Sensitive_Data_Exposure)

Answer the questions below

==Question #1: Access the Confidential Document!  ==

  

![](https://i.imgur.com/M1s8jfu.png)

Navigate to the About Us page, and hover over the _"Check out our terms of use"_.

  

![](https://i.imgur.com/5PsmlD4.png)

  

You will see that it links to  [http://10.10.227.49](http://machine_ip/ftp/legal.md)[/ftp/legal.md](http://machine_ip/ftp/legal.md). Navigating to that **/ftp/** directory reveals that it is exposed to the public!

![](https://i.imgur.com/EY664PR.png)  

![](https://i.imgur.com/Xp2aZJW.png)  


![[Pasted image 20240419200342.png]]

We will download the acquisitions.md and save it. It looks like there are other files of interest here as well.

After downloading it, navigate to the **home page** to receive the flag!

![[Pasted image 20240419201449.png]]


| Answer | edf9281222395a1c5fee9b89e32175f1ccf50c5b |
| ------ | ---------------------------------------- |

==Question #2: Log into MC SafeSearch's account!  ==

After watching the video there are certain parts of the song that stand out.

He notes that his password is "Mr. Noodles" but he has replaced some "vowels into zeros", meaning that he just replaced the o's into 0's.

We now know the password to the _mc.safesearch@juice-sh.op_ account is "**Mr. N00dles**"

![[Pasted image 20240419203054.png]]


![[Pasted image 20240419203110.png]]


| Answer | 66bdcffad9e698fd534003fbb3cc7e2b7b55d7f0 |
| ------ | ---------------------------------------- |


==Question #3: Download the Backup file!  ==

We will now go back to the  [http://10.10.227.49](http://machine_ip/ftp/)[/ftp/](http://machine_ip/ftp/) folder and try to download package.json.bak. But it seems we are met with a 403 which says that only .md and .pdf files can be downloaded. 

![](https://i.imgur.com/LDUkDBQ.png)  

To get around this, we will use a character bypass called "Poison Null Byte". A Poison Null Byte looks like this: _%00_. 

Note: as we can download it using the url, we will need to encode this into a url encoded format.

The Poison Null Byte will now look like this: _%2500._ Adding this and then a **.md** to the end will bypass the 403 error!

![](https://i.imgur.com/2qugsl5.png)

**Why does this work?** 

A Poison Null Byte is actually a NULL terminator. By placing a NULL character in the string at a certain byte, the string will tell the server to terminate at that point, nulling the rest of the string.

![[Pasted image 20240419203842.png]]

| Answer | bfc1e6b4a16579e85e06fee4c36ff8c02fb13795 |
| ------ | ---------------------------------------- |
