### What is PGP?

PGP stands for Pretty Good Privacy. It’s a software that implements encryption for encrypting files, performing digital signing and more.

### What is GPG?

[GnuPG or GPG](https://gnupg.org/) is an Open Source implementation of PGP from the GNU project. You may need to use GPG to decrypt files in CTFs. With PGP/GPG, private keys can be protected with passphrases in a similar way to SSH private keys. If the key is passphrase protected, you can attempt to crack this passphrase using John The Ripper and gpg2john. The key provided in this task is not protected with a passphrase.

The man page for GPG can be found online [here](https://www.gnupg.org/gph/de/manual/r1023.html).

### What about AES?

AES, sometimes called Rijndael after its creators, stands for Advanced Encryption Standard. It was a replacement for DES which had short keys and other cryptographic flaws.

AES and DES both operate on blocks of data (a block is a fixed size series of bits).

AES is complicated to explain, and doesn’t seem to come up as often. If you’d like to learn how it works, here’s an excellent video from Computerphile [https://www.youtube.com/watch?v=O4xNJsjtN6E](https://www.youtube.com/watch?v=O4xNJsjtN6E)

Answer the questions below

| Question                                                                                                      | Answer     |
| ------------------------------------------------------------------------------------------------------------- | ---------- |
| Time to try some GPG. Download the archive attached and extract it somewhere sensible.                        |            |
| You have the private key, and a file encrypted with the public key. Decrypt the file. What's the secret word? | Pineapple. |
```
gpg --import tryhackme.key
```
```
gpg2john tryhackme.key > hash
```
```
john --format=gpg --wordlist=/usr/share/wordlists/rockyou.txt hash
```
```
gpg --decrypt message.gpg
```
![[Pasted image 20240403200411.png]]
