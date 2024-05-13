Structures are very common in modern software, especially with Windows. The entire Windows OS is highly object-oriented. The general definition of a structure is a data type that holds multiple pieces of data. To start, let's look at arrays which are essentially the most bare-bones data structure you can get.

#### Arrays

Arrays store multiple pieces of data which are the same type sequentially in memory. Let's say you have an array of 5 integers that starts at the address of 0x4000. The size of the array is 20 bytes since each integer is 4 bytes. The first integer is at 0x4000+0x0, the second is at 0x4000+0x04, and so on. Arrays are usually easy to analyze, like the character array (string) we encountered in the loop task.

#### Classes

Classes can have multiple pieces of data which are of different types. This is what makes them harder to work with when reversing. To figure out the layout of a class, you will have to do some analysis. You need to figure out not only how many things are in the class, but also their data types. There is quite an extensive number of ways to do this, but it generally comes down to just looking at the functions which use the class and paying close attention to how they use it. We will take a look at reverse engineering a class structure in a future room. For now, I'll give you a crash course.

Let's say we have the following class:

```cpp
class Human {
public:
	int age;
	float height;
	char* name;
	Human(char* newName, int newAge, float newHeight)
		: age(newAge), height(newHeight), name(newName) {}
};
```

This class's data will take up 16 bytes. 4 bytes for the age, 4 bytes for the height, and 8 for the name (pointers hold addresses and addresses in x64 are 8 bytes). How would this be identified in assembly? Let's say a pointer to the class is contained in RAX, and the address of the class is 0x4000. Here's some pseudo-assembly:

```asm
mov RAX, 0x4000     ; RAX = Address of the class and the age variable (offset 0)
lea RBX, [RAX+0x4]  ; RBX = Address of height
lea RCX, [RAX+0x8]  ; RCX = Address of name
mov [RAX], 0x32     ; age = 50
mov [RBX], 0x48     ; height = 72
mov [RCX], 0x424F42 ; name = "BOB"
```

As you can see we have the base address stored in RAX, and the items of the class are accessed via offsets. One of the things to pay attention to when dealing with classes is the use of addresses/pointers and the lea instruction. This is done because you usually want to access the data in the class, not a copy of it.

Dealing with classes is usually not too bad, but sometimes you aren't given the full class. For example, it's common for some parts of a class to only be referenced once such as some header information, so you have to be careful. Once again we'll take a look at an actual structure in a future room.

Answer the questions below

Structures are everywhere, be ready for them!