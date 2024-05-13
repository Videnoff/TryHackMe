**When running the samples on their own, outside of IDA, run them via the command line.**

Before you load the program into IDA, I want to quickly repeat a warning. When you are prompted for debug symbols **do not** do it. This is to maintain realism. If you wish to use debug symbols for further learning on your own, you can load them manually after the program is loaded into IDA. The debug symbols are provided in a folder on the Desktop along with the samples. If you attempt to download symbols IDA may crash.

#### **Getting Started**  

Let's take a look at a sample that calls a function. For this task use **HelloWorld.exe**. It's usually a good idea to run the program before doing any reverse engineering, so go ahead and do that. Again, when you run the program do so from a command prompt since the program closes very quickly.

We are going to start from main(), find it in the function list if IDA doesn't navigate to it automatically. The main() function should look something like this:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/059b8317bfc82482e7646b3765f28b9d.PNG)  

Notice the `sub RSP, 28h` at the top. For this function that's the entire prologue. It's setting up the function by moving the stack pointer and creating a new stack frame area.

#### printf()

For now, we will focus on the first function call within main(), which is a call to printf(). IDA does not resolve that this is printf(), so instead, you can identify it as such based on the parameters passed and what it does when the program runs. IDA shows two strings loaded into the first two parameters for the function call. The first parameter (passed via RCX) is the format string "%s\n", the second parameter (RDX) is the "Hello with..." string. Immediately after the two parameters is the call. In IDA you can rename the sub_### to whatever you want by right-clicking and going to _Rename_ or by selecting the function and pressing _N_. Renaming variables and functions is very useful when dealing with bigger projects.

That's it for the call to printf(). The first parameter is the format string, the second is the "Hello..." string, and printf() makes the magic happen. Feel free to look into printf() more if you'd like.

#### std::cout

Now let's look at the second function call which is to std::cout.

We can identify it's std::cout without using the string printed to the console because we can see things related to cout, basic_ostream, and char_traits. You may notice the names of the functions are quite odd as displayed in IDA. We will discuss this in the DLL section, but in short, the names are mangled for function overloading. For now, look past the name mangling. With that said, you may not be familiar with those functions so the first thing to do is look them up. Here's a brief overview of them all:

- basic_ostream - C++ template for output streams. [More info here](https://en.cppreference.com/w/cpp/io/basic_ostream).
- char_traits - Provides some abstraction from basic character and string types.  
    
- cout - std::cout - Sends text to the console.

Now to address the elephant in the room. Where is the string that's supposed to be printed? Let's find it.

To find our string go to _View > Open Subviews > Strings_ or press _Shift + F12_. Note that this may take a bit to process. Then look for the string in the list. You can use Ctrl + F to search. Double-click the string in the list and this will bring you to the string where you can see all references to that string. IDA calls these XREFs, short for cross-references.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/2beb8a49b216bf582c6eb0426ab4d238.png)  

The string only has one reference, so double-click it. This will bring you to the location of the string which is in a very large function.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/4d5c84ea7ec963e86d8c4227f746fbb8.png)

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/39b72c7a4549dbe9311ca57b36b25c04.png)  

The string is very clearly not where we would've expected it to be. We can see `sputn`, which long story short means we're dealing with character streams. So what is this massive function and what is it doing? If you go to the top of the function in the listing view you can see what references it. Sure enough, main() references this function. So what's going on here?  

#### Inlining

One compiler/linker optimization that makes noticeable changes to the code is inlining. When a function gets inlined it's essentially pasted where the call would be instead of making a call. See the following example.

**Without** Function Inlining:

```cpp
int Add(int x, int y){
    return x+y;
}
int main(){
    int x = RandInt();
    int res = Add(x, 5)
}
```

**With** Function Inlining:

```cpp
int main(){
    int x = RandInt();
    int res = x + 5;
}
```

What's happening with our string in HelloWorld.exe is similar. Instead of the string being passed as a parameter to std::cout, it's directly referenced in std::cout. You may think that this would cause problems because what if std::cout is called to print a different string? You'd be correct, this would cause problems for further calls to std::cout. As it turns out if std::cout is called more than once you will not see this optimization used. Instead, you will see it used similar to how printf() is used.  

I encourage you to write a program to play around with this to develop a deeper understanding of it. You may have noticed that there's some interesting stuff with std::cout that I skipped over. In short, it has to do with function overloading, basic_ostream, and streambuf which deals with character streams. If you're interested, simple searches of those things will bring you some useful information.  

That concludes the basic function example. It's really easy to understand function calls as long as you know the calling convention used. Luckily for x64 Windows it only uses fastcall, but other systems and architectures will likely not be that nice. Be sure to know whatever calling convention you're dealing with well, it will make your work much easier.

Answer the questions below

| Question                                                                                                                                                                                      | Answer          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| In the HelloWorld.exe sample, which instruction sets up the first parameter for the call to printf()? Provide the full instruction as shown in IDA, with single spaces. Example: mov RAX, RBX | lea rcx, Format |
