Luckily for us I was able to snag a copy of the source code from my dad's flash drive  

```
#include "unistd.h"
#include "stdio.h"
#include "stdlib.h"
void shell(){
setuid(1000);
setgid(1000);
system("cat /var/backups/shadow.bak");
}

void get_input(){
char buffer[32];
scanf("%s",buffer);
}

int main(){   get_input();   
} 
``` 
  

The SUID file seems to expect 32 characters of input, and then immediately exits. This seems to warrant further investigation. Luckily I was practicing binary exploitation back when I was using that PC, so I have tools preinstalled to examine. One of those tools is pwndbg, a plugin for GDB which allows you to better examine binary files.  

Run `gdb /opt/secret/root` and you should see a screen similar to this  

![](https://imgur.com/yXO2cLo.jpg)

```
gdb /opt/secret/root
```
![[Pasted image 20240328213552.png]]


This means that pwndbg has successfully been initialized. The next step is to test if anything happens when you send more then 32 characters. To do this type `r < <(cyclic 50)`, that command runs the program and provides 50 characters worth of "cyclic" input.

Cyclic input goes like this: "aaaaaaaabaaacaaadaaaeaaaf" etc. Because it's in this "cyclic" format, it allows us to better understand the control we have over certain registers, for reasons you are about to see.

Once you run that command you should see something similar to this screen

![](https://imgur.com/RDSPKbe.jpg)  

```
r < <(cyclic 50)
```



Now this is where some knowledge of assembly helps. It seems that in this case we're able to overwrite EIP, which is known as the instruction pointer. The instruction pointer tells the program which bit of memory to execute next, which in an ideal case would have the program run normally. However, since we're able to overwrite it, we can theoretically execute any part of the program at any time.

Recall the shell function from the source code, if we can overwrite EIP to point to the shell function, we can cause it to execute. This is also where the benefits of cyclic input show themselves. Recall that cyclic input goes in 4 character/byte sequences, meaning we're able to calculate exactly how many characters we need to provide before we can overwrite EIP.

Luckily cyclic provides this functionality with the -l flag, running cyclic -l {fault address} will tell us exactly how many characters we need to provide we can overwrite EIP.

Running `cyclic -l 0x6161616c` outputs 44, meaning we can overwrite EIP once we provide 44 characters of input.  

That's all we needed for pre-explotation!  

Answer the questions below

Read the above :)