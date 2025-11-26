#self-taught 
**Just In Time Compilation** (**JIT compilation**) (also *dynamic translation* or *run-time compilations*) is compilation (of computer code) during execution of a program (at run time) rather than before execution.
This may consist of source code translation but is more commonly bytecode translation to machine code, which is then executed directly.
A system implementing a JIT compiler typically continuously analyses the code being executed and identifies parts of the code where the speedup gained from compilation or recompilation would outweigh the overhead of compiling that code.

JIT compilation is a combination of the two traditional approaches to translation to machine code: *ahead-of-time compilation* (*AOT*), and *interpretation*, which combines some advantages and drawbacks of both. 
Roughly, JIT compilation combines the speed of compiled code with the flexibility of interpretation, with the overhead of an interpreter and the additional overhead of compiling and linking (not just interpreting).
JIT compilation is a form of dynamic compilation, and allows adaptive optimization such as dynamic recompilation and microarchitecture-specific speedups.
Interpretation and JIT compilation are particularly suited for dynamic programming languages, as the runtime system can handle late-bound data types and enforce security guarantees.