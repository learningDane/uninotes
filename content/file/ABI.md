#self-taught 
ABI stands for **Application Binary Interface**.
An ABI defines the low-level interface between compiled code and the system or other compiled code.

While an API (Application Programming Interface) tells you how to call a function in source code, the ABI tells you how the compiled machine code should interact.
# What an ABI specifies
1. Calling conventions
	1. how arguments are passed between functions
	2. who cleans up the stack
	3. return value location
2. data layout/alignment
	1. size of primitive types
	2. how types are aligned in memory
3. name mangling
	1. how function names appear in object files (especially in [[C++]]).
4. system-level conventions
	1. how system calls are made
	2. which registers are preserved across calls
5. binary format expectations
	1. for linking and loading object files ([[ELF]], [[Mach-O]], PE)
# Examples
- [[Linux]] uses the [[System V Binary Application Interface]], like most [[Unix]]-like systems.