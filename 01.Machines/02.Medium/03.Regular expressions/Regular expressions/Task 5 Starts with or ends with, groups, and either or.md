Sometimes it's very useful to specify that we want to search by a certain pattern **in the beginning or the end of a line**. We do that with these characters:  
`^` - starts with  
`$` - ends with

So for example, if you want to search for a line that **starts with** `abc`, you can use `^abc`.  
If you want to search for a line that **ends with** `xyz`, you can use `xyz$`.

Note: The `^` hat symbol is used to exclude a charset when enclosed in `[`square brackets`]`, but when it is not, it is used to specify the beginning of a word.

You can also define groups by enclosing a pattern in `(`parentheses`)`. This function can be used for many ways that are not in the scope of this tutorial. We will use it to define an **either/ or** pattern, and also to repeat patterns. To say "or" in Regex, we use the `|` pipe.

For an "either/or" pattern example, the pattern `during the (day|night)` will match both of these sentences: `during the day` and `during the night`.  
For a repetition example, the pattern `(no){5}` will match the sentence `nonononono`.

Answer the questions below

| Question                                                                                                                                                                                                                                                                        | Answer                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Match every string that starts with "Password:" followed by any 10 characters excluding "0"                                                                                                                                                                                     | Password:[^0]{10}     |
| Match "username: " in the beginning of a line (note the space!)                                                                                                                                                                                                                 | username:\s           |
| Match every line that doesn't start with a digit (use a metacharacter)                                                                                                                                                                                                          | ^\d                   |
| Match this string at the end of a line: EOF$                                                                                                                                                                                                                                    | EOF\$$                |
| Match all of the following sentences:<br><br>- I use nano<br>- I use vim                                                                                                                                                                                                        | I use (nano\|vim)     |
| Match all lines that start with $, followed by any single digit, followed by $, followed by one or more non-whitespace characters                                                                                                                                               | \$\d\$\S+             |
| Match every possible IPv4 IP address (use metacharacters and groups)                                                                                                                                                                                                            | (\d{1,3}\.){3}\d{1,3} |
| Match all of these emails while also adding the username and the domain name (not the TLD) in separate groups (use \w): [hello@tryhackme.com](mailto:hello@tryhackme.com), [username@domain.com](mailto:username@domain.com), [dummy_email@xyz.com](mailto:dummy_email@xyz.com) | (\w+)@(\w+)\.com      |
