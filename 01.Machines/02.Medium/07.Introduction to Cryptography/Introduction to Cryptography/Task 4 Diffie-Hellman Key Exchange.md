Alice and Bob can communicate over an insecure channel. By insecure, we mean that there are eavesdroppers who can read the messages exchanged on this channel. How can Alice and Bob agree on a secret key in such a setting? One way would be to use the Diffie-Hellman key exchange.

Diffie-Hellman is an asymmetric encryption algorithm. It allows the exchange of a secret over a public channel. We will skip the modular arithmetic background and provide a simple numeric example. We will need two mathematical operations: power and modulus. _x__p_, i.e., _x_ raised to the power _p_, is _x_ multiplied by itself _p_ times. Furthermore, _x_ mod _m_, i.e., _x_ modulus _m_, is the remainder of the division of _x_ by _m_.

1. Alice and Bob agree on _q_ and _g_. For this to work, _q_ should be a prime number, and _g_ is a number smaller than _q_ that satisfies certain conditions. (In modular arithmetic, _g_ is a generator.) In this example, we take _q_ = 29 and _g_ = 3.
2. Alice chooses a random number _a_ smaller than _q_. She calculates _A_ = (_g__a_) mod _q_. The number _a_ must be kept a secret; however, _A_ is sent to Bob. Let’s say that Alice picks the number _a_ = 13 and calculates _A_ = 313%29 = 19 and sends it to Bob.
3. Bob picks a random number _b_ smaller than _q_. He calculates _B_ = (_g__b_) mod _q_. Bob must keep _b_ a secret; however, he sends _B_ to Alice. Let’s consider the case where Bob chooses the number _b_ = 15 and calculates _B_ = 315%29 = 26. He proceeds to send it to Alice.
4. Alice receives _B_ and calculates _k__e__y_ = _B__a_ mod _q_. Numeric example _k__e__y_ = 2613 mod 29 = 10.
5. Bob receives _A_ and calculates _k__e__y_ = _A__b_ mod _q_. Numeric example _k__e__y_ = 1915 mod 29 = 10.

We can see that Alice and Bob reached the same key.

Although an eavesdropper has learned the values of _q_, _g_, _A_, and _B_, they won’t be able to calculate the secret _k__e__y_ that Alice and Bob have exchanged. The above steps are summarized in the figure below.

![Graphical illustration showing a numeric example of the five steps of Diffie-Hellman](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/6993f1edbc899d252e949ac403294d52.png)  

Although the numbers we have chosen make it easy to find _a_ and _b_, even without using a computer, real-world examples would select a _q_ of 256 bits in length. In decimal numbers, that’s 115 with 75 zeroes to its right (I don’t know how to read that either, but I was told it is read as 115 quattuorvigintillion). Such a large _q_ will make it infeasible to find _a_ or _b_ despite knowledge of _q_, _g_, _A_, and _B_.

Let’s take a look at actual Diffie-Hellman parameters. We can use `openssl` to generate them; we need to specify the option `dhparam` to indicate that we want to generate Diffie-Hellman parameters along with the specified size in bits, such as `2048` or `4096`.

In the console output below, we can view the prime number `P` and the generator `G` using the command `openssl dhparam -in dhparams.pem -text -noout`. (This is similar to what we did with the RSA private key.)

![[Pasted image 20240317221006.png]]

Diffie-Hellman key exchange algorithm allows two parties to agree on a secret over an insecure channel. However, the discussed key exchange is prone to a Man-in-the-Middle (MitM) attack; an attacker might reply to Alice pretending to be Bob and reply to Bob pretending to be Alice. We discuss a solution to this problem in Task 6.

Answer the questions below

On the AttackBox, you can find the directory for this task located at `/root/Rooms/cryptographyintro/task04`; alternatively, you can use the task file from Task 2 to work on your own machine.


| Question                                                                                                                 | Answer |
| ------------------------------------------------------------------------------------------------------------------------ | ------ |
| A set of Diffie-Hellman parameters can be found in the file `dhparam.pem`. What is the size of the prime number in bits? | 4096   |
```
openssl dhparam -in dhparams.pem -text -noout
```


| Question                                                       | Answer |
| -------------------------------------------------------------- | ------ |
| What is the prime number’s last byte (least significant byte)? | 4f     |
