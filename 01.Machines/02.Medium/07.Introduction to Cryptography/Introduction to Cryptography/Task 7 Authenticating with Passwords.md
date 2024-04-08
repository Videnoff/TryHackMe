Let’s see how cryptography can help increase password security. With PKI and SSL/TLS, we can communicate with any server and provide our login credentials while ensuring that no one can read our passwords as they move across the network. This is an example of protecting data in transit. Let’s explore how we can safeguard passwords as they are saved in a database, i.e., data at rest.

The least secure method would be to save the username and the password in a database. This way, any data breach would expose the users’ passwords. No effort is required beyond reading the database containing the passwords.

|Username|password|
|---|---|
|`alice`|`qwerty`|
|`bob`|`dragon`|
|`charlie`|`princess`|

The improved approach would be to save the username and a hashed version of the password in a database. This way, a data breach will expose the hashed versions of the passwords. Since a hash function is irreversible, the attacker needs to keep trying different passwords to find the one that would result in the same hash. The table below shows the MD5 sum of the passwords. (We chose MD5 just to keep the password field small for the example; otherwise, we would have used SHA256 or something more secure.)

|Username|Hash(Password)|
|---|---|
|`alice`|`d8578edf8458ce06fbc5bb76a58c5ca4`|
|`bob`|`8621ffdbc5698829397d97767ac13db3`|
|`charlie`|`8afa847f50a716e64932d995c8e7435a`|

The previous approach looks secure; however, the availability of rainbow tables has made this approach insecure. A **rainbow table** contains a list of passwords along with their hash value. Hence, the attacker only needs to look up the hash to recover the password. For example, it would be easy to look up `d8578edf8458ce06fbc5bb76a58c5ca4` to discover the original password of `alice`. Consequently, we need to find more secure approaches to save passwords securely; we can add salt. A **salt** is a random value we can append to the password before hashing it. An example is shown below.

|Username|Hash(Password + Salt)|Salt|
|---|---|---|
|`alice`|`8a43db01d06107fcad32f0bcfa651f2f`|`12742`|
|`bob`|`aab2b680e6a1cb43c79180b3d1a38beb`|`22861`|
|`charlie`|`3a40d108a068cdc8e7951b82d312129b`|`16056`|

The table above used `hash(password + salt)`; another approach would be to use `hash(hash(password) + salt)`. Note that we used a relatively small salt along with the MD5 hash function. We should switch to a (more) secure hash function and a large salt for better security if this were an actual setup.

Another improvement we can make before saving the password is to use a key derivation function such as PBKDF2 (Password-Based Key Derivation Function 2). PBKDF2 takes the password and the salt and submits it through a certain number of iterations, usually hundreds of thousands.

We recommend you check the [Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) if you like to learn about other techniques related to password storage.

Answer the questions below

| Question                                                                                                                                                     | Answer    | SS                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | ------------------------------------ |
| You were auditing a system when you discovered that the MD5 hash of the admin password is `3fc0a7acf087f549ac2b266baf94b8b1`. What is the original password? | qwerty123 | ![[Pasted image 20240318191359.png]] |
