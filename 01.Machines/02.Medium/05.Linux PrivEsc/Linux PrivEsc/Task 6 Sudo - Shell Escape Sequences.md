List the programs which sudo allows your user to run:

```
sudo -l
```

![[Pasted image 20240219222843.png]]

Visit GTFOBins ([https://gtfobins.github.io](https://gtfobins.github.io)) and search for some of the program names. If the program is listed with "sudo" as a function, you can use it to elevate privileges, usually via an escape sequence.

Choose a program from the list and try to gain a root shell, using the instructions from GTFOBins.

For an extra challenge, try to gain a root shell using all the programs on the list!

Remember to exit out of the root shell before continuing!  

Answer the questions below

| Question                                                                               | Answer  |
| -------------------------------------------------------------------------------------- | ------- |
| How many programs is "user" allowed to run via sudo?                                   | 11      |
| One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it? | apache2 |
| Consider how you might use this program with sudo to gain root privileges without a shell escape sequence.                                                                                       |         |
