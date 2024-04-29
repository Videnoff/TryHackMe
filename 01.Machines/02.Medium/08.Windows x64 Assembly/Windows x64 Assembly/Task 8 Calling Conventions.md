# Windows x64 Calling Convention

There are many calling conventions, I will cover the one used on x64 Windows in detail. Once you understand one you can understand the others very easily, it's just a matter of remembering which is which (if you choose to).

Before we start, be aware that **attention to detail is _very_ important here**.

When a function is called you could, theoretically, pass parameters via registers, the stack, or even on disk. You just need to be sure that the function you are calling knows where you're putting the parameters. This isn't too big of a problem if you are using your own functions, but things would get messy when you start using libraries. To solve this problem we have **calling conventions** that define how parameters are passed to a function, who allocates space for variables, and who cleans up the stack.

> **Callee** refers to the function being called, and the **caller** is the function making the call.

There are several different calling conventions including cdecl, syscall, stdcall, fastcall, and more. Because I've chosen to focus on x64 Windows for simplicity, we will be working with x64 fastcall. If you plan to reverse engineer on other platforms, be sure to learn their respective calling convention(s).

> You will sometimes see a double underscore prefix before a calling convention's name. For example: __fastcall. I won't be doing this because it's annoying to type.

# Fastcall

Fastcall is _the_ calling convention for x64 Windows. Windows uses a four-register fastcall calling convention by default. Quick FYI, when talking about calling conventions you will hear about something called the "Application Binary Interface" (ABI). The ABI defines various rules for programs such as calling conventions, parameter handling, and more.

#### How does the x64 Windows calling convention work?

- The first four parameters are passed in registers, **_LEFT_** to **_RIGHT_**. Parameters that are _**not**_ floating-point values, such as integers, pointers, and chars, will be passed via RCX, RDX, R8, and R9 (in that order). Floating-point parameters will be passed via XMM0, XMM1, XMM2, and XMM3 (in that order).
- If there is a mix of floating-point and integer values, they will still be passed via the register that corresponds to their position. For example, `func(1, 3.14, 6, 6.28)` will pass the first parameter through RCX, the second through XMM1, the third through R8, and the last through XMM3.
- If the parameter being passed is too big to fit in a register then it is passed by reference (a pointer to the data in memory). Parameters can be passed via any sized corresponding register. For example, RCX, ECX, CX, CH, and CL can all be used for the first parameter. Any other parameters are pushed onto the stack, **_RIGHT_** to **_LEFT_**.

> There is _always_ going to be space allocated on the stack for 4 parameters, even if there aren't any parameters. This space isn't completely wasted because the compiler can, and often will, use it. Usually, if it's a debug build, the compiler will put a copy of the parameters in the space. On release builds, the compiler will use it for temporary or local variable storage.

Here are some more rules of the calling convention:

- The base pointer (RBP) is saved when a function is called so it can be restored.
- A function's return value is passed via RAX if it's an integer, bool, char, etc., or XMM0 if it's a float or double.
- Member functions have an implicit first parameter for the "this" pointer. Because it's a pointer and it's the first parameter, it will be passed via RCX. This can be very useful to know.
- The _caller_ is responsible for allocating space for parameters for the _callee_. The caller must always allocate space for 4 parameters even if no parameters are passed.
- The registers RAX, RCX, RDX, R8, R9, R10, R11, and XMM0-XMM5 are considered _volatile_ and must be considered destroyed on function calls.
- The registers RBX, RBP, RDI, RSI, RSP, R12, R13, R14, R15, and XMM6-XMM15 are considered _nonvolatile_ and should be saved and restored by a function that uses them.

## Stack Access

Data on the stack such as local variables and function parameters are often accessed with RBP or RSP. On x64 it's extremely common to see RSP used instead of RBP to access parameters. Remember that the first four parameters, even though they are passed via registers, still have space reserved for them on the stack. This space is going to be 32 bytes (0x20), 8 bytes for each of the 4 registers. Remember this because at some point you will see this offset when accessing parameters passed on the stack.

