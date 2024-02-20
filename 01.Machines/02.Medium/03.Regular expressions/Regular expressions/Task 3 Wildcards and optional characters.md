The wildcard that is used to match any single character (except the line break) is the `.` dot. That means that `a.c` will match `aac`, `abc`, `a0c`, `a!c`, and so on.

Also, you can set a character as optional in your pattern using the `?` question mark. That means that `abc?` will match `ab` and `abc`, since the `c` is optional.

Note: If you want to search for `.` a literal dot, you have to **escape it** with a `\` reverse slash. That means that `a.c` will match `a.c`, but also `abc`, `a@c`, and so on. But `a\.c` will match **just** `a.c`.

Answer the questions below

| Question                                                               | Answer |
| ---------------------------------------------------------------------- | ------ |
| Match all of the following words: Cat, fat, hat, rat                   | .at       |
| Match all of the following words: Cat, cats                            | [cC]ats?       |
| Match the following domain name: cat.xyz                               | cat\.xyz       |
| Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz   | [ch]ats?\.xyz       |
| Match every 4-letter string that doesn't end in any letter from n to z | ...[^n-z]       |
| Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)                                                                       | [^r]ats?       |
