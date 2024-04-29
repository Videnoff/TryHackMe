Note: There are two different syntaxes for assembly: Intel and AT&T. We will focus on Intel because I think it's the easiest to read and it's the default for Windows tools. Note that when working with Linux, AT&T is more commonly used.

# ﻿Registers

Depending on whether you are working with 64-bit or 32-bit assembly things may be a little different. As already mentioned this course focuses on 64-bit Windows.

What Is Assembly?

The end goal of a compiler is to translate high-level code into a language the CPU can understand. This language is Assembly. The CPU supports various instructions that all work together doing things such as moving data, performing comparisons, doing things based on comparisons, modifying values, and anything else that you can think of. While we may not have the high-level source code for any program, we can get the Assembly code from the executable.

### Assembly VS C:

Small example:

```c
if(x == 4){
    func1();
}else{
    return;
}
```

is functionally the same as the following pseudo-assembly:

```assembly
mov RAX, x
cmp RAX, 4
jne 5       ; Line 5 (ret)
call func1
ret
```

This should be fairly self-explanatory, but I'll go over it briefly. First, the variable `x` is moved into RAX. RAX is a register, think of it as a variable in assembly. Then, we compare that with 4. If the comparison between RAX (4) and 5 results in them not being equal then jump (jne) to line 5 which returns. Otherwise, they are equal, so call `func1()`.

### **The Registers**

Let's talk about **General Purpose Registers (GPR)**. You can think of these as variables because that's essentially what they are. The CPU has its own storage that is extremely fast. This is great, however, space in the CPU is extremely limited. Any data that's too big to fit in a register is stored in memory (RAM). Accessing memory is much slower for the CPU compared to accessing a register. Because of the slow speed, the CPU tries to put data in registers instead of memory if it can. If the data is too large to fit in a register, a register will hold a pointer to the data so it can be accessed.

#### **There are 8 main general-purpose registers:**

There are several GPR's, each with an assigned task. However, this task is more of a template as registers are usually used for whatever, except for a few. Regardless, it's good to know their assigned purpose for when they are used according to their designation.

- RAX - Known as the **accumulator register**. Often used to store the return value of a function.
- RBX - Sometimes known as the **base register**, not to be confused with the base pointer. Sometimes used as a base pointer for memory access.
- RDX - Sometimes known as the **data register**.
- RCX - Sometimes known as the **counter register**. Used as a loop counter.
- RSI - Known as the **source index**. Used as the source pointer in string operations.
- RDI - Known as the **destination index**. Used as the destination pointer in string operations.
- RSP - The **stack pointer**. Holds the address of the top of the stack.
- RBP - The **base pointer**. Holds the address of the base (bottom) of the stack.

All of these registers are used for holding data. Something to point out immediately is that these registers can be used for anything. Again, their "use" is just common practice. For example, RAX is often used to hold the return value of a function but it doesn't have to (and often doesn't). However, imagine you were writing a program in Assembly. It would be extremely helpful to know where the return value of a function went, otherwise why call the function? Also, look at the Assembly example I gave earlier. It uses RAX to store the _x_ variable.

With that said, some registers are best left alone when dealing with typical data. For example, RSP and RBP should almost always only be used for what they were designed for. They store the location of the current stack frame (we'll get into the stack soon) which is very important. If you do use RBP or RSP, you'll want to save their values so you can restore them to their original state when you are finished. As we go along, you'll get the hang of the importance of various registers at different stages of execution.

#### **The Instruction Pointer**

RIP is probably the most important register. RIP is the "Instruction Pointer". It is the address of the _next_ line of code to be executed. You cannot directly write into this register, only certain instructions such as ret can influence the instruction pointer.

#### **Register Break Downs**

Each register can be broken down into smaller segments which can be referenced with other register names. RAX is 64 bits, the lower 32 bits can be referenced with EAX, and the lower 16 bits can be referenced with AX. AX is broken down into two 8 bit portions. The high/upper 8 bits of AX can be referenced with AH. The lower 8 bits can be referenced with AL.

![](https://raw.githubusercontent.com/0xZ0F/Z0FCourse_ReverseEngineering/master/Chapter%203%20-%20Assembly/%5Bignore%5D/RegisterBreakdown.png)  

RAX consists of all 8 bytes which would be bytes 0-7. EAX consists of bytes 4-7, AX consists of bytes 6-7, AH consists of only byte 6, and AL consists of only byte 7 (the final byte).

If `0x0123456789ABCDEF` was loaded into a 64-bit register such as RAX, then RAX refers to `0x0123456789ABCDEF`, EAX refers to `0x89ABCDEF`, AX refers to `0xCDEF`, AH refers to `0xCD`, AL refers to `0xEF`.

What is the difference between the "E" and "R" prefixes? Besides one being a 64-bit register and the other 32 bits, the **"E" stands for extended**. The **"R" stands for register**. The "R" registers were newly introduced in x64, and no, you won't see them on 32-bit systems.

To see how _all_ registers are broken apart go here:  
[https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/x64-architecture](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/x64-architecture)

## Different Data Types

- **Floating Point Values** - Floats and Doubles.
- **Integer Values** - Integers, Booleans, Chars, Pointers, etc.

Different data types can't be put in just any register. Floating-point values are represented differently than integers. Because of this, floating-point values have special registers. These registers include **YMM0 to YMM15** (64-bit) and **XMM0 to XMM15** (32-bit). The XMM registers are the lower half of the YMM registers, similar to how EAX is the lower 32 bits of RAX. Something unique about these registers is that they can be treated as arrays. In other words, they can hold multiple values. For example, YMM# registers are 256-bit wide each and can hold 4 64-bit values or 8 32-bit values. Similarly, the XMM# registers are 128-bits wide and can hold 2 64-bit values or 4 32-bit values. Special instructions are needed to utilize these registers as vectors.

A nice table of these registers, and more information about them, can be found here: [https://en.wikipedia.org/wiki/Advanced_Vector_Extensions](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions)

### Extra Registers

There are additional registers that should be mentioned. These registers don't have any special uses. There are registers **r8 to r15** which are designed to be used by integer type values (not floats or doubles). The lower 4 bytes (32 bits), 2 bytes (16 bits), and 8 bits (1 byte) can all be accessed. These can be accessed by appending the letter "d", "w", or "b".  
Examples:

- R8 - Full 64-bit (8 bytes) register.
- R8D - Lower double word (4 bytes).
- R8W - Lower word (2 bytes)
- R8B - Lower byte.

Answer the questions below

| Question               | Answer |
| ---------------------- | ------ |
| How many bytes is RAX? | 8      |
| How many bytes is EAX? | 4      |
