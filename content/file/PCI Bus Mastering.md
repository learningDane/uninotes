#uni 
> Bus Mastering PCI: ![[BUSmasteringPCI.svg]]

I dispositivi che sono in grado di essere iniziatori (il ponte BUS-PCI lo è sempre) sono detti **BUS Master** e devono essere dotati dei collegamenti REQ/GNT verso l'**arbitro**, il quale ha il compito di coordinare i vari BUS master sull'accesso al bus.

Quando un bus master desidera iniziare una transazione attiva REQ, l'arbitro se decide di cedergli il controllo del bus attiva il relativo GNT.
Siccome per ottimizzare i tempi l'arbitro può assegnare il controllo anche durante una transazione già avviata da un altro bus master, il bus master che ha ricevuto il GNT, prima di iniziare a pilotare le linee del BUS, attende che `FRAME#` e `IRDY#` siano disattivi (poiché questo segna la fine della transazione come abbiamo visto; [[Bus PCI]]).

Tutto questo ovviamente è completamente trasparente al software e si comporta come se il dispositivo fosse collegato direttamente al BUS principale.

Il ponte è configurato in modo da comportarsi come obiettivo per ogni transazione di memoria con indirizzi appartenenti alla RAM che si trova sul BUS principale e in caso di uscita (da RAM a dispositivo) traduce semplicemente la transazione sul bus principale, in caso di entrata invece copia temporaneamente i dati da trasferire in un buffer interno (**posted writes**) e inizia le necessarie operazioni di scrittura in DMA verso la RAM.

Il ponte sul bus si comporta esattamente come nel caso di un solo dispositivo DMA (vedi [[DMA]]).

Anche il BUS PCI offre una operazione di tipo *write-and-invalidate* (vedi [[DMA#Ottimizzazioni per il trasferimento di Intere Cacheline]]) che può essere sfruttata da BUS masters con l'intenzione di sovrascrivere intere cacheline.

> Nota che lo standard PCI prevede che il software comunichi ai dispositivi la dimensione di una cacheline (poiché lo standard è indipendente dal processore), in particolare il software di inizializzazione (in genere il PCI BIOS) deve scrivere la dimensione della cacheline in "**Cache line size**" nello spazio di configurazione delle varie funzioni (vedi [[Bus PCI#Spazio di configurazione]]).
# Interazione con il meccanismo delle interruzioni
La presenza della bufferizzazione intermedia dei dati da trasferire crea un problema con i trasferimenti in ingresso e le interruzioni: quando il dispositivo ha trasmesso i dati al ponte vuole inviare una richiesta di interruzione poiché dal suo punto di vista ha terminato l'operazione di scrittura, questa richiesta di interruzione potrebbe però arrivare prima che il ponte finisca di completare l'operazione sulla RAM, in questo caso il software potrebbe accedere al buffer prima che l'operazione sia effettivamente conclusa.

> Soluzione software:
> Possiamo sfruttare il fatto che il ponte gestisce con disciplina FIFO tutti i trasferimenti tra bus locale e bus pci, nella routine di gestione della interruzione inseriamo allora una lettura da un registro del dispositivo coinvolto, il software quindi verrà bloccato fino alla fine della operazione da parte del bus e la conseguente lettura del registro.
> D'altronde spesso una lettura da registro del dispositivo è già necessaria per segnalare la gestione della richiesta di interruzione, questa lettura quindi assolve ad entrambi i compiti e non dobbiamo risolvere niente.

> Soluzioni hardware:
> - si crea un collegamento di handshake tra il controllore delle interruzioni e il ponte: prima di inoltrare una richiesta di interruzione, il controllore chiede il permesso al ponte, il quale ovviamente non accetterà fino alla fine del trasferimento verso la RAM (soluzione adottata dalla nostra macchina QEMU).
> - soluzione più moderna: le richieste di interruzione non viaggiano su linee separate ma vengono trasmesse (codificate) direttamente sul bus PCI stesso, queste sono **message signaled interrupts**. In questo modo, sempre grazie alla disciplina FIFO del ponte, l'interruzione verrà inoltrata sul bus locale solo dopo la fine del trasferimento verso la RAM.