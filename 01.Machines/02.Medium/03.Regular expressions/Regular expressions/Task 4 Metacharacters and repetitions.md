There are easier ways to match bigger charsets. For example, `\d` is used to match any **single** digit. Here's a reference:  
`\d` matches a digit, like `9`  
`\D` matches a non-digit, like `A` or `@`  
`\w` matches an alphanumeric character, like `a` or `3`  
`\W` matches a non-alphanumeric character, like `!` or `#`  
`\s` matches a whitespace character (spaces, tabs, and line breaks)  
`\S` matches everything else (alphanumeric characters and symbols)

Note: Underscores `_` are included in the `\w` metacharacter and not in `\W`. That means that `\w` will match every single character in `test_file`.

Often we want a pattern that matches many characters of a single type in a row, and we can do that with repetitions. For example, `{2}` is used to match the preceding character (or metacharacter, or charset) two times in a row. That means that `z{2}` will match exactly `zz`.

Here's a reference for each repetition along with how many times it matches the preceding pattern:

`{12}` - **exactly 12** times.  
`{1,5}` - **1 to 5** times.  
`{2,}` - **2 or more** times.  
`*` - **0 or more** times.  
`+` - **1 or more** times.

Answer the questions below

| Question                                                                                                   | Answer  |
| ---------------------------------------------------------------------------------------------------------- | ------- |
| Match the following word: catssss                                                                          | cats{4} |
| Match all of the following words (use the * sign): Cat, cats, catsss                                       | [cC]ats*        |
| Match all of the following sentences (use the + sign): regex go br, regex go brrrrrr                       | regex go br+        |
| Match all of the following filenames: ab0001, bb0000, abc1000, cba0110, c0000 (don't use a metacharacter)  | [abc]{1,3}[01]{4}        |
| Match all of the following filenames: File01, File2, file12, File20, File99                                | [fF]ile\d{1,2}        |
| Match all of the following folder names: kali tools, kali     tools                                        | kali\s+tools        |
| Match all of the following filenames: notes~, stuff@, gtfob#, lmaoo!                                       | \w{5}\W        |
| Match the string in quotes (use the * sign and the \s, \S metacharacters): "2f0h@f0j0%!     a)K!F49h!FFOK" | \S*\s*\S        |
| Match every 9-character string (with letters, numbers, and symbols) that doesn't end in a "!" sign         | \S{8}[^!]        |
| Match all of these filenames (use the + symbol): .bash_rc, .unnecessarily_long_filename, and note1                                                                                                           | \.?\w+        |
