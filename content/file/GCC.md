#self-taught 
GCC stands for **GNU Compiler Collection**, it is a collection of [[compiler]]s from the [[GNU Project]] that supports various programming languages, hardware architectures, and operating systems.
GCC is distributed by the [[Free Software Foundation (FSF)]] under the GNU general public license (GNU GPL).
GCC is a key component of the [[GNU toolchain]].
It originally supported [[C]] and [[C++]] (and was therefore called the GNU C Compiler), but it now supports [[Rust]], [[COBOL]], [[GO]], [[Objective-C]], [[Objective-C++]] and [[Fortran]] between others.
# GCC vs G++
- GCC: gnu c compiler
- G++: gnu c++ compiler

- gcc will compile .c and .cpp files as C and C++ respectively
- g++ will compile both .c and .cpp files as C++

- if you use g++ for linking it will also link the g++ STD libraries
- gcc compiling .c files has fewer predefined macros

extra macros when compiling .cpp files with cpp or using g++:
```c++
#define __GXX_WEAK__ 1
#define __cplusplus 1
#define __DEPRECATED 1
#define __GNUG__ 4
#define __EXCEPTIONS 1
#define __private_extern__ extern
```
# Alternatives
- Apple and [[FreeBSD]] have switched to [[Clang]] + [[LLVM]].
# Flags
Most of the common flags are the same as in [[Clang]]:
```shell
-E # Run only the preprocessor stage.

-fsyntax-only # Run the preprocessor, parser and semantic analysis stages.

-S # Run the previous stages as well as LLVM generation and optimization stages and target-specific code generation, producing an assembly file.

-c # Run all of the above, plus the assembler, generating a target ".o" object file (no linker)

-save-temps # runs all stages but also saves every intermediate prdoduced file (Keeps .i, .bc, .s, .o, etc)

no stage selection option # If no stage selection option is specified, all stages above are run, and the linker is run to combine the results into an executable or shared library.

-save-temps # Save intermediate compilation results.

-march=architecture # specifies for what architecture for the current platform to compile

# to compile for a different platform+architecture you must use the correct binary:
gcc ecc # will compile for the current platform, and specified architecture (or current if unspecified)
triple-gcc # will compile for the specified triple, for example:
x86_64-pc-linux-gcc ecc # will compile for x86_64 linux machines 

# code generation options
-0x # with x = 0,1,2,3,fast,s,g,4 
# specifies the level of optimizaziont to use (currently >3 defaults to 3)
# -0fast is the fastest but is unsafe and breaks IEEE compliance

-flto             # Enable Link Time Optimization
```
# External Links
- [[GCC]]
- [[Compiler]]
- [[ABI]] 
- [[LLVM]]