This is going to be a quick introduction to how binary is manipulated and how basic mathematical operations are performed in binary. Let's start with learning what true and false mean for a computer, then we'll talk about the four fundamental operations: **NOT**, **AND**, **OR**, and **XOR**.

**True / False  
**

In computing, false is represented with the value 0, and true is represented as anything _other than_ 0. This is why in binary true is 1 and false is 0. When programming true could be, 1, 100, a memory address, or a character. Again, true is anything other than 0.

**NOT (Shown as "!")**  
The NOT operation will simply flip the bit.

- NOT 1 = 0
- NOT 0 = 1

![](https://raw.githubusercontent.com/0xZ0F/Z0FCourse_ReverseEngineering/master/Chapter%202%20-%20BinaryBasics/%5Bignore%5D/BONot.png)

**AND (Shown as "&")**  

AND will check if both bits are 1 and if they are the result will be 1, otherwise, the result is 0.

- 1 AND 1 = 1
- 1 AND 0 = 0
- 0 AND 0 = 0

![](https://raw.githubusercontent.com/0xZ0F/Z0FCourse_ReverseEngineering/master/Chapter%202%20-%20BinaryBasics/%5Bignore%5D/BOAnd.png)

**OR (Shown as "|")**  

OR will check if one of the bits is one and if so, then the result is 1, otherwise, the result is 0.

- 1 OR 1 = 1
- 1 OR 0 = 1
- 0 OR 0 = 0

![](https://raw.githubusercontent.com/0xZ0F/Z0FCourse_ReverseEngineering/master/Chapter%202%20-%20BinaryBasics/%5Bignore%5D/BOOr.png)

**XOR (Shown as "^")**  

The result is 1 if either of the bits is one, **but not both**, otherwise, the result is 0. Another way to think of XOR is it's checking if the bits are different.  

- 1 XOR 1 = 0
- 1 XOR 0 = 1
- 0 XOR 0 = 0

![](https://raw.githubusercontent.com/0xZ0F/Z0FCourse_ReverseEngineering/master/Chapter%202%20-%20BinaryBasics/%5Bignore%5D/BOXor.png)

  

There are inverses of these operations, such as NAND and NOR. These operations perform the respective primary operation then perform a NOT at the end. For example, NAND performs an AND operation followed by a NOT operation on the result of the AND operation.  

Answer the questions below

| Question                                                                              | Answer |
| ------------------------------------------------------------------------------------- | ------ |
| What is the result of the binary operation: 1011 AND 1100?                            | 1000   |
| What is the result of the binary operation: 1011 NAND 1100? _Include_ leading zeroes. | 0111   |
