Now that we have the password hashes, we can crack them and get the root password! Recall from the previous outputs that our root password hash is 
"`$6$rFK4s/vE$zkh2/RBiRZ746OW3/Q/zqTRVfrfYJfFjFc2/q.oYtoF1KglS3YWoExtT3cvA3ml9UtDS8PFzCk902AsWx00Ck.`".

Luckily hashcat supports cracking linux password hashes. You can find a list of hashcat modes [here](https://hashcat.net/wiki/doku.php?id=example_hashes) and rockyou.txt(a popular wordlist) [here](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) (if you don't already have it on your system)  

Recommended tool - Hashcat:

Usage: `hashcat {flags} {hashfile} {wordlist}`

Useful flags:

| -a  | Specify attack mode,attack modes can be found in the man page. |
| --- | -------------------------------------------------------------- |
| -m  | Specifies which mode to use, refer back to the list of modes   |

  

Answer the questions below

| Question                   | Answer    | SS                                   |
| -------------------------- | --------- | ------------------------------------ |
| What is the root password! | love2fish | ![[Pasted image 20240328225454.png]] |

```
hashcat -m 1800 -a 0 rootpass /usr/share/wordlists/rockyou.txt
```
