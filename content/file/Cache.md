#uni 
L’unità di trasferimento utilizzata dal controllore cache
è detta **cacheline**.
Un esempio tipico è di avere cacheline di 64 byte, allineate
naturalmente.
# Politiche di cache
Per le operazioni di lettura:
- **read hit**: se la cacheline richiesta è presente in cache completa la lettura con i dati presenti in cache
- **read miss**: se la cacheline richiesta non è presente in cache il controllore deve leggere la cacheline della memoria, scriverla nella cache dati a partire dalla posizione dettata dall’indice, e aggiornare l’etichetta; a questo punto i dati sono in cache e si procede come nel caso precedente

Per le operazioni di scrittura:
- **write miss**: se la cacheline è assente:
	- **write no-allocate**: il processore completa la scrittura in memoria senza caricare la cacheline in cache
	- **write allocate**: il processore carica la cacheline in cache e quindi procede poi come con una *write hit*.
- **write hit**: se la cacheline è presente:
	- **write back**: il processore aggiorna solo la cache
	- **write through**: il processore aggiorna sia la cache sia la memoria

Si noti che nel caso di write back la cacheline dovrà essere riscritta in memoria prima di essere rimpiazzata da un’altra cacheline, perché altrimenti le scritture eseguite dal programma andrebbero perse.

La tecnica è comunque conveniente se il programma riesce ad eseguire tante scritture sulla stessa cacheline prima che questa debba essere scritta, in quanto si riduce il numero di scritture in memoria.

Per evitare scritture inutili, inoltre, il controllore cache può associare ad ogni cacheline un *bit dirty* e porlo a 1 quando il processore ha eseguito almeno una scrittura in quella linea.
Le cacheline che hanno il bit dirty a zero non hanno bisogno di essere riscritte in memoria.

> Le cache moderne sono tipicamente write-allocate e write-back
# Cache ad indirizzamento diretto
Si noti che, in caso di read miss, una eventuale cacheline che si trovava in cache allo stesso indice di quella appena caricata verrà rimpiazzata. Questo è il difetto principale delle cache ad indirizzamento diretto: due cacheline che hanno lo stesso indice non possono essere mantenute contemporaneamente in cache, anche se il resto della cache è vuota.
![[Pasted image 20251213123720.png]]
# Cache Associativa a Insiemi
