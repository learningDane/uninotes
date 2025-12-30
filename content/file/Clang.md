#self-taught 
# Clang
**[Clang](https://clang.llvm.org/)** is an "[[LLVM]] native" C/C++/Objective-C [[compiler]], which aims to deliver amazingly fast compiles, extremely useful [error and warning messages](https://clang.llvm.org/diagnostics.html) and to provide a platform for building great source level tools.
Clang is one of the primary sub-projects of [[LLVM]].
The [Clang Static Analyzer](https://clang-analyzer.llvm.org/) and [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) are tools that automatically find bugs in your code, and are great examples of the sort of tools that can be built using the Clang frontend as a library to parse C/C++ code.
# Clang vs GCC
Clang was born to be a drop-in replacement for GCC to be used with LLVM, so it keeps pretty much every flag possible with gcc.
# Clang Options
```shell
clang -### [options] main.c
# shows which commands it would execute

-E # Run only the preprocessor stage.

-fsyntax-only # Run the preprocessor, parser and semantic analysis stages.

-S # Run the previous stages as well as LLVM generation and optimization stages and target-specific code generation, producing an assembly file.

-c # Run all of the above, plus the assembler, generating a target ".o" object file (no linker)

-save-temps # runs all stages but also saves every intermediate prdoduced file (Keeps .i, .bc, .s, .o, etc)

no stage selection option # If no stage selection option is specified, all stages above are run, and the linker is run to combine the results into an executable or shared library.

-save-temps # Save intermediate compilation results.

-arch architecture # specifies for what architecture for the current platform to compile 

-target architecture # specifies for what architecture to compile, every platform possibible (must specify new triple: <architecture-OS-ABI), so must fully specify target platform and ABI
# examples
# x86_64-apple-macos13.0
# arm64-apple-macos14.0
# x86_64-pc-linux-gnu
# armv7-none-eabi           -> ARM bare-metal
# wasm32-unknown-unknown    -> WebAssembly 32-bit

# code generation options
-0x # with x = 0,1,2,3,fast,s,z,g,4 
# specifies the level of optimizaziont to use (currently >3 defaults to 3)
# -0fast is the fastest but is unsafe and breaks IEEE compliance

-flto             # Enable Link Time Optimization, Can merge LLVM bitcode across modules at link time
-flto=full
-filto=thin
-emit-llvm # when used with -S it outputs LLVM IR, with -c emits LLVM bitcode
-I path # Add the specified directory to the search path for include files.
```
# External Links
- [[GCC]]
- [[Compiler]]
- [[ABI]] 
- [[LLVM]]