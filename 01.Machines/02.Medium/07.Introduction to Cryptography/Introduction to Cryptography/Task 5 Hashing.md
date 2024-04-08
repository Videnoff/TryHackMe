A cryptographic hash function is an algorithm that takes data of arbitrary size as its input and returns a fixed size value, called _message digest_ or _checksum_, as its output. For example, `sha256sum` calculates the SHA256 (Secure Hash Algorithm 256) message digest. SHA256, as the name indicates, returns a checksum of size 256 bits (32 bytes). This checksum is usually written using hexadecimal digits. Knowing that a hexadecimal digit represents 4 bits, the 256 bits checksum can be represented as 64 hexadecimal digits.

In the terminal output below, we calculate the SHA256 hash values for three files of varying sizes: 4 bytes, 275 MB, and 5.2 GB. Using `sha256sum` to calculate the message digest for each of the three files, we get three completely different values that appear random. It is worth stressing that the length of the resulting message digest or checksum is the same, no matter how small or big the file is. In particular, the four-byte file `abc.txt` and the 5.2 GB file resulted in message digests of equal length independent of the file size.

![[Pasted image 20240318185931.png]]

But why would we need such a function? There are many uses, in particular:

- Storing passwords: Instead of storing passwords in plaintext, a hash of the password is stored instead. Consequently, if a data breach occurs, the attacker will get a list of password hashes instead of the original passwords. (In practice, passwords are also “salted”, as discussed in a later task.)
- Detecting modifications: Any minor modification to the original file would lead to a drastic change in hash value, i.e. checksum.

In the following terminal output, we have two files, `text1.txt` and `text2.txt`, which are almost identical except for (literally) one bit being different; the letters `T` and `t` are different in one bit in their ASCII representation. Even though we have flipped only a single bit, it is evident that the SHA256 checksums are entirely different. Consequently, if we use a secure hash function algorithm, we can easily confirm whether any modifications have taken place. This can help protect against both intentional tampering and file transfer errors.

![[Pasted image 20240318185952.png]]

Some of the hashing algorithms in use and still considered secure are:

- SHA224, SHA256, SHA384, SHA512
- RIPEMD160

Some older hash functions, such as MD5 (Message Digest 5) and SHA-1, are cryptographically broken. By broken, we mean that it is possible to generate a different file with the same checksum as a given file. This means that we can create a hash collision. In other words, an attacker can create a new message with a given checksum, and detecting file or message tampering won’t be possible.

### HMAC

Hash-based message authentication code (HMAC) is a message authentication code (MAC) that uses a cryptographic key in addition to a hash function.

According to [RFC2104](https://www.rfc-editor.org/rfc/rfc2104), HMAC needs:

- secret key
- inner pad (ipad) a constant string. (RFC2104 uses the byte `0x36` repeated B times. The value of B depends on the chosen hash function.)
- outer pad (opad) a constant string. (RFC2104 uses the byte `0x5C` repeated B times.)

Calculating the HMAC follows the following steps as shown in the figure:

1. Append zeroes to the key to make it of length B, i.e., to make its length match that of the ipad.
2. Using bitwise exclusive-OR (XOR), represented by ⊕, calculate _k__e__y_ ⊕ _i__p__a__d_.
3. Append the message to the XOR output from step 2.
4. Apply the hash function to the resulting stream of bytes (in step 3).
5. Using XOR, calculate _k__e__y_ ⊕ _o__p__a__d_.
6. Append the hash function output from step 4 to the XOR output from step 5.
7. Apply the hash function to the resulting stream of bytes (in step 6) to get the HMAC.

![Graphical illustration showing how an HMAC is calculated](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/d8b175af1d32a759f66b223efdac8972.png)  

The figure above represents the steps expressed in the following formula: _H_(_K_⊕_o__p__a__d_,_H_(_K_⊕_i__p__a__d_,_t__e__x__t_)).

To calculate the HMAC on a Linux system, you can use any of the available tools such as `hmac256` (or `sha224hmac`, `sha256hmac`, `sha384hmac`, and `sha512hmac`, where the secret key is added after the option `--key`). Below we show an example of calculating the HMAC using `hmac256` and `sha256hmac` with two different keys.

![[Pasted image 20240318190014.png]]

Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task05`; alternatively, you can use the task file from Task 2 to work on your own machine.

| Question                                              | Answer                                                           |
| ----------------------------------------------------- | ---------------------------------------------------------------- |
| What is the SHA256 checksum of the file `order.json`? | 2c34b68669427d15f76a1c06ab941e3e6038dacdfb9209455c87519a3ef2c660 |
```
sha256sum order.json
```


| Question                                                                                                 | Answer                                                           |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Open the file `order.json` and change the amount from `1000` to `9000`. What is the new SHA256 checksum? | 11faeec5edc2a2bad82ab116bbe4df0f4bc6edd96adac7150bb4e6364a238466 |
```
sha256sum order.json
```


| Question                                                              | Answer                                                           |
| --------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Using SHA256 and the key `3RfDFz82`, what is the HMAC of `order.txt`? | c7e4de386a09ef970300243a70a444ee2a4ca62413aeaeb7097d43d2c5fac89f |
```
hmac256 3RfDFz82 order.txt
```
