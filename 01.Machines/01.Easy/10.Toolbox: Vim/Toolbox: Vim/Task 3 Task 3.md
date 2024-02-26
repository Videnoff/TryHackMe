First of all,

Congratulations!

You can now type in, utilise functions of and move around in a Vim document! Congratulations. You're now an order of magnitude more capable than you were before! Remember, repetition is key so keep going! 

**Now lets learn how to exit vim...**

There are six ways to exit vim, hold on, don't run away. They are:  

- write the file, but don't exit [equivalent to save]
- ^ as root 
- write and quit [equivalent to save and exit]
- quit [fails if there is unsaved changes]
- force quit [will exit with unsaved changes]
- save and quit [all active tabs]

  

**Guide**

I suggest making a small learning directory, and writing a few small documents, in Vim of course, to test these out on- if you get stuck, there's the help guide outlined in the last task- or you can use google. 

Answer the questions below

| Question                                           | Answer |
| -------------------------------------------------- | ------ |
| How do we write the file, but don't exit?          | :w       |
| How do we write the file, but don't exit- as root? | :w !sudo tee %       |
| How do we write and quit?                          | :wq       |
| How do we quit?                                    | :q       |
| How do we force quit?                              | :q!       |
| How do we save and quit, for all active tabs?                                                   | :wqa       |
