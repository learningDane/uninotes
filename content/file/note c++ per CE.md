#uni 
# typedef
```c++
typedef unsigned short natw;
typedef unsigned short ioaddr;
```
# Esempi
[[C++#Typecasting]]
```c++
natw* video = reinterpret_cast<natw*>(0xb8000);	// array di 2000 word;
	// Nei PC compatibili IBM, 0xb8000 è l’indirizzo base della text mode video memory (schermo in modalità testo 80x25 a colori).
	// reinterpret_cast converte l'argomento in natw*
	// ovvero converte il numero(indirizzo) 0xb8000 in un puntatore a natw
	// quindi dichiariamo un puntatore a natw chiamato "video" e gli assegnamo il valore di 0xb8000
	// NON posso fare direttamente nat* video = 0xb8000 perché 0xb8000 è un INT
	// devo speficare al compilatore che 0xb8000 è un indirizzo di memoria del tipo natw*
```