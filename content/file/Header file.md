#uni 
Header files contain the declarations of functions, to be used by the Linker. They normally provide good documentation on how to use the functions, which can be really useful when not having the implementation file to read.

header.h
```c
#ifndef header
#define header

// comments

int function(int a, int b);
ecc

#endif
```

implementation is in lib

file.c
```c
#include <stdio.h>
// < > mean that it is a Global file, that exists in a library that we installed in the system system-wide

#include "lib/header.h"
// "" mean the file is in this folder, it is a local file

int main() {
	function(a,b);
	return 0;
}
```

linking
```bash
gcc file.c header.h -o file.o -lheader -L$(pwd)/lib
```
running
```bash
LD_LIBRARY_PATH=$(pwd)/lib ./file.o
```

to get info about the linking
```bash
ldd code
```