#self-taught 
The **LLVM Project** is a collection of modular and reusable [[compiler]] and toolchain technologies.
LLVM began as a research project at the University of Illinois, with the goal of providing a modern, SSA-based compilation strategy capable of supporting both static and dynamic compilation of arbitrary programming languages.
Since then, LLVM has grown to be an umbrella project consisting of a number of subprojects, many of which are being used in production by a wide variety of commercial and open source projects as well as being widely used in academic research. Code in the LLVM project is licensed under the "**Apache 2.0 License** with LLVM exceptions".
# Primary Subprojects
### Clang
![[Clang#Clang]]
### LLVM Core
The LLVM Core libraries provide a modern source- and target-independent optimizer, along with code generation support for many popular CPUs.
These libraries are built around a well specified code representation known as the **LLVM intermediate representation** ("**LLVM IR**").
The LLVM Core libraries are well documented, and it is particularly easy to invent your own language (or port an existing compiler) to use LLVM as an optimizer and code generator.
### Libc and Libc++
Libc and Libc++ are standard conformant and high-performance implementations of the [[C]] and [[C++]] standard libraries, fully integrated with LLVM.
# Supported Languages
- [[C]]
- [[C++]]
- [[Objective-C]]
- [[Objective-C++]]
- [[Rust]]
- [[Swift]]
- ...
# How LLVM works
1. **Front End:** 
    This part of the compiler reads high-level source code from different languages (like C++, Rust, or Swift) and translates it into the universal LLVM Intermediate Representation (IR). 
2. **Intermediate Representation (IR):** 
    LLVM IR is an abstract, low-level, and machine-independent representation of the code. It's a standardized format that allows different programming languages to share the same optimization and code generation tools. 
3. **Middle End:** 
    This component applies various optimizations to the LLVM IR, improving the code's performance and efficiency. 
4. **Back End:** 
    The final stage translates the optimized LLVM IR into machine code specific to a target hardware architecture (like [[Assembly x86-64]] or [[ARM]]).