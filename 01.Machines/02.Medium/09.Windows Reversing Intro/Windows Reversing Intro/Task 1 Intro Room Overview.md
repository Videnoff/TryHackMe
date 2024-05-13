This room is part of a series of rooms that will introduce you to reverse engineering software on Windows. This is going to be a fairly short and easy room in which you will be introduced to how higher-level concepts look at a lower level. You will also start to get familiar with IDA. We will use the skills learned here to perform more advanced reverse engineering techniques in future rooms.

The programs provided in this room are compiled with MSVC (C++ compiler built-in with Visual Studio) set to release mode for x64. Debug binaries and symbols will not be used to teach with, however, debug symbols will be provided for those who are curious. This is done to make everything as realistic as possible. Debug symbols are a luxury when reverse engineering, and aren't common when dealing with executables.

#### Get Hands-On.

**When running the samples on their own, outside of IDA, run them via the command line.**

Use the VM provided alongside this room to get hands-on with the material. This will greatly improve your experience and learning in this room. The VM has IDA Freeware installed along with the samples for the room.

VM Credentials:

- **Username:** thm
- **Password:** THMWinRE!

Quick note for the VM: When you load an executable into IDA you will be asked for debug symbols (a PDB). Say no to this. A further explanation as to why will be provided in the next task. If you attempt to download symbols IDA may crash.

#### Bring your own VM!

While the VM hosting on THM is great, they do have their limitations. Things such as processing power and internet access will make some tasks more difficult and it's for those reasons why I highly recommend you make a VM on your own computer. All you will need to do is install IDA Freeware and get the programs we will be reverse engineering.

Answer the questions below

Let's get started!