#uni 
[[Assembly x86-64]], [[C++]] 
In [[C]], `extern` is sufficient for telling a [[C]] program that the function is defined in another file.
In [[C++]] though function names will get mangled ([[mangling]]), so the linker will fail to link the mangled symbol to the [[Assembly x86-64]] function.
This leads us to also need the `"C"` option tells the compiler to use [[C]] style calling conventions, so the function name will not be mangled.
```c++
extern "C" void func();
```
# C calls Assembly subroutine
```c
extern void func();          <-----------------------------------
int main() {
	func();
	return 0;
	}
```

```asm
# .global in x86_64, ARM MASM and others use EXPORT func
.global func           <----------------------------------------
func: 
	# instructions
	ret

```
One can also make a symbol weak: linker will prefer a strong definition if it exists (a different implementation, if available, takes precedence over this one):
```asm
.global func
.weak func
# in MASM, ARM: EXPORT func [WEAK]
```
WEAK is used to define "default" implementations.
# Assembly calls C function
```c
void func(){
	// code
}
```

```asm
.global _start        # entry point if there is no main (linux syscall style)
# .extern in x86_64, ARM MASM and others use IMPORT func
.extern func     <------------------------------

_start:
	# code
	call func     <------------------------------
	
	# exit program (linux syscall style)
	mov $60, %rax    # syscall 60 is exit
	xor %rdi, %rdi   # status is 0
	syscall
```
# Compiling and linking with GCC
```bash
# gcc, at&t syntax
gcc file.c file.s -o file.o

# gcc, intel syntax
gcc filec.c -o filec.o                    # c compiling
gcc -masm=intel files.s -o files.o        # assembly compiling
gcc files.o filec.o -o file.o             # linking
```
# Inline assembly
This way one cannot access directly the cpu registers.
```c
int main(void) {
	int t,a,b;
	__asm {
		ADD t, a, b; // t,a,b are virtual registers
	}
	return 0;
	}
```

# Parametri
There are sixteen 64-bit registers in x86_64: %**rax** , %**rbx** , %**rcx** , %**rdx** , %**rdi** , %**rsi** , %**rbp** , %**rsp** , and %**r8-r15** .

Of these, %rax , %rcx , %rdx , %rdi , %rsi , %rsp , and %r8-r11 are considered **caller-saved registers**, meaning that *they are not necessarily saved across function calls*. 

By convention, ==%rax is used to store a function’s return value==, if it exists and is no more than 64 bits long. (Larger return types like structs are returned using the stack.) 

Registers %rbx , %rbp , and %r12-r15 are **callee-saved registers**, meaning that *they are saved across function calls*. 
This means that when writing a subroutine one must pay attention not to overwrite these registers.

Register %rsp is used as the _stack pointer_ , a pointer to the topmost element in the stack.

Additionally, ==%rdi , %rsi , %rdx , %rcx , %r8 , and %r9 are used to pass the first six integer or pointer parameters to called functions==. 
Additional parameters (or large parameters such as structs passed by value) are passed on the stack.
# Prologo
```Assembly
	pushq %rbp
	movq %rsp, %rbp
	sub $memoriaallocata, %rsp
```
# Epilogo
```assembly
	# mov %rbp, %rsp
	# pop %rbp
	# questi due equivalgono a leave
	leave
	ret

```