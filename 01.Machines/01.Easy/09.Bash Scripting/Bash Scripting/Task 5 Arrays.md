For this module i suggest you follow along in the attackbox or a standard linux terminal to make it easier to understand.

Arrays are used to store multiple pieces of data in one variable, which can then be extracted by using an index. Most commonly notated as `var[index_position]`.

Arrays use indexing meaning that each item in an array stands for a number.

In the array `['car', 'train', 'bike', 'bus']` each item has a corresponding index.

All indexes start at position 0

  

|   |   |
|---|---|
|item|index|
|car|0|
|train|1|
|bike|2|
|bus|3|

  

Now we have covered this, let's make an array in bash.  

The syntax is as follows.

  

We have the variable name, in our case ‘transport’

We then wrap each item in brackets leaving a space between each item.

`transport=('car' 'train' 'bike' 'bus')`

We can then echo out all the elements in our array like this:

`echo "${transport[@]}"`

You can try this in your own terminal and see what it outputs.

Where the "@" means all arguments, and the [] wrapped around it specifies its index.

So what if we wanted to print out the item `train`.

We would simply type:

`echo "${transport[1]}"`

because the train is at index position 1.

  

The last thing we will cover is if we want to change an element, or delete it. If we wanted to remove an element we would use the `unset` utility.

`unset transport[1]`

This now removes the `train` item, if we wanted to we could echo it back out and see that it is indeed gone,

Now lets set it to something else. We can do:

`transport[1]='trainride'`

If we echo the array then we get:

`car trainride bike bus`

  

So we successfully managed to swap out an element in our array!

  

As a little side project try building on your previous project of a biography maker, include arrays so that you can store multiple names and multiple facts about the person. Then in the next module we can expand even further.

Given the array please answer the following questions

`cars=('honda' 'audi' 'bmw' 'tesla')`  

Answer the questions below

| Question | Answer |
| ---- | ---- |
| What would be the command to print audi to the screen using indexing. | echo "${cars[1]}" |
| If we wanted to remove tesla from the array how would we do so? | unset cars[3] |
| How could we insert a new value called toyota to replace tesla? | cars[3]='toyota' |
