![](https://i.imgur.com/qi5qt4r.png)  

  

OWASP Zap is a security testing framework much like Burp Suite. It acts as a very robust enumeration tool. It’s used to test web applications.

Why wouldn’t I use Burp Suite?

That’s a GOOD question! Most people in the Info-sec community DO just use Burp Suite. But OWASP ZAP has a few benefits and features that the Burp Suite does not and it’s my preferred program of the two. 

What are the benefits to OWASP ZAP?

It’s completely open source and free. There is no premium version, no features are locked behind a paywall, and there is no proprietary code.  

There’s a couple of feature benefits too with using OWASP ZAP over Burp Suite:

- Automated Web Application Scan: This will automatically passively and actively scan a web application, build a sitemap, and discover vulnerabilities. This is a paid feature in Burp. 
    
- Web Spidering: You can passively build a website map with Spidering. This is a paid feature in Burp.
    
- Unthrottled Intruder: You can bruteforce login pages within OWASP as fast as your machine and the web-server can handle. This is a paid feature in Burp.
    
- No need to forward individual requests through Burp: When doing manual attacks, having to change windows to send a request through the browser, and then forward in burp, can be tedious. OWASP handles both and you can just browse the site and OWASP will intercept automatically. This is NOT a feature in Burp. 
    

If you’re already familiar with Burp the keywords translate over like so:

![](https://lh6.googleusercontent.com/KpTw37QyRfu1WTf5rIGz4ZDwEPm7s4CutgFTSrFBsXJT97a8HT8HiIcuUciFCyVXxcfVmCMuX1TbhOAM2gZLBYgkzPQzpF3tcd_DpcudC6JElYRDoZhUcXeP4mtn83UeUa7gKnWG)

This guide will teach you how to do the following in ZAP: 

- Automated Scan
    
- Directory Bruteforce
    
- Authenticated Scan
    
- Login Page Bruteforce
    
- Install ZAP Extensions
    

This room will be using OWASP Zap against the DVWA machine, feel free to deploy your own instance and follow along.

Answer the questions below

| Question                                                                                                                                                              | Answer           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| What does ZAP stand for?                                                                                                                                              | Zed Attack Proxy |
| Connect to the TryHackMe network and deploy the machine. Once deployed, wait a few minutes and visit the web application: [http://10.10.54.184](http://10.10.54.184/) |                  |
