The process for reverse engineering a DLL is mostly the same as executables, but they are usually easier since you can see more function names. It's also more common to see debug symbols provided with DLLs than it is to see them with executables.

#### Imports, Exports, Modules

You've probably seen many function names that are all nonsense. As mentioned earlier, most function names do not survive through compilation since they are just there for human understanding. You may, however, notice that some names do exist. This could be because of two main reasons.

- First, the tool recognizes the function and names it accordingly. IDA does this with FLIRT (Fast Library Identification and Recognition Technology) signatures. FLIRT signatures are used to identify standard library functions. The general idea of how they work is they search memory for a chunk of bytes that match a known chunk of bytes in a standard library function. Once a match is found, the function can be named accordingly. You can learn more about FLIRT signatures on the [IDA/Hex-Rays website](https://hex-rays.com/products/ida/tech/flirt/in_depth/). The main() function is a little more difficult since its signature is different for every program. However, IDA can still sometimes find it using some tricks. One commonality of the main() function is that it's called from the program entry point, usually towards the end. There's also usually a test against the return value of main() to determine if anything other than zero was returned. You can use that knowledge to help find the main() function, and there are several other ways as well. I won't get into this here as it can get quite long and advanced. I highly encourage you to do your own research on this.  
    
- Second, its name may be preserved because it's imported from or exported by a DLL. For a developer to use a function from a DLL the developer needs to know and be able to resolve the name of the function they want. Because of this, the names have to stay intact. The DLL can expose its function names through the DLL/PE header, library file, or header file (.h or .hpp). The library and header files are not required, but they are usually included.

**Imports** are the functions the executable is using/importing from a DLL, and **exports** are the functions a DLL provides/exports. DLL's are known as dynamic-link libraries since they are loaded into memory once and can be loaded into any number of processes at any time without making any more copies. The Windows OS is built on DLLs.

**Modules** are essentially anything related to a process that import or export functions. For example, Loop.exe includes modules such as ntdll.dll, kernel32.dll, etc. If you were to run Loop.exe, while it is running Loop.exe itself is considered a module of the process.  

#### Name Mangling/Decoration

C++ function overloading allows you to have two different functions with the same names that take different parameters. This becomes a problem when a DLL is exporting functions since the exported names will be the same. For developers, this problem is solved by using libraries and header files. On a lower level, this problem is solved by mangling the names so they are unique. _**ALL**_ exported **C++** function names get mangled whether they have overrides or not.  

Function mangling is also called function decoration, which is probably a more appropriate name just not as popular. Although the mangled names may look like random garbage, there is a method to the madness. Here is an example of a mangled function name: `??0?$_Yarn@D@std@@QEAA@PEBD@Z`. As random as it may seem, it can be decoded. By de-mangling the name you can find the function type and parameter types. Different compilers use different mangling schemes, in this series of rooms everything uses the Microsoft C++ compiler and mangling scheme. You don't need to know how the schemes work since reverse engineering tools can decode them, but if you'd like here are some links.  

Microsoft C++ Mangling Scheme: [http://mearie.org/documents/mscmangle/](http://mearie.org/documents/mscmangle/)  
More Mangling Schemes: [https://en.wikipedia.org/wiki/Name_mangling](https://en.wikipedia.org/wiki/Name_mangling)  

Side note for the programmers out there. Putting `extern "C"` before a function makes it use C linkage, thus removing the name mangling. This does prevent you from overloading the function.  

#### Running DLL

When reverse engineering a DLL you may want to run it so you can analyze it in a debugger. This presents an obvious problem, you can't simply run a DLL. Here's a bit more detail on how DLLs work.

When a DLL is loaded, the function DllMain() is executed within the context of the process which loads the DLL. Here the DLL can run whatever code it wants.

You may have heard of DLL injection, this is one way it can be done. You can get the target process to call LoadLibrary() on your DLL which will cause DllMain() within your DLL to be executed within the context of the target process.

There's a program that comes with Windows called rundll32.exe which does pretty much that, it just loads your DLL making DllMain() execute. As a developer, you can make rundll32.exe execute functions within the DLL, but I don't think anyone does this.  

For reverse engineers, what if we want to dynamically analyze a function within a DLL? The best way to do this is to write your own code which calls the function you're interested in. Without a library or header file, here's one way (there's probably a more elegant way) in which you could call a function within a DLL with only the .dll file. This does not include any error handling, it's only the code of interest. It's a call to a function called Add() within the DLL named DLL.DLL:  

```cpp
HMODULE dll = LoadLibraryA("DLL.DLL");
typedef void(WINAPI* Add_TypeDef)(int, int); // Add(int x, int y)
Add_TypeDef Add = (Add_TypeDef)GetProcAddress(dll, "Add_MangledName");
Add(1, 2);
```

Unless you have a header or library file, you will likely need to reverse engineer the function to find out what parameters are passed to it.

That's all there is to DLLs since other than all of that they are the same as executables when it comes to reverse engineering.  

Answer the questions below

A DLL is an executable on easy mode.