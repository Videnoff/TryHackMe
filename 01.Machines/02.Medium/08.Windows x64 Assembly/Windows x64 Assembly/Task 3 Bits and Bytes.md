## Bits and Bytes

Data type sizes vary based on architecture. These are the most common sizes and are what you will come across when working with desktop Windows and Linux.

- **Bit is one binary digit**. Can be 0 or 1.
- **Nibble is 4 bits.**
- **Byte is 8 bits**.
- **Word is 2 bytes**.
- **Double Word (DWORD) is 4 bytes**. Twice the size of a word.
- **Quad Word (QWORD) is 8 bytes**. Four times the size of a word.

Before we get into other data types, let's talk about signed vs unsigned. Signed numbers can be positive or negative. Unsigned numbers can only be positive. The names come from how they work. Signed numbers need a sign bit to distinguish whether or not they're negative, similar to how we use the + and - signs.

### Data Type Sizes

- **Char** - 1 byte (8 bits).
- **Int** - There are 16-bit, 32-bit, and 64-bit integers. When talking about integers, it's usually 32-bit. For signed integers, one bit is used to specify whether the integer is positive or negative.
    - **_Signed_ Int**
        - 16 bit is -32,768 to 32,767.
        - 32 bit is -2,147,483,648 to 2,147,483,647.
        - 64-bit is -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
    - **_Unsigned_ Int** - Minimum is zero, maximum is twice that of a signed int (of the same size). For example: unsigned 32-bit int goes from 0 to 4,294,967,295. That is twice the signed int maximum of 2,147,483,647, however, its minimum value is 0. This is due to signed integers using the sign bit, making it unavailable to represent a value.
- **Bool** - 1 byte. Interestingly, a bool only _needs_ 1 bit because it's either 1 or 0 but it still takes up a full byte. This is because computers don't tend to work with individual bits due to alignment (talked about later). So instead, they work in chunks such as 1 byte, 2 bytes, 4 bytes, 8 bytes, and so on.

For more data types go here: [https://www.tutorialspoint.com/cprogramming/c_data_types.htm](https://www.tutorialspoint.com/cprogramming/c_data_types.htm)[  
](https://www.tutorialspoint.com/cprogramming/c_data_types.htm)

### Offsets

Data positions are referenced by how far away they are from the address of the first byte of data, known as the base address (or just the address), of the variable. The distance a piece of data is from its base address is considered the offset. For example, let's say we have some data, 12345678. Just to push the point, let's also say each number is 2 bytes. With this information, 1 is at offset 0x0, 2 is at offset 0x2, 3 is at offset 0x4, 4 is at offset 0x6, and so on. You could reference these values with the format BaseAddress+0x##. BaseAddress+0x0 or just BaseAddress would contain the 1, BaseAddress+0x2 would be the 2, and so on.

Answer the questions below

| Question                  | Answer |
| ------------------------- | ------ |
| How many bytes is a WORD? | 2      |
| How many bits is a WORD?  | 16     |
