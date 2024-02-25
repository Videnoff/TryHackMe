  
![](https://i.ibb.co/k2DgyGg/carbon-19.png)  

  

When we talk about conditionals it means that a certain piece of code relies on a condition being met, this is often determined with relational operators, such as equal to, greater than, and less than.

  

We will make a simple "if" statement to check if a variable is equal to a value, we will also make a script that checks if a file exists and that it is writeable, if it is we will write a message to that file, if not writeable it will delete it and make a new one. A Lot of new things will be taught here so pay attention.

  

First, we will discuss the basic syntax of an if statement.

All if statements look like so:
                                                                        ![](https://i.ibb.co/RBNwXHX/carbon-15.png)

  

  

Let's look at an example:
                                                                       ![](https://i.ibb.co/34LR4sT/carbon-16.png)

  

  

If statements always use a pair of brackets and in the case of the [] we need to leave a space on both sides of the text(the bash syntax). We also always need to end the if statement with `fi`

  

Here a variable is being declared as 10 and in the top line of the if statement the variable $count is being compared to the integer 10.

If they are equal then it outputs **true**, if its false it outputs **false**. As we know 10 is equal to 10 so it outputs true.

The **-eq** is one way of doing this, you could also use “**=**”

  

| Operator | Description |
| ---- | ---- |
| -eq | Checks if the value of two operands are equal or not; if yes, then the condition becomes true. |
| -ne | Checks if the value of two operands are equal or not; if values are not equal, then the condition becomes true. |
| -gt | Checks if the value of left operand is greater than the value of right operand; if yes, then the condition becomes true. |
| -lt | Checks if the value of left operand is less than the value of right operand; if yes, then the condition becomes true. |
| -ge | Checks if the value of left operand is greater than or equal to the value of right operand; if yes, then the condition becomes true. |

^^^^^ These are some examples.

  

So now let's use this to make a little script that compares an input(a parameter) and checks it against a value to check if it's true or not. A guessing game if you will.
                                                                         ![](https://i.ibb.co/R9gvH5J/carbon-17.png)

  

  

Now let's test this in our terminal.

`# ./example.sh guessme`

`"They are equal"`

`# ./example.sh hi`

`"They are not equal"`

And we can see that it works!

Feel free to play around with these and try making different combinations and using different operators.

  

Now let's create another script where we will use 2 conditions simultaneously and coming back to a concept we learnt in the first lesson.

Let's begin.

We want to make a script that we will perform on a file given by a **parameter**.

We then check if it exists and if it has **write** permissions. If it has write perms then we echo “**hello**” to it. If it is either non-accessible or doesn't exist we will create the file and echo “hello” to it. Let's begin!
                                                                        ![](https://i.ibb.co/k2DgyGg/carbon-19.png)  

  

`─# ./example.sh hello.txt                                                                                                                ─# cat hello.txt`

hello

And we can see that it worked!!

The **-f** checked if the file existed.

The **-w** checked if the file was writable, without write permissions we wouldn't be able to output our text into the file.

  

To finish off our little project from the previous task. You can build on your script using an if/else statement. Test to see if the age is under 18, if it is then echo out their name with "You are not eligible for work" or something along these lines, if they are over 18 then ask them for their job, you can do this with `read`

Feel free to add anything you like and make it as complicated as you wish and good luck with your project!

Answer the questions below

| Question                                                    | Answer |
| ----------------------------------------------------------- | ------ |
| What is the flag to check if we have read access to a file? | -r       |
| What is the flag to check to see if it's a directory?                                                            | -d       |
