Using a key exchange such as the Diffie-Hellman key exchange allows us to agree on a secret key under the eyes and ears of eavesdroppers. This key can be used with a symmetric encryption algorithm to ensure confidential communication. However, the key exchange we described earlier is not immune to Man-in-the-Middle (MITM) attack. The reason is that Alice has no way of ensuring that she is communicating with Bob, and Bob has no way of ensuring that he is communicating with Alice when exchanging the secret key.

Consider the figure below. It is an attack against the key exchange explained in the Diffie-Hellman Key Exchange task. The steps are as follows:

1. Alice and Bob agree on _q_ and _g_. Anyone listening on the communication channel can read these two values, including the attacker, Mallory.
2. As she would normally do, Alice chooses a random variable _a_, calculates _A_ ( _A_ = (_g__a_) mod _q_) and sends _A_ to Bob. Mallory has been waiting for this step, and she has selected a random variable _m_ and calculated the respective _M_. As soon as Mallory receives _A_, she sends _M_ to Bob, pretending she is Alice.
3. Bob receives _M_ thinking that Alice sent it. Bob has already picked a random variable _b_ and calculated the respective _B_; he sends _B_ to Alice. Similarly, Mallory intercepts the message, reads _B_ and sends _M_ to Alice instead.
4. Alice receives _M_ and calculates _k__e__y_ = _M__a_ mod _q_.
5. Bob receives _M_ and calculates _k__e__y_ = _M__b_ mod _q_.

Alice and Bob continue to communicate, thinking that they are communicating directly, unaware that they are communicating with Mallory, who can read and modify the messages before sending them to the intended recipient.

![Illustration showing the Man-in-the-Middle attack against Diffie-Hellman Key Exchange](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/640464d74c639afe684eed13c6707229.png)  

This susceptibility necessitates some mechanism that would allow us to confirm the other party’s identity. This brings us to Public Key Infrastructure (PKI).

Consider the case where you are browsing the website [example.org](https://example.org/) over HTTPS. How can you be confident that you are indeed communicating with the `example.org` server(s)? In other words, how can you be sure that no man-in-the-middle intercepted the packets and altered them before they reached you? The answer lies in the website certificate.

The figure below shows the page we get when browsing example.org. Most browsers represent the encrypted connection with some kind of a lock icon. This lock icon indicates that the connection is secured over HTTPS with a valid certificate.

![Screenshot of a browser showing a lock icon for an encrypted connection](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/0c5bba05433f39f193e19b111a623f33.png)  

At the time of writing, example.org uses a certificate signed by DigiCert Inc., as shown in the figure below. In other words, DigiCert confirms that this certificate is valid (till a certain date).

![Screenshot showing the validity of a website certificate](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/22c1e51aec7038f6247317f8c3299616.png)  

For a certificate to get signed by a certificate authority, we need to:

1. Generate Certificate Signing Request (CSR): You create a certificate and send your public key to be signed by a third party.
2. Send your CSR to a Certificate Authority (CA): The purpose is for the CA to sign your certificate. The alternative and usually insecure solution would be to self-sign your certificate.

For this to work, the recipient should recognize and trust the CA that signed the certificate. And as we would expect, our browser trusts DigiCert Inc as a signing authority; otherwise, it would have issued a security warning instead of proceeding to the requested website.

![Screenshot showing the certificate authorities trusted by a web browser](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/0892193b8b3defdc3cedbc1dcf1843a8.png)  

You can use `openssl` to generate a certificate signing request using the command `openssl req -new -nodes -newkey rsa:4096 -keyout key.pem -out cert.csr`. We used the following options:

- `req -new` create a new certificate signing request
- `-nodes` save private key without a passphrase
- `-newkey` generate a new private key
- `rsa:4096` generate an RSA key of size 4096 bits
- `-keyout` specify where to save the key
- `-out` save the certificate signing request

Then you will be asked to answer a series of questions, as shown in the console output below.

![[Pasted image 20240318190717.png]]

Once the CSR file is ready, you can send it to a CA of your choice to get it signed and ready to use on your server.

Once the client, i.e., the browser, receives a signed certificate it trusts, the SSL/TLS handshake takes place. The purpose would be to agree on the ciphers and the secret key.

We have just described how PKI applies to the web and SSL/TLS certificates. A trusted third party is necessary for the system to be scalable.

For testing purposes, we have created a self-signed certificate. For example, the following command will generate a self-signed certificate.

`openssl req -x509 -newkey -nodes rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365`

The `-x509` indicates that we want to generate a self-signed certificate instead of a certificate request. The `-sha256` specifies the use of the SHA-256 digest. It will be valid for one year as we added `-days 365`.

To answer the questions below, you need to inspect the certificate file `cert.pem` in the `task06` directory. You can use the following command to view your certificate:

`openssl x509 -in cert.pem -text`

Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task06`; alternatively, you can use the task file from Task 2 to work on your own machine.

| Question                                    | Answer |
| ------------------------------------------- | ------ |
| What is the size of the public key in bits? | 4096   |
```
openssl x509 -in cert.pem -text | less
```


| Question                                   | Answer |
| ------------------------------------------ | ------ |
| Till which year is this certificate valid? | 2039   |
