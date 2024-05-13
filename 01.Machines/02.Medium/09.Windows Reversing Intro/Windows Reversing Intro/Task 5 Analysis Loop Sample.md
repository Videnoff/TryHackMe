**When running the samples on their own, outside of IDA, run them via the command line.**

It's highly encouraged to follow along for this portion in your own VM, as it will make it must easier for you to understand. This task uses _Loop.exe_. Load it into IDA and go to the main() function. The graph view is highly recommended.

I'm also going to state now and multiple times to keep the bigger picture in mind. Don't analyze one instruction at a time, it usually requires multiple instructions to perform one high-level action. It's also important to point out that we will be making assumptions. You won't always know what something is or does, which is why you make your best guess. As you go, use your guess to attempt to understand what's going on while at the same time validating/testing your guess.

At a high level there are three main types of loops used: For, While, and Do-While. When working on a low level you'll usually see a do-while and sometimes a while. Keep in mind that a for loop is only an abstracted while loop. When dealing with loops expect to see a counter/iterator register initialized at the beginning and incremented/decremented at the end. The condition for the loop is usually at the end since that's when you would determine whether or not to continue the loop. There is often a condition at the start as well which would be a check to skip the entire loop. There may also be conditions within the loop that break/jump out of the loop.

## Reversing Our First Loop

Before we throw it into IDA, as always you should run it. After running it the purpose seems to be to get input from the user and count the number of lowercase characters then output the result. Simple enough, you could probably guess how it works without having to do any reversing, but let's take a look so we can learn since it won't always be that easy.

Go ahead and load _Loop.exe_ into IDA and go main(). You may notice it's quite large. I would encourage you to use graph view, it makes understanding the flow of the program much easier. Once again, press _Space_ to quickly switch between the graph view and the listing view.

#### Initial Analysis

To start let me introduce you to the best skill to develop as a reverse engineer. It's being able to skim over the unimportant stuff otherwise you'll waste your time and go into a rabbit hole. In the graph view, we can see a big box at the top. Looking at it we can see that it mostly just prints stuff so we can skim through it just to make sure there's nothing important. Looking towards the bottom of the big box, which I will refer to as the loop initialization part of the code, we can see some interesting stuff.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/c589119cfccf744d193afacced918896.png)  

The reason why it's interesting is for two main reasons. First, it doesn't appear to be printing anything like the previous lines were. Second, there's a loop following it which we can quickly identify because of the arrows provided in graph view. Let's start our analysis by taking a look at `mov rsi, [rsp+58h+var_20]` since it seems to be the start of the difference. **Important:** Don't forget about the code we just skimmed over. If we get lost or need more information (foreshadowing) one of the first things we'll do is go back to the code we skimmed over.  

Looking at the move into RSI, RDI, and RDX we don't get much since the data is uninitialized. Notice the `test RDX, RDX` as it can reveal a little extra. Testing a register against itself will test if the register is zero. In this case, if RDX is zero it jumps past the loop because of `jz short loc_140001332`. Based on this we know that RDX shouldn't be zero, since if it is, it appears to fail/skip the loop. Since we are iterating over input we can guess RDX is most likely the length of the string, but it could also be checking if a buffer is empty. One of the nice things about IDA is it can determine if data is a buffer or just a normal data type such as an integer. You can see that two of the moves involve var_##, and another uses rsp+58h+Block. This means that the move into RDI involves a buffer and the moves into RSI and RDX are normal data types. We can now solidify our guess that RDX is the length of the string since the loop is likely to be iterating over the string. We'll keep this in mind as we move forward to both verify our guess and better understand what the loop is doing.  

#### Analyzing The Loop

The first thing I like to do is go to the end of the loop to identify the register being used as the counter and the end case for the loop. **The key to finding the counter is identifying the register which gets incremented or decremented.** The end case for the loop can be identified by a comparison to the counter.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/910b9d301441ef6a0a30270a3df34214.png)  

At the bottom, you can see RCX being incremented then compared to RDX. In other words, the counter is compared to what we assume is the length of the string. Now we know RCX is the counter and the condition between RCX and RDX is the end condition. This also solidifies that RDX is the length of the string.  

Now let's look at the first block involved in the loop.

**Loop Block 1**  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/3fe0362521d7e7ccf8b22c91cff107f7.png)  

Once again, you must try to understand multiple instructions together since they likely come together to perform one task.  

We see the _address_ of the buffer (identified because of "Block") being put into RAX, so RAX is how the string will be referenced in the loop.  

