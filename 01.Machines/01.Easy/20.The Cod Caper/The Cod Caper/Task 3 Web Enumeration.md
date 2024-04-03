Since the only services running are SSH and Apache, it is safe to assume that we should check out the web server first for possible vulnerabilities. One of the first things to do is to see what pages are available to access on the web server.

Recommended tool: gobuster  

Useful flags:  

| -x         | Used to specify file extensions i.e "php,txt,html"                                                                                                                |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --url      | Used to specify which url to enumerate                                                                                                                            |
| --wordlist | Used to specify which wordlist that is appended on the url path i.e<br><br>"http://url.com/word1"<br><br>"http://url.com/word2"<br><br>"http://url.com/word3.php" |

Recommended wordlist: [big.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/big.txt)  

Answer the questions below

| Question                                              | Answer             | SS                                   |
| ----------------------------------------------------- | ------------------ | ------------------------------------ |
| What is the name of the important file on the server? | /administrator.php | ![[Pasted image 20240324225043.png]] |
```
gobuster dir --url http://10.10.210.201 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html -o scans/gobuster
```
