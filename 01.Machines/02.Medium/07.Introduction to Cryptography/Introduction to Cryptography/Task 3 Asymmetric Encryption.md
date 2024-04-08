Symmetric encryption requires the users to find a secure channel to exchange keys. By secure channel, we are mainly concerned with confidentiality and integrity. In other words, we need a channel where no third party can eavesdrop and read the traffic; moreover, no one can change the sent messages and data.

Asymmetric encryption makes it possible to exchange encrypted messages without a secure channel; we just need a reliable channel. By reliable channel, we mean that we are mainly concerned with the channel’s integrity and not confidentiality.

When using an asymmetric encryption algorithm, we would generate a key pair: a public key and a private key. The public key is shared with the world, or more specifically, with the people who want to communicate with us securely. The private key must be saved securely, and we must never let anyone access it. Moreover, it is not feasible to derive the private key despite the knowledge of the public key.

How does this key pair work?

If a message is encrypted with one key, it can be decrypted with the other. In other words:

- If Alice encrypts a message using Bob’s public key, it can be decrypted only using Bob’s private key.
- Reversely, if Bob encrypts a message using his private key, it can only be decrypted using Bob’s public key.

### Confidentiality

We can use asymmetric encryption to achieve confidentiality by encrypting the messages using the recipient’s public key. In the following two figures, we can see that:

Alice wants to ensure confidentiality in her communication with Bob. She encrypts the message using Bob’s public key, and Bob decrypts them using his private key. Bob’s public key is expected to be published on a public database or on his website, for instance.

