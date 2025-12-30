#uni 
Il Meltdown fu scoperto a Gennaio 2018, insieme a [[Spectre]], è una vulnerabilità dei processori [[Intel]] che sfrutta la tecnica dell'[[Esecuzione Speculativa]].
# Idea
L'idea è voler leggere la memoria di sistema dal livello utente, per esempio per accedere alla **finestra FM**, potendo quindi leggere la memoria di altri processi utente.
Per fare ciò si sfrutta il fatto che una eventuale eccezione di protezione viene sollevata solamente nello stadio di ritiro, quindi alcune istruzioni che seguono immediatamente una istruzione di accesso non permesso, vengono eseguite, anche se poi ne vengono annullati gli effetti.

>Pensiamo a cosa NON viene annullato: in caso di una cache read-miss, la cacheline alla quale si cerca di accedere viene caricata in cache.
# Esecuzione
Allochiamo quindi un buffer $256 \times 64$, ovvero 256 cacheline, chiamiamolo `buf`, e facciamo in modo di rimuoverlo dalla cache con determinate istruzioni, poi eseguiamo un codice come segue:
```asm
xor %rax, %rax
# mettiamo un byte 'b' dall'indirizzo proibito in %al
mov indirizzo_proibito, %al
# moltiplichiamo per 64 (così facendo 'b' diventa un indice di cacheline)
shl $6, %rax
# facciamo caricare in cache la cacheline di indice 'b'
mov buf(%rax), %rbx
```

Dopo l'istruzione di accesso proibito, vengono eseguite ma annullate durante lo stadio di ritiro anche lo shift e l'accesso al buffer, annullandone ogni effetto, tranne il caricamento in cache della cacheline di indice 'b', ovvero il byte "prelevato" dall'indirizzo proibito.

Per scoprire quante vale 'b', ed aver quindi effettivamente letto un byte dalla memoria di sistema, possiamo tentare di accedere ad ognuna delle 256 cacheline a partire da `buf`, solo per una di queste il tempo di accesso sarà di pochi cicli di clock, l'indice di questa cacheline all'interno del buffer sarà il valore del byte all'indirizzo proibito, 'b'.

Così facendo abbiamo effettivamente letto un byte dalla memoria di sistema, possiamo poi ripeterlo quante volte necessario e per esempio leggere la finestra FM.

> In risposta al meltdown, gli sviluppatori di [[Linux]] hanno fatto in modo di rimuovere la finestra FM ogni volta che il processore giri a livello utente, e ripristinarla quando si torna a livello sistema, ovviamente pagando in termini di TLB miss (vedi [[Memoria Virtuale]]).