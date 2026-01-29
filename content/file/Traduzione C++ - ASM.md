#uni 
# Allineamento e Dimensione delle strutture
1. Una struttura ha per allineamento il *massimo* degli allineamenti dei suoi membri
2. *Ogni* membro di una struttura deve rispettare il suo allineamento
3. I membri di una struttura sono disposti in memoria nello stessi ordine in cui il programmatore li ha dichiarati
# Variabili Globali
```c++
int a =  10; // 4 byte
int main () {...}
```
---
```asm
.data
a: .long 10
```
# Variabili Locali
```c++
void funzione () {
	int a = 10;
}
```
---
```asm
.set a, -4
.text
	push %rbp
	movq %rsp, %rbp
	subq $16, %rsp
	# stack deve essere allineato a 16
	
	movq $10, %rax
	movq %rax, a(%rbp)
```
# Main
```C++
int main() {
	...
	return xxx;
	}
```
---
```asm
.global main
main:
prologo:
	push %rbp
	movq %rsp, %rbp
	subq yyy, %rsp

epilogo:
	movq xxx, %rax
	leave
	ret

```
# Parametri di funzione
```C++
void funzione(int &var , int n1 , int n2) { }
// int &var è un indirizzo -> 32 bit su qemu, 64 irl
```
---
```asm
.global funzione
.set var -8
.set n1 -12
.set n2 -16

funzione:
	push %rbp
	movq %rsp, %rbp
	# 8 byte + 4 byte + 4 byte
	subq $16, %rsp
	
	# l'ordine in cui li mettiamo in stack è a nostro piacimento
	movq %rdi, var(%rbp) #8byte
	movq %esi, n1(%rbp) #4byte
	movq %edx, n2(%rbp) #4byte
```
# Costruttore di Classe
```C++
struct st1 {
	char vc[8];
}

class cl {
	st1 s;
	int v[4];
}

cl::cl(char c, st1& s2) {}
```
---
```
/*
cl:
1 2 3 4 5 6 7 8
+-----------+
|   st1     | 0
+-----------+
| v[0] v[1] | 8
+-----------+
| v[2] v[3] | 16
+-----------+

stack:
7 6 5 4 3 2 1 0
+--------+
|  ----  |
+--------+ 
| ind S2 | -24
+--------+
|    c   | -16
+--------+
|  this  |  -8
+--------+
| vecRBP |  0 
+--------+
*/
```
- %RDI = this
- %RSI = c
- %RDX = indirizzo di s2
- %RCX
- %r8
- %r9
---
```asm
.global _ZN2clC1EcR3st1
.set this -8
.set c -16
.set s2 -24
 
.set st1_classe 0
.set v_classe 8
_ZN2clC1EcR3st1:
	push %rbp
	movq %rsp, %rbp
	subq $32, %rsp
	
	movq %rdi, this(%rbp)
	movb %sil, c(%rbp)
	movq %rdx, s2(%rbp)
	
	# per inserire qualcosa in v[2]_classe
	
```