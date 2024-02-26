Lets get used to using Vim for basic text editing...

**Modes**  

There are three basic modes in Vim:

- Command mode is where you can run commands. This is the default mode in which Vim starts up
- Insert mode is where you insert i.e. write the text  
    
- Visual mode is where you visually select a bunch of text so that you can run a command/operation only on that part of the text.

These form the pillars of navigating and using Vim. Try and answer the questions and work out how to begin creating a basic text document in Vim.

**Navigation**  

Now that you know how to start creating a text document, you're going to need to know how to navigate it.

- left
- right
- up
- down
- jump to the start of a word
- jump to the end of a word

Hint, focus on key clusters, not combinations of keys for this.

**Inserting Text**

Now you're comfortable in basic typing and navigating the document, lets get into using vim in a more powerful way!

The shortcuts for appending and inserting are crucial, I suggest trying to implement them into your typing routine so that they really stick.

  

FOR HELP WITH THE QUESTIONS

The easiest way to ask for help is to start with executing :help during a Vim session. This will drop us into the main help file which has an overview of the basics.

To get help with a specific command, we can provide that command as an argument to the :help command. By invoking :help gg, we learn more details about gg including that *C-home* does the same thing and that by providing a [count], we can use gg to jump anywhere in a file.


Answer the questions below

| Question                                                 | Answer |
| -------------------------------------------------------- | ------ |
| How do we enter "INSERT" mode?                           | i       |
| How do we start entering text into our new Vim document? | typing       |
| How do we return to command mode?                        | esc       |
| How do we move the cursor left?                          | h       |
| How do we move the cursor right?                         | l       |
| How do we move the cursor up?                            | k       |
| How do we move the cursor down?                          | j       |
| How do we jump to the start of a word?                   | w       |
| How do we jump to the end of a word?                     | e       |
| How do we insert (before the cursor)                     | i       |
| How do we insert (at the beginning of the line?)         | I       |
| How do we append (after the cursor)                      | a       |
| How do we append (at the end of the line)                | A       |
| How do we make a new line under the current line?                                                         | o       |