What's this weird RSI comparison and the `cmovnb`? The `cmovnb` instruction is a conditional move if not below. This is saying move RBX into RAX if RSI is not less than 0x10. You could also think of it as if RSI is greater than or equal to 0x10.  

- Let's find out what RDI is. In the initialization block (the big one) at the bottom, we see that the string buffer is moved into RDI (`mov rdi, [rsp+58h+Block]`). Since RDI is 8 bytes, the first 8 bytes of the buffer are moved into RDI. Note that, unlike RAX, RDI does not contain the address of the buffer. RAX was given the address because of the `lea` instruction whereas RDI is given the first 8 bytes (based on the size of the RDI register) of data within the buffer because of a `mov` instruction.  
    
- Now for RSI. We can see at the bottom of the initialization block that RSI is set to an unknown value (`mov rsi, [rsp+58h+var_20]`). Keep looking to find what modifies that variable and you will see towards the middle of the first block that it's initialized to 0xF (`mov [rsp+58h+var_20], 0Fh`). Unless RSI or RSP+58h+var_20 are modified elsewhere, the `cmovnb` will never occur since 0xF _is_ below 0x10.
- So what exactly is all of this doing since it doesn't appear to be related to the loop? We will come back to this, for now since it doesn't seem to affect the loop we will ignore it.

Next, there is a comparison between RAX+RCX and 0x61 (ASCII "a") then a jump if less than. This is getting an offset in the string with the distance being the loop counter (RCX). The RAX+RCX is the same as string[index] or RAX[RCX] in a high-level language, where RCX is the index/offset that is added to the base address of the string contained in RAX. Now let's break that down in a more understandable way. It will compare the current character in the string being iterated over against the character "a". If the current character is less than "a" it will skip to the final block in the loop which will start the next iteration. Otherwise, it will continue to the second block. So the good outcome, in this case, is that the character is greater than or equal to "a" since it wouldn't skip to the end of the loop.

Once again remember the bigger picture. The goal of this program is to count lowercase characters. The behavior we just analyzed makes sense, a lowercase character is not going to be less than the ASCII value of 0x61.  

**Part 2**  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/1e80c37be90f7b9a26f1c2b85b8fd22b.png)  

The second block does almost the same thing as the first, except it compares the current character against "z". If it's greater than then it will jump to the end. However, there is something very important that is easy to skip. Notice RBX is incremented. The condition in which RBX is incremented is if the current character is _not_ less than "a", and _not_ greater than "z". In other words, if it's a lower case character (a-z) RBX is incremented! So RBX is going to hold the result of how many characters are lower case.

Finally, at the end of the loop, the loop counter (RCX) is incremented then compared to the length of the string (RDX) and jumps if below to the start of the loop. Otherwise, it continues to the code after the loop.

**Part 3  
**

Now to look at the rest of the function to see what else there is and maybe find out what was going on with RSI and all of that `cmovnb` business. First look at the big block after the loop.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/1763873139b63372893c7e9ec1ca3ac4.png)  

It appears it is printing the results out as seen when we ran the program. Towards the bottom of the block we see something familiar though, a comparison between RSI and 0x10. If RSI is less than 0x10, it will jump to the function epilogue. Based on this we can assume that RSI and 0x10 have something to do with error handling, possibly input validation or parameter validation. Looking further at the few small blocks at the end of the function it seems the assumption is correct.

  
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/3c0519a6df526993aba847023492fbd7.png)

It further compares RSI and we can see functions related to invalid parameters and freeing memory. Remember earlier when I said a good reverse engineer knows when to skip stuff, this is that time. RSI doesn't seem to be tied to the loop or user input, instead, it appears to be generated by the compiler. Because of this, we will avoid the rabbit hole and not dig deep into it, however, feel free to do so if you'd like.

That's all there is to it! With enough practice and experience, this sort of task could take you a mere few seconds. As a beginner, this sort of thing can be a bit confusing, which is why we broke it down. Ironically, breaking it down can sometimes make it harder to understand which is why it's vital to keep the big picture in mind, analyze multiple related instructions together, and make guesses when you need to. Of course, be prepared for your guess to be wrong.  

Answer the questions below

| Question                                                                                                                                                                                | Answer  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| In the Loop.exe sample, what instruction is the key to finding out what register is the counter? Provide the full instruction as shown in IDA, with single spaces. For example: dec RAX | inc rcx |
