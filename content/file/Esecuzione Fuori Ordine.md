#uni 
Il limite principale della pipeline ([[Pipeline]]) è la sua natura strettamente sequenziale: se una istruzione richiede più tempo per essere eseguita (per esempio in caso di Cache miss ([[Cache]]) le istruzioni dopo rimangono bloccate in attesa che questa termini.

Con la tecnica dell'esecuzione fuori ordine invece analizziamo le istruzioni, e se non dipendono da una istruzione bloccata, vengono comunque eseguite, anche se localizzate nel programma dopo l'istruzione "lenta".
# Dipendenza tra le istruzioni
Date due istruzioni `j` ed `i`, con `j` dopo `i`:
```asm
i: add x, y, z
j: add a, b, c
```
Diremo che `j` dipende da `i`:
- *per i dati* se `j` usa direttamente o indirettamente il risultato prodotto da `i` (legge dal registro in cui `i` scrive)
- *per i nomi* se `j` scrive in un registro utilizzato da `i` 
	- **antidipendenza**: `j` scrive in un registro dal quale `i` legge
	- **dipendenza in uscita**: `j` scrive in un registro sul quale `i` scrive
- *per il controllo* se `j` deve essere eseguita o meno in base al risultato prodotto da `i`

tabella riassuntiva: 

| i/j | r                     | w                     |
| --- | --------------------- | --------------------- |
| r   | -                     | dati                  |
| w   | nomi (antidipendenza) | nomi (dip. in uscita) |

Problema: le dipendenza per il controllo richiedono la conoscenza dell'intero programma, ma la CPU non conosce il programma, è costretto quindi ad assumere che *ogni* istruzione dopo una istruzione di controllo dipenda per il controllo da essa.

Nota che le dipendenze sono proprietà del programma da eseguire (le alee invece sono situazioni indesiderate che dipendono dalla struttura del processore) e *se non correttamente gestite* possono portare ad alee.
# Architettura per l'esecuzione fuori ordine
Facendo riferimento alla pipeline ([[Pipeline]]):

Rimuoviamo gli stadi di: lettura Operandi, Esecuzione, Scrittura operandi, ed introduciamo:
- uno **stadio di Emissione**, che riceve le istruzioni in ordine dallo stadio di decodifica e decide se lasciarle proseguire o meno
- più **Unità di Esecuzione**, che lavorano in parallelo
- una **Dashboard**, che contiene i registri e informazioni su ognuno di essi: 
	- un flag `W` che vale 1 se qualche istruzioni in esecuzione ha quel registro come destinatario.
	- un contatore `C` che conta quante istruzioni in esecuzione hanno quel registro come sorgente.

*Le istruzioni che si trovano negli stadi di esecuzione possono essere completate in qualsiasi ordine*.

*Il compito di evitare le alee spetta allo stadio di emissione*.

Notiamo che le uniche dipendenza che possono generare alee sono quelle tra una nuova istruzione in arrivo e quelle che si trova nelle unità di esecuzione, poiché dipendenza tra una istruzione in arrivo e istruzioni già completate non danno problemi.

Lo stadio di emissione:
- quando emette una istruzione setta il campo `W` del destinatario e incrementa il campo `C` dei sorgente.
- quando una istruzione viene completata fa il contrario
- quando riceve una istruzione:
	- controlla i campi `W` e `C` del registro destinatario, se anche uno è diverso da zero, entra in stallo, fino a che entrambi i campi non tornino a zero. 
	- controlla il campo `W` dei registri sorgente, se anche uno è diverso da zero entra in stallo, fino a che entrambi non tornino a zero.

> Quindi lo stadio di emissione emette una istruzione (operativa o di salto) solamente se il suo registro destinatario non è utilizzato e i suoi registri sorgente non sono oggetto di scrittura (da parte di istruzioni in esecuzione).
## Ottimizzazione delle dipendenza sui dati
Ogni stallo dello stadio di emissione rallenta l'esecuzione del flusso di istruzioni, introduciamo le **stazioni di prenotazione**, buffer in cui lo stadio di emissione inserisce istruzioni che devono attendere altre istruzioni per via di dipendenza, in questo modo riduciamo gli stalli.

In particolare lo stadio di emissione inserisce una istruzione con dipendenze in una stazione di prenotazione libera, dove l'istruzione ad ogni clock monitora lo stato dei flag dei propri registri, entrando nell'unità di esecuzione solo quando permesso.

È possible avere stazioni di prenotazione in grado di memorizzare più istruzioni, con disciplina FIFO.
## Ottimizzazione delle dipendenza sui nomi
Notiamo che in generale quando indichiamo un registro come operando sorgente, quello che vogliamo indicare realmente è il suo contenuto, il risultato di una istruzione precedente, se avessimo un numero di registri sufficiente potremmo salvare ogni risultato in un diverso registro, e non avremmo più dipendenze sui nomi. 

Ovviamente questo è irrealizzabile, però effettivamente non ci interessa eliminare tutte le dipendenze sui nomi, ma solo quelle che possono portare ad alee, ovvero le dipendenze sui nomi tra istruzioni in esecuzione contemporaneamente, che sono un numero gestibile: ci basta un registro diverso per contenere il risultato di ogni istruzione in esecuzione.

Per aumentare il numero di registri disponibili al programmatore però dobbiamo cambiare il set di istruzioni (o perlomeno la loro codifica), e comunque programmi già compilati non potrebbero usufruire di altri registri.

Decidiamo allora di aggiungere registri in modo trasparente al software, introducendo lo **stadio di rinomina dei registri** tra lo stadio di decodifica e quello di emissione. 

Chia
# Struttura pipeline con esecuzione fuori ordine

> Struttura della pipeline dotata di esecuzione fuori ordine, con ottimizzazione delle dipendenze: ![[pipeline_con_esec_fuori_ordine.svg]]
# Istruzioni che accedono alla memoria
Rispetto alle istruzioni operative o di salto abbiamo difficoltà in più:
- non possiamo avere una dashboard che contiene `W` e `C` per ogni byte della memoria
- per sapere se ci sono sovrapposizione di indirizzi, vanno prima calcolati (`offset`+`base`)

Prevediamo allora una unica unità di esecuzione per le scritture in memoria, in questo modo le `st` sono eseguite nell'ordine in cui vengono emesse, *evitando le alee dovute a dipendenze sui nomi in uscita*.

---
Abbiamo inoltre uno **store buffer**, in cui le `st` vengono inserite ed estratte con disciplina FIFO una alla volta. Ogni entrata di questo buffer contiene un campo indirizzo (che deve essere calcolato) ed un campo dato, quando entrambi i campi sono stati riempiti l'istruzione è pronta e verrà eseguita quando tutte le scritture precedenti verranno terminate.

L'istruzione verrà rimossa dallo store buffer solo quando la scrittura sarà completata, in questo modo lo store buffer contiene tutte le scritture *in corso* ovvero istruzioni emesse e non ancora terminate, le uniche che possono causare alee.

Le istruzioni di lettura (`ld`) devono avere uno o più **load buffer** (l'ordine delle letture non è importante), ogni entrata del buffer contiene l'indirizzo al quale l'istruzione vuole leggere.

Per poter proseguire una istruzione `ld` deve attendere che tutte le istruzioni di scrittura emesse (quelle nello store buffer) calcolino il loro indirizzo, in caso di sovrapposizione la `ld` deve attendere che le `st` problematiche vengano completate, *evitando le alee dovute alle dipendenze sui dati*.
Come ottimizzazione una `ld` che trova una `st` con sovrapposizione di indirizzo nello store buffer, può prendere il dato direttamente da li, questa tecnica prende il nome di **store forwarding**.

---
Infine prevediamo che ogni istruzione `st`, appena il suo indirizzo è stato calcolato, attenda che vengano calcolati gli indirizzi delle `ld` che erano già in qualche load buffer quando la `st` è stata emessa e deve attendere che le `ld` con indirizzi con sovrapposizione vengano prima completate, *evitando le alee dovute alle antidipendenze*.

> In breve, le `st` vengono eseguite in ordine una alla volta e attendono che vengano completate le `ld` emesse prima di loro (se c'è sovrapposizione), le `ld` possono essere eseguite contemporaneamente e devono solo aspettare che vengano completate le `st` emesse prima di loro (se c'è sovrapposizione).

# Esecuzione fuori ordine nei primi processori Intel
[[Intel]] riuscì ad implementare l'esecuzione fuori ordine nel Pentium Pro del 1995.

Il trucco, utilizzato da tutti i processori Intel da quel momento in poi, è di codificare internamente le istruzioni x86 in microistruzioni simil-RISC, molto più facili da implementare con pipeline ed esecuzione fuori ordine.

Infine oltre ai registri architetturali (rax ecc) si usano anche registri **microarchitetturali**, non accessibili al programmatore, per contenere risultati intermedi.