- 1-4 Parameters:
    - Arguments will be pushed via their respective registers, left to right. The compiler will likely use RSP+0x0 to RSP+0x18 for other purposes.
- More Than 4 Parameters:
    - The first four arguments are passed via registers, left to right, and the rest are pushed onto the stack starting at offset RSP+0x20, right to left. This makes RSP+0x20 the fifth argument and RSP+0x28.

Here is a very simple example where the numbers 1 to 8 are passed from one function to another function. Notice the order they are put in.

```c
function(1,2,3,4,5,6,7,8)
```

```nasm
MOV RCX 0x1 ; Going left to right.
MOV RDX 0x2
MOV R8 0x3
MOV R9 0x4
PUSH 0x8 ; Now going right to left.
PUSH 0x7
PUSH 0x6
PUSH 0x5
CALL function
```

In this case, the stack parameters should be accessed via RSP+0x20 to RSP+0x28.

Putting them in registers left to right and then pushing them on the stack right to left may not make sense, but it does once you think about it. By doing this, if you were to pop the parameters off the stack they would be in order.

```asm
POP R10 ; = 5
POP R11 ; = 6
POP R12 ; = 6
POP R13 ; = 7
```

Now you can access them, left to right in order: RCX, RDX, R8, R9, R10, R11, R12, R13.

Beautiful :D

# Further Exploration

That's the x64 Windows fastcall calling convention in a nutshell. Learning your first calling convention is like learning your first programming language. It seems complex and daunting at first, but that's probably because you're overthinking it. Furthermore, it's typically harder to learn your first calling convention than it is your second or third.

If you want to learn more about this calling convention you can here:  
[https://docs.microsoft.com/en-us/cpp/build/x64-calling-convention?view=vs-2019](https://docs.microsoft.com/en-us/cpp/build/x64-calling-convention?view=vs-2019)  
[https://docs.microsoft.com/en-us/cpp/build/x64-software-conventions?view=vs-2019](https://docs.microsoft.com/en-us/cpp/build/x64-software-conventions?view=vs-2019)

> Quick reminder, it may not hurt to go back and read the registers, memory layout, and instructions sections again. Maybe even come back and read this section after those. All of these concepts are intertwined, so it can help. I know it's annoying and sometimes frustrating to re-read, but trust me when I say it's worth it.

# cdecl (C Declaration)

After going in-depth on fastcall, here's a quick look at cdecl.

- The parameters are passed on the _stack_ backward (right to left).
- The base pointer (RBP) is saved so it can be restored.
- The return value is passed via EAX.
- The caller cleans the stack. This is what makes cdecl cool. Because the caller cleans the stack, cdecl allows for a variable number of parameters.

Like I said after you understand your first calling convention learning others is pretty easy. Quick reminder, this was only a brief overview of cdecl.

See here for more info:  

- [https://docs.microsoft.com/en-us/cpp/build/x64-software-conventions?view=vs-2019](https://docs.microsoft.com/en-us/cpp/build/x64-software-conventions?view=vs-2019)
- [https://docs.microsoft.com/en-us/cpp/build/x64-calling-convention?view=vs-2019](https://docs.microsoft.com/en-us/cpp/build/x64-calling-convention?view=vs-2019)
- [https://docs.microsoft.com/en-us/cpp/build/prolog-and-epilog?view=vs-2019](https://docs.microsoft.com/en-us/cpp/build/prolog-and-epilog?view=vs-2019)
- [https://www.gamasutra.com/view/news/171088/x64_ABI_Intro_to_the_Windows_x64_calling_convention.php](https://www.gamasutra.com/view/news/171088/x64_ABI_Intro_to_the_Windows_x64_calling_convention.php)

Answer the questions below

| Question                                                                    | Answer |
| --------------------------------------------------------------------------- | ------ |
| In fastcall, what 64-bit register will hold the return value of a function? | RAX    |
| In fastcall, what register is the first function parameter passed in?       | RCX    |
