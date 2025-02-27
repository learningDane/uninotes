#uni 
```bash
arch -x86_64 bash
```

stampare traduzione non ottimizzata da C a assembly
```shell
gcc -O0 main.c -o main.o
objdump -d main.o
```

compilare senza linking:
```C
extern int somma(int a, int b); //basta la firma della funzione

int main() {
ecc
}
```
```shell
gcc -c main.c -o main.o
```
linkare:
```shell
gcc somma.o main.o main
```