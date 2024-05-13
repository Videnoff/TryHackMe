Remember how functions need stack frames? Function prologues and epilogues will set up, create, and destroy stack frames according to the calling convention in use. I will introduce them here and point them out as we encounter them on our journey.  

#### Prologue

The prologue comes before the body of a function is executed. Not all prologues are the same, but here are three things that can happen and the order they usually happen in.

1. Volatile registers are saved. If there is shadow space available, and the appropriate compilation options are chosen, the shadow space can be used to hold volatile registers. If there is no room in shadow space then registers are pushed onto the stack.
2. Space is allocated for the stack frame by subtracting from RSP. The amount subtracted from RSP can be used to determine the number of function parameters.
3. RSP or RBP may be preserved to be restored later. Since RBP isn't used much for stack purposes in x64 when it gets preserved it's likely _not_ being preserved to keep a stack address safe, rather it's being treated the same as the other volatile registers. In the case that it _is_ being used for stack purposes, you may see something along the lines of `mov RSP, RBP` which moves RSP to where RBP was at, setting up a new stack frame right next to the previous one.  
    

Generally speaking, it's fine to skim over the function prologue, however, note that it can hint at how many parameters are passed to the function.  

#### Epilogue

The epilogue is pretty straightforward, it undoes/unwinds any stack-related things, mostly caused by the prologue. The epilogue can be a nice place to double-check you didn't miss anything within the prologue, but it's generally more useless to a reverse engineer than the prologue.

You may see the following in the epilogue:

1. Addition to RSP to restore/delete the stack frame.
2. Restoring registers, usually done by popping registers off the stack which were pushed on the stack during the prologue.
3. Return.

That's all there is to most epilogues.

Quick side note, you may have heard that nothing on disk is ever actually deleted. When you delete something the OS simply marks that area on disk as not being used so the OS knows it can write to that location without overwriting anything important. This is why data removal software exists. It will go in and fill in the area with zeroes or junk data so the original data is removed. Similarly, nothing gets deleted from the stack by the prologue or epilogue. When the next stack frame is made it will be put right where the old one was and there will still be data there. This is why you should initialize variables upfront, because otherwise, your variable may contain garbage from the previous function/stack frame.  

Answer the questions below

It's like a play, but there's way more bits.