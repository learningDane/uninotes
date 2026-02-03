#uni 
# 2026.01.15
---
- Supponiamo di avere un sistema con CPU, memoria e dispositivo DMA. Come funziona il DMA e che problemi ci potrebbero essere? Disegna lo schema. Cosa deve avere un dispositivo DMA? Il DMA deve sapere indirizzo e numero di byte, una volta che sa queste cose, cosa fa? Perché necessitiamo di HOLD (hold request) e HOLDA (hold acknowledge)? Cosa può fare la CPU durante un trasferimento DMA (r: istruzioni che operano su registri interni o cache)? Se ordino un trasferimento di 1000 byte in DMA, quante volte si svolge l'handshake (r: il DMA fa l'handshake ogni volta che ha byte pronti da trasferire)? Esempio: il DMA è collegato ad una tastiera, chiediamo al DMA di trasferire 1000 caratteri dalla tastiera alla memoria (r: il DMA farà molto probabilmente 1000 handshake, una per ogni volta che l'utente digita sulla tastiera).
voto: Conferma voto dello scritto (24).
---
- domanda:
```c++
des_sem *s = &array_des_sem[i];

// A cosa corrisponde questa cosa in assembly?

// Lo scriva in pseudo-assembly
```
- Cosa fa il processore quando accetta una richiesta di interruzione esterna? Che passaggi svolge? La IDT si trova sempre allo stesso indirizzo? Come fa la CPU a sapere dove viene caricata la IDT (r: si usa l'istruzione `lidtr`)? Che informazioni si trovano in una riga della IDT (r: bit di presenza, indirizzo a cui saltare, campo L, campo DPL)? Cosa fa il processore con questi campi? Perché il processore salva quelle cose nella pila di sistema, se effettua il cambio di pila ovviamente? Perché non salva in pila sistema il contenuto di TUTTI i registri?
voto: 19.
---
- Allo schema disegnato alla prima domanda aggiungiamo una cache write-through, cosa cambia? Se ho `int x; char buf[1000]; int y;` cosa può succedere (r: x o y possono essere nelle cacheline toccate dal buffer, dobbiamo usare padding e/o dire al compilatore di allineare il buffer)?
voto: 26.
---
- Supponiamo di voler usare il meccanismo delle interruzioni ma senza nucleo, quindi vogliamo scrivere un programma, che contiene una parte principale ed una parte che gestisce l'interruzione, che inizializzazioni dobbiamo fare affinché le interruzioni mettano in esecuzione il codice che vogliamo?
voto: Rimandato.
---
- La MMU quando deve tradurre un indirizzo fa una table-walk, come funziona e quanti accessi in memoria (nel caso peggiore) deve fare (r: lettura delle 4 tabelle + scrittura dei 4 bit A + scrittura del bit D nella tabella di livello 1 = 8 perché bit A e D della tabella di livello 1 si scrivono insieme)? Faccia lo schema delle entrate delle tabelle. Faccia lo schema della traduzione. I `+` e i `*` nella traduzione rendono necessari addizionatori e moltiplicatori nella MMU (r: no se le tabelle occupano una pagina e sono allineate naturalmente)? Se trovo il bit A già settato nella tabella di livello 4, cosa vuol dire (r: sto facendo un accesso ad una regione di livello 4 a cui ho già accceduto)?
voto: 28.
---
- Supponiamo di voler usare il meccanismo delle interruzioni ma senza nucleo, quindi vogliamo scrivere un programma, che contiene una parte principale ed una parte che gestisce l'interruzione, che inizializzazioni dobbiamo fare affinché le interruzioni mettano in esecuzione il codice che vogliamo, faccia l'esempio del timer (r: so a che piedino dell'apic arrivano le interruzioni di nostro interesse, settiamo nell'apic il registro relativo al piedino (non possiamo usare i primi 32 tipi), configuriamo il timer, impostiamo il gate della IDT relativa al tipo deciso, il DPL non serve per le interruzioni esterne, disabilitiamo interruzioni nel gate ed infine mettiamo l'indirizzo dell'handler desiderato, ATTENZIONE dobbiamo caricare l'indirizzo della IDT nel registro IDTR tramite l'istruzione `idtr`, infine abilitiamo le interruzioni con la istruzione `sti`)? Dobbiamo avere particolari accorgimenti durante la scrittura dell'handler (r: ci serve `iretq`, dobbiamo mandare EOI all'apic, salva_stato e carica_stato, perché vengono ripristinati solo i registri scratch altrimenti)?
voto: 24.
---
- Torniamo al DMA e supponiamo di avere una cache write-back, cosa cambia rispetto alla write-through (r: )? Io ho una cache write-back, faccio una scrittura, quando è che questa cacheline verrà effettivamente trasferita in RAM (r: quando si rende necessaria una sostituzione della cacheline in cache, prima di sostituirla si aggiorna la RAM, altrimenti i cambiamenti andrebbero persi)? Che ottimizzazioni possiamo avere nel caso di bit dirty e scrittura DMA (r: se il DMA vuole scrivere una intera cacheline la invalidiamo nella cache e il DMA scrive nella RAM)?
voto: 23.

# 2026.02.03
---
- Cosa Contiene il TLB? Disegna lo schema (TLB associativo a 2 vie). Quali bit in più sono presenti nei descrittori di pagina virtuale (risp: A,P,PS)? Perché questi bit non sono presenti nel TLB? Oltre ad usare TLB diversi per pagine di diverse dimensioni, quale altra soluzione è possibile per il bit PS? Come si utilizza e aggiorna il bit D nel TLB? Perché va aggiornato subito in memoria attraverso una table-walk invece di lasciarlo in TLB e successivamente scriverlo in memoria (stile write-back)?
voto: conferma voto dello scritto (30).