![When using asymmetric encryption, Alice encrypts the messages using Bob's public key before sending them to Bob. Bob decrypts the messages using his private key.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/684696712007bfb81595bc823deb6293.png)  

When Bob wants to reply to Alice, he encrypts his messages using Alice’s public key, and Alice can decrypt them using her private key.

![When using asymmetric encryption, Bob encrypts the messages using Alice's public key before sending them to Alice. Alice decrypts the messages using her private key.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/321e8f02228699aab1a333791fe57d4a.png)  

In other words, it becomes easy to communicate with Alice and Bob while ensuring the confidentiality of the messages. The only requirement is that all parties have their public keys available for interested senders.

Note: In practice, symmetric encryption algorithms allow faster operations than asymmetric encryption; therefore, we will cover later how we can use the best of both worlds.

### Integrity, Authenticity, and Nonrepudiation

Beyond confidentiality, asymmetric encryption can solve integrity, authenticity and nonrepudiation. Let’s say that Bob wants to make a statement and wants everyone to be able to confirm that this statement indeed came from him. Bob needs to encrypt the message using his private key; the recipients can decrypt it using Bob’s public key. If the message decrypts successfully with Bob’s public key, it means that the message was encrypted using Bob’s private key. (In practice, he would encrypt a hash of the original message. We will elaborate on this later.)

Being decrypted successfully using Bob’s public key leads to a few interesting conclusions.

- First, the message was not altered across the way (communication channel); this proves the message _integrity_.
- Second, knowing that no one has access to Bob’s private key, we can be sure that this message did indeed come from Bob; this proves the message _authenticity_.
- Finally, because no one other than Bob has access to Bob’s private key, Bob cannot deny sending this message; this establishes _nonrepudiation_.

![To prove authenticity using asymmetric encryption, Bob encrypts the message using his private key and the recipients can decrypt it using Bob’s public key.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/11329c3e017fe2016fc21bc789b29259.png)  

We have seen how asymmetric encryption can help establish confidentiality, integrity, authenticity, and nonrepudiation. In real-life scenarios, asymmetric encryption can be relatively slow to encrypt large files and vast amounts of data. In another task, we will see how we can use asymmetric encryption in conjunction with symmetric encryption to achieve these security objectives relatively faster.

### RSA

RSA got its name from its inventors, Rivest, Shamir, and Adleman. It works as follows:

1. Choose two random prime numbers, _p_ and _q_. Calculate _N_ = _p_ × _q_.
2. Choose two integers _e_ and _d_ such that _e_ × _d_ = 1 mod _ϕ_(_N_), where _ϕ_(_N_) = _N_ − _p_ − _q_ + 1. This step will let us generate the public key (_N_,_e_) and the private key (_N_,_d_).
3. The sender can encrypt a value _x_ by calculating _y_ = _x__e_ mod _N_. (Modulus)
4. The recipient can decrypt _y_ by calculating _x_ = _y__d_ mod _N_. Note that _y__d_ = _x__e__d_ = _x__k__ϕ_(_N_) + 1 = (_x__ϕ_(_N_))_k_ × _x_ = _x_. This step explains why we put a restriction on the choice of _e_ and _d_.

Don’t worry if the above mathematical equations looked too complicated; you don’t need mathematics to be able to use RSA, as it is readily available via programs and programming libraries.

RSA security relies on factorization being a hard problem. It is easy to multiply _p_ by _q_; however, it is time-consuming to find _p_ and _q_ given _N_. Moreover, for this to be secure, _p_ and _q_ should be pretty large numbers, for example, each being 1024 bits (that’s a number with more than 300 digits). It is important to note that RSA relies on secure random number generation, as with other asymmetric encryption algorithms. If an adversary can guess _p_ and _q_, the whole system would be considered insecure.

Let’s consider the following practical example.

1. Bob chooses two prime numbers: _p_ = 157 and _q_ = 199. He calculates _N_ = 31243.
2. With _ϕ_(_N_) = _N_ − _p_ − _q_ + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects _e_ = 163 and _d_ = 379 where _e_ × _d_ = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (31243,163) and the private key is (31243,379).
3. Let’s say that the value to encrypt is _x_ = 13, then Alice would calculate and send _y_ = _x__e_ mod _N_ = 13163 mod 31243 = 16342.
4. Bob will decrypt the received value by calculating _x_ = _y__d_ mod _N_ = 16341379 mod 31243 = 13.

The previous example was to understand the mathematics behind it better. To see real values for _p_ and _q_, let’s create a real keypair using a tool such as `openssl`.

![[Pasted image 20240317201951.png]]

We executed three commands:

- `openssl genrsa -out private-key.pem 2048`: With `openssl`, we used `genrsa` to generate an RSA private key. Using `-out`, we specified that the resulting private key is saved as `private-key.pem`. We added `2048` to specify a key size of 2048 bits.
- `openssl rsa -in private-key.pem -pubout -out public-key.pem`: Using `openssl`, we specified that we are using the RSA algorithm with the `rsa` option. We specified that we wanted to get the public key using `-pubout`. Finally, we set the private key as input using `-in private-key.pem` and saved the output using `-out public-key.pem`.
- `openssl rsa -in private-key.pem -text -noout`: We are curious to see real RSA variables, so we used `-text -noout`. The values of _p_, _q_, _N_, _e_, and _d_ are `prime1`, `prime2`, `modulus`, `publicExponent`, and `privateExponent`, respectively.

If we already have the recipient’s public key, we can encrypt it with the command `openssl pkeyutl -encrypt -in plaintext.txt -out ciphertext -inkey public-key.pem -pubin`

The recipient can decrypt it using the command `openssl pkeyutl -decrypt -in ciphertext -inkey private-key.pem -out decrypted.txt`

Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task03`; alternatively, you can use the task file from Task 2 to work on your own machine.

| Question                                                                                                                                                                   | Answer     |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| Bob has received the file `ciphertext_message` sent to him from Alice. You can find the key you need in the same folder. What is the first word of the original plaintext? | Perception |
```
openssl pkeyutl -decrypt -in ciphertext_message -inkey private-key-bob.pem -out decrypted_bob.txt
```



| Question                                                            | Answer |
| ------------------------------------------------------------------- | ------ |
| Take a look at Bob’s private RSA key. What is the last byte of _p_? | e7     |
```
openssl rsa -in private-key-bob.pem -text -noout
```


| Question                                                            | Answer |
| ------------------------------------------------------------------- | ------ |
| Take a look at Bob’s private RSA key. What is the last byte of _q_? | 27     |
```
openssl rsa -in private-key-bob.pem -text -noout
```
