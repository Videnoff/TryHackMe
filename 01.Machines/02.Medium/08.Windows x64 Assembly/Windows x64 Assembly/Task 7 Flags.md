# Flags

Flags are used to signify the result of the previously executed operation or comparison. For example, if two numbers are compared to each other the flags will reflect the results such as them being even. Flags are contained in a register called EFLAGS (x86) or RFLAGS (x64). I usually just refer to it as the flags register. There is an actual FLAGS register that is 16 bit, but the semantics are just a waste of time. If you want to get into that stuff, look it up, Wikipedia has a good article on it. I'll tell you what you need to know.

## Status Flags

Here are the flags you should know. Note that when I say a "flag is set" I mean the flag is set to 1 which is true/on. 0 is false/off.

- **Zero Flag (ZF)** - Set if the result of an operation is zero. Not set if the result of an operation is _not_ zero.
- **Carry Flag (CF)** - Set if the last _unsigned_ arithmetic operation carried (addition) or borrowed (subtraction) a bit beyond the register. It's also set when an operation would be negative if it wasn't for the operation being unsigned.
- **Overflow Flag (OF)** - Set if a _signed_ arithmetic operation is too big for the register to contain.
- **Sign Flag (SF)** - Set if the result of an operation is negative.
- **Adjust/Auxiliary Flag (AF)** - Same as the carry flag but for Binary Coded Decimal (BCD) operations.
- **Parity Flag (PF)** - Set to 1 if the number of bits set in the last 8 bits is even. (10110100, PF=1; 10110101, PF=0)
- **Trap Flag (TF)** - Allows for single-stepping of programs.

For a full list of flags see: [https://www.tech-recipes.com/rx/1239/assembly-flags/](https://www.tech-recipes.com/rx/1239/assembly-flags/)

## Examples

#### Basic Comparison

Here are some examples to demonstrate flags being set.

Here's the first example. The following code is trying to determine if RAX is equal to 4. Since we're testing for equality, the ZF is going to be the most important flag.  
On line 2 there is a CMP instruction that is going to be testing for equality between RAX and the number 4. The way in which CMP works is by subtracting the two values. So when `cmp RAX, 4` runs, 4 is subtracted from RAX (also 4). This is why the comparison results in zero because the subtraction process literally results in zero. Since the result is zero, the ZF flag is set to 1 (on/true) to denote that the operation resulted in the value of 0, also meaning the values were equal! That brings us to the JNE, which jumps if _not_ equal/zero. Since the ZF is set it will not jump, since they _are_ equal, and therefore the call to func1() is made. If they were not equal, the jump would be taken which would jump over the function call straight to the return.  

```assembly
mov RAX, 4
cmp RAX, 4
jne 5       ; Line 5 (ret)
call func1
ret
; ZF = 1, OF = 0, SF = 0
```

#### Subtraction  

The following example will be demonstrating a _signed_ operation. SF will be set to 1 because the subtraction operation results in a negative number. Using the `cmp` instruction instead of `sub` would have the same results, except the value of the operation (-6) wouldn't be saved in any register.  

```assembly
mov RAX, 2
sub RAX, 8  ; 2 - 8 = -6.
; ZF = 0, OF = 0, SF = 1
```

#### Addition  

The following is an example where the result is too big to fit into a register. Here I'm using 8-bit registers so we can work with small numbers. The biggest number that can fit in a signed 8-bit register is 128. AL is loaded with 75 then 60 is added to it. The result of adding the two together should result in 135, which exceeds the maximum. Because of this, the number wraps around and AL is going to be -121. This sets the OF because the result was too big for the register, and the SF flag is set because the result is negative. If this was an unsigned operation CF would be set.

```assembly
mov AL, 75
add AL, 60
; ZF = 0, OF = 1, SF = 1
```

## Final Note

Hopefully, that gives you a good idea of what flags are and how they work. Remember that CMP will set flags depending on the result of the comparison. Conditional jumps will simply look at the flags. This tells us that a conditional jump does not need to be immediately proceeded with a CMP to work. Also, flags are set by things other than CMP instructions.

Answer the questions below

| Question                                                                                            | Answer |
| --------------------------------------------------------------------------------------------------- | ------ |
| If two equal values are compared to each other, what will ZF be set to as result of the comparison? | 1      |
