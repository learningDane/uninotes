#uni 
Siccome nel [[C++]] è possibile l'**overloading** (avere più funzioni con lo stesso nome ma con parametri diversi), è necessario trovare il modo di identificare univocamente ogni funzione con i suoi parametri, se vogliamo implementare una funzione in assembly da chiamare da un file c++.
Oppure possiamo dichiarare la funzione in C++ come:
```C++
extern "C" ecc
```
questo indica al compilatore che la funzione usa il linking di [[C]] e quindi il nome non deve essere *mangled*, e può cercarlo semplicemente tramite il nome.
# tipi built-in:
==v => void==
w => wchar_t
b => bool
c => char
a => signed char
h => unsigned char
s => short
t => unsigned short
i => int
j => unsigned int
l => long
m => unsigned long
f => float
d => double
# tipi utente:
`<N><NOME>`
Dove N è il numero di caratteri di `<NOME>` e `<NOME> `è il nome del tipo ad esempio

5Punto
2st
9struttura
4elem
# Tipi composti:
P => puntatore
K => const
R => riferimento

> Le keyword su riferiscono all'oggetto immediatamente precedente (o quello successivo se non esiste un precedente, ad esempio `const int` == `int const`). 

> Const se è l'ultima keyword "cade": `void foo(int const)` == `void foo(int)`. Infatti `const` è implicito poiché alla funzione viene passato il valore.

somma(punto*) = `__Z5sommaP5punto`
# Nomi ripetuti
Se un tipo utente viene riferito più volte (ad esempio somma(st, st)) anzichè riscriverlo si usa:

S_  => per riferisi al primo tipo utente incontrato nella stringa
S0_ => per riferisi al secondo
S1_ => al terzo e così via

somma(st, st) => `_Z5somma2stS_`
somma(punto, punto, st, st*, punto*)  => `_Z5somma5puntoS_2stPS0_PS_`
# Funzioni di Classi
`_ZN<nomeNested>E<parametri>`
- N : nested
- E : end nested
- nomeNested è composto da (in ordine) tutti gli spazi di nomi che ci portano alla funzione
- il nome di ogni costrutture è "C1"
- il nome di ogni distrutture è "D1"

```asm
.global __ZN<lenght><name>C1E[parametri]

[parametro] = <composito><lenght><name>
```
# Esempio
```
cl:cl(st1&, int[])
-> 
__ZN2clC1ER3st1Pi
```
# c++filt
Questo comando può dato il mangle, darci la traduzione human readable:
```shell
$> c++filt <mangle>
humanreadable
$>
```
