Onto one of the last key things about using Vim, finding and replacing patterns.

**Keep going!**

We can use Vim to search for any literal pattern in the text, allowing you to search through large text files with ease. As well as allowing for replacing of patterns, or just repeat characters / white space.

**vimgrep**

You can also use "vimgrep" to use grep inside vim, allowing you to search using grep syntax and regex if you so desire.

  

Guide

I suggest making a small learning directory, and writing a few small documents, in Vim of course, to test these out on- if you get stuck, there's the help guide outlined in the last task- or you can use google. 

Answer the questions below

| Question                                                                 | Answer |
| ------------------------------------------------------------------------ | ------ |
| How do we search forwards for a pattern (use "pattern" for your answer)  | /pattern       |
| How do we search backwards for a pattern (use "pattern" for your answer) | ?pattern       |
| How do we repeat this search in the same direction?                      | n       |
| How do we repeat this search in the opposite direction?                  | N       |
| How do we search for "old" and replace it with "new"                     | :%s/old/new/g       |
| How do we use "grep" to search for a pattern in multiple files?                                                                         | :vimgrep       |
 