#uni 
```bash
arch -x86_64 bash
```

stampare traduzione non ottimizzata da C a assembly
```shell
gcc -O0 filte.c -o filte.o
objdump -d filte.o
```

compilare senza linking:
```C
extern int somma(int a, int b); //basta la firma della funzione

int main() {
ecc
}
```
```shell
# va fatto singolarmente su tutti i filte che vuoi compilare senza linking e poi linkare dopo
gcc -c filte.c -o filte.o
```
linkare:
```shell
gcc filte1.o filte2.o -o filtefinale.o
```
# C++
```bash
_ZnumeroCaratteriNomeFunzione+input

extern int somma(int,int);
#diventa
_Z5sommaii

>>c++filt -n _Z5somma #restituisce:
somma

>>c++filt -n _Z5sommaii #restituisce:
somma(int,int)
# c sta per char, i sta per int, P sta per puntatore, R sta per riferimento, N sta per nested
>>c++filt -n _Z5somma5punto #restituisce:
somma(punto)

>>c++filt -n _Z5sommaPi #restituisce:
somma(int*)

>>c++filt -n _Z5sommaRi #restituisce:
somma(int&)

>>c++filt -n _ZN2cl5sommaE #restituisce:
cl::somma #ovvero la funzionoe somma della classe cl

#S_ significa la prima cosa che ho tradotto come argomento di questa funzione
>>c++filt -n _Z5somma5puntoS_ #restituisce:
somma(punto,punto)

# S_ è il primo, S0_ è il secondo, S1_ è il terzo ecc
>>c++filt -n _Z5somma5puntoS_2stPS0_PS_ #restituisce:
somma(punto,punto,st,st*,punto*)
```