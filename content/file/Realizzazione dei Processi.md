#uni 
>Stati di esecuzione di un processo:
>![[statidiesecuzionediunprocesso.svg]]

Il processore esegue un solo processo per volta, che si evolve nel tempo solo se si trova in ___esecuzione___, in tutti gli altri stati è fermo.

Un processo ___pronto___ è fermo solo perché il processore è già impegnato, ma può essere ___schedulato___, e andrà quindi in esecuzione tramite una istruzione di ___dispatch___.

Un processore in esecuzione può essere sospeso forzatamente con una azione che prende il nome di ___preemption___ (prelazione), attenzione però il processo non si blocca, passa invece nello stato di pronto.

Noi realizzeremo un sistema a ___priorità fissa___, ovvero ad ogni processo è assegnata una priorità numerica e il sistema si impegna a garantire che in qualsiasi momento sia in esecuzione il processo a priorità maggiore tra tutti quelli pronti. Ci impegnano inoltre a garantire che un processo non possa attivarne altri a priorità maggiore della propria.

Inoltre il nostro sistema sarà monoutente e monoprogramma, ma multiprocesso.
Tra i sistemi multiprocesso distinguiamo:
- ___sistemi a memoria comune___
- ___sistemi a scambio di messaggi___: tutti i processi hanno propria memoria e comunicano tra loro attraverso messaggi.
Noi realizzeremo un sistema ibrido.
# Realizzazione dei Processi nel sistema didattico
Nel nostro sistema ogni processo utente ha una sua pila utente distinta da quella di tutti gli altri processi, a cui ha accesso esclusivo, mentre le sezioni `.text`, `.data` e `.bss`, e anche lo ___heap___, sono condivise tra tutti. In pratica sono condivise tutte le entità globali definite nel modulo utente, più lo heap.

Dal punto di vista del sistema ogni processo ha:
- un ___descrittore___: contiene tutte le informazioni che il sistema deve ricordare relativamente al processo. Tra queste vi è il ___contesto___ (contenuto di tutti i registri del processore), e anche le informazioni necessarie a recuperare la "foto" di tutta la memoria, memorizzata sull'hard disk.
- una propria ___pila sistema___ 

>Strutture dei dati del sistema associate ad ogni processo utente:
>![[strutturedatiprocessi.svg]]

Ogni registro ha il suo posto assegnato all'interno di Contesto, per facilità definiamo le costanti `I_RAX`, `I_RBX` ecc, che stanno per i relativi indirizzi.

Ricordo che nel nostro sistema didattico utilizziamo un solo [TSS](Protezione.md#Registro%20TR%20e%20Tast%20State%20Segment), identificato dal registro %tr, che inizializziamo solo una volta all'avvio del sistema. Per fare in modo che il meccanismo delle interruzioni utilizzi la pila sistema del processo corrente, sovrascriviamo il segmento TSS ogni volta che cambiamo processo.

- La variabile globale `puntatore` di tipo puntatore a `des_proc` punta al processo attualmente in esecuzione
- La variabile globale `pronti` di tipo puntatore a `des_proc` punta alla testa della coda dei processe pronti

Predisponiamo inoltre una coda diversa per ogni tipo di evento atteso dai processi bloccati.
Tutte queste code saranno mantenute in ordine di priorità, in modo tale da dover semplicemente estrarre il `des_proc` in testa alla coda `pronti`.

Per gestire il caso in cui tutti i processi siano bloccati, realizziamo un processo ___dummy___ a priorità minima, sempre pronto, che esegue un ciclo infinito in cui controlla il numero di processi attualmente esistenti nel sistema, se scopre che tutti i processi sono terminati, il processo dummy esegue lo ___shutdown___.
# Cambio di Processo
Il cambio di Processo può accadere solo quando il processo attuale si porta a livello di sistema, che può accadere solo in questi 3 casi:
- il processo esegue una istruzione `int`
- il processore genera una eccezione
- il processore accetta una interruzione esterna

Il processore fa quanto segue:
1. consulta l'entrata della IDT per prelevare l'indirizzo a cui saltare
2. salva in pila l'indirizzo a cui tornare
3. esegue altre azioni in base ai flag contenuti nel cancello
	- se deve innalzare il livello di privilegio, esegue il cambio di Pila, prelevando il puntatore alla nuova pila dal campo `punt_nucleo` del descrittore di processo puntato dal registro %tr
	  Tutti i Cancelli nel nostro sistema prevedono innalzamento di privilegio e la disabilitazione delle interrupt.
4. in pila (nuova o vecchia) salva il puntatore alla vecchia pila, il contenuto di %rflags, il livello di privilegio precedente l'innalzamento e l'indirizzo della prossima istruzione da eseguire

Faremo attenzione a mantenere il seguente schema per ogni codice a cui salta:
```assembly
call salva_stato
...
call carica_stato
iretq
```