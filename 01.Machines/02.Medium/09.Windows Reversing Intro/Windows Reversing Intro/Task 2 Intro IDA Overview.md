## Tool Introductions  

In this room, we will be using IDA Freeware. Historically the downside to IDA has always been its pricing, however, thanks to recent developments in other tools, the free version of IDA now has many more features than it used to. Other good tools include x64dbg, Ghidra, WinDBG, Radare2, and of course GDB. My daily drivers are x64dbg and Ghidra. IDA is used for this series since it's easy for beginners and results in us only having to use one tool.  

First, let's discuss static vs dynamic analysis. **Static** analysis involves looking at the program as it exists on disk; The program is never executed. **Dynamic** analysis involves analyzing the process as it runs. Dynamic analysis is usually preferred unless dealing with malware. Dynamic analysis allows you to see data in memory and how it's being used. Static on the other hand requires you to guess or do detailed reverse engineering to figure it out.

There are three main functionalities that our tools will provide, those are debugging, disassembling, and decompiling. **Disassemblers** will translate the program from its bytes on disk or in memory into its assembly code equivalent and present it in an informative way. **Decompilers** are similar to disassemblers except instead of giving us the assembly, it attempts to recreate the code in C/C++. The downside to decompilers is that they can be inaccurate, or lack information. Because of this, if you're using a decompiler it's a good idea to have the disassembled code next to the decompiled code to check for inaccuracies. **Debuggers**, alongside disassemblers and decompilers, will allow us to place breakpoints within the program while it's running and analyze registers, memory, statuses, and more. They also allow for changing data in memory while the program is running.

## IDA Overview  

IDA is quite an extensive tool, I will only show you what you need to know. I **highly** encourage you to learn more about how to use IDA on your own time. It's not difficult to use, rather there's just a lot to it. For the following explanations, I will be using notepad.exe (C:\Windows\System32\notepad.exe).  

To load a program into IDA you can start IDA then follow the prompts, or you can alternatively just drag and drop the executable file onto the IDA icon on your Desktop. While loading the program into IDA it will prompt you about the type of file, you can just stick with the defaults. At some point, you will be asked about debug symbols (PDB). In the real world, get any debug symbols you can. Normally you will only have the debug symbols for Windows libraries. For the sake of this room, we won't use any except for what comes with the system by default.  

#### Debug Symbols  

Debug symbols are extremely helpful and you should use them when you can. Unfortunately, you will usually only have debug symbols for common libraries and rarely for the executable of interest. In addition to that, most reversing tools download symbols for common libraries so if you don't have an internet connection you won't get them. Note that because of this, don't attempt to download symbols in IDA when using the VM otherwise you will get errors and it may crash. In this room, we will go over the samples **without** their debug symbols to maintain as much realism as possible. However, for further learning purposes, debug symbols will be provided if you wish to manually load them.  

#### Code Views  

The two primary views, listing and graph view, show the program in its disassembled form. You can switch between the two by pressing the space bar. I recommend you spend most of your time in graph view, as it shows the flow of the program.

![IDA Graph View](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/a47d33022ae2526933d169bca81f1a06.PNG)

As you can see in the graph view, the arrows represent the destination of jump instructions. This is incredibly useful and a massive time saver.  

![IDA Listing View](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/e4d0dba634cd54a6997e820c23fa5d13.PNG)

In the listing view, you can see slightly more information, however, it's much harder to understand the flow of the program.

You may find it helpful to enable Auto Comments by going to _Options > General > Disassembly (Selected by default) > Auto Comments  
_Play around with it on/off and see if you like it. I found it useful when I started since it describes what is happening in the assembly.

![IDA Decompiled/Pseudocode View](https://tryhackme-images.s3.amazonaws.com/user-uploads/600dd6c4ac4b18769b2a8cdf/room-content/04214c9a470ae01a1d65e20f91df4a3c.PNG)

**You need to have internet access to be able to decompile code with IDA Freeware, so it will NOT work in the provided VM.**  
IDA also has a decompiler. Do not become reliant on decompilers as they aren't always accurate and often have issues representing every instruction in longer sections of code. With that said, they are a great place to get a general idea of what's going on. To decompile, IDA calls it pseudocode, you can click on the area of code you want to decompile and press _F5_. You can also go to _View > Open Subviews > Generate Pseudocode_.

**I will not be utilizing the decompiler feature of IDA for this series of rooms.**

#### Imports/Exports

These tabs are pretty self-explanatory. The imports tab shows all of the functions imported by the current program from other sources. The exports tab shows all of the functions exposed by the current program. Note that the exports of an executable usually contain only the entry point (where the program starts executing from).

#### Functions

On the left, you can see the Functions window which shows the identified functions for the current program. Depending on what symbols you have access to, you may have more or less functions with actual names. If there are no symbols to identify a function, it will instead be given a generic name such as sub_140001000 where 140001000 is the address of the function.

#### Other Subviews

You can find other useful tabs/subviews under _View > Open Subviews_. I encourage you to play around with the different subviews as there's a significant amount of information found within them. One subview in particular which you should get familiar with is the _Strings_ subview. Here you can view all identified strings in memory. This can be helpful, as we will see later when finding a certain function or place of interest.

## Further Learning  

As mentioned, IDA is packed full of stuff. I highly recommend you play around and get familiar with IDA. There are loads of guides, videos, and even books out there to assist you!  

Answer the questions below

Once you feel comfortable with IDA, let's start doing some reverse engineering!