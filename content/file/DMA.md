#uni 
Per ora abbiamo visto due modalità di trasferimento dati da dispositivo a memoria:
- a controllo di programma
- ad interruzioni
Vediamo ora la modalità **DMA**, **Direct Memory Access**, che prevede che sia direttamente il dispositivo ad eseguire le necessarie operazioni di scrittura o lettura sulla RAM, una volta istruito dal software.

In generale il software vuole eseguire un trasferimento tra dispositivo ed un buffer in memoria, quindi comunica al dispositivo l'indirizzo del buffer, il numero di byte e il tipo di operazione, d'ora in poi l'operazione è presa in carico dal dispositivo, che la eseguirà e notificherà il software alla conclusione.

Analizziamo prima il caso con un solo dispositivo DMA (quando saranno più di uno ci ricollegheremo facilmente a questo caso): 
colleghiamo il dispositivo direttamente al BUS locale, questo però può essere pilotato da solo un dispositivo alla volta, DMA o CPU, introduciamo quindi i collegamenti **HOLD** e **HOLDA** (hold acknowledge) fra dispositivo e CPU, l'accesso al BUS verrà quindi arbitrato come segue:
1. il dispositivo normalmente mantiene i suoi piedini in uscita in alta impedenza;
2. quando il dispositivo vuole eseguire un trasferimento, attiva HOLD
3. la CPU in risposta, al termine dell'accesso in corso se presente, mette i suoi piedini in uscita in alta impedenza e attiva HOLDA
4. il dispositivo esegue l'accesso ed infine disattiva HOLD
5. la CPU disattiva HOLDA e continua ad operare come suo solito

Nota che il dispositivo avvia il protocollo HOLD/HOLDA ogni volta che ha qualche byte da trasferire, ma in generale non completerà l'operazione con un solo trasferimento e dovrà ripetere l'handshake più volte per una sola operazione.

Essenzialmente la CPU da al DMA priorità nell'accesso al BUS, questa tecnica è chiamata **cycle stealing**.

Durante un trasferimento in DMA (HOLD e HOLDA attivi) la CPU può solo svolgere istruzioni senza operandi in memoria.

> Il software deve fare attenzione a non accedere al buffer per tutta la durata del trasferimento DMA.
# Interazione con la cache
> Interazione tra DMA e controllore Cache:![[DMAeCACHE.svg]]

Introduciamo la cache, i collegamenti di handshake devono ora essere collegati al controllore cache, poiché è questa e non la CPU ad interagire con il BUS.

> Adesso la CPU sarà in grado di eseguire MOLTE più istruzioni poiché avrà a disposizione anche gli operandi in cache, il rallentamento della CPU dovuto al cycle stealing con la cache è *trascurabile*.

Nascono però complicazioni con l'introduzione della cache, in particolare problemi di consistenza tra contenuto in ram e contenuto in cache, nel caso di cache hit, ovviamente nel caso di cache miss nulla cambia rispetto a quanto visto sopra.
## Cache Write-Through
Ovviamente possiamo ignorare il caso di Cache miss.

Per quanto riguarda le cache hit, poiché stiamo parlando di una cache write through, il contenuto in RAM è sempre aggiornato quindi le *Uscite* (da RAM a DMA) non danno problemi.

Parlando di *Entrate* invece, alla fine del trasferimento il contenuto in RAM è più aggiornato del contenuto in cache, dobbiamo quindi o invalidare la cache o aggiornare il contenuto.

> Soluzione *hardware*:
> Sia DMA che controllore cache sono collegati direttamente sul bus, il controllore cache può quindi controllare cosa sta facendo il dispositivo dma, in particolare può controllore a quali indirizzi accede ed invalidare le relative cacheline, questa tecnica si chiama ***snooping***.
> Se il controllore cache riceve in ingresso anche le linee dati, può automaticamente aggiornare il contenuto in cache, questa tecnica si chiama ***snarfing*** (solitamente non è prevista nei processori [[Intel]]).

Per esempio i processore ARM non realizzano questa soluzione (snooping) in hardware.

> Soluzione *software*:
> Disponiamo di alcune istruzioni che sono in grado di invalidare il contenuto della cache, per intero o in base ad un intervallo di indirizzi.
> Queste istruzioni devono essere eseguite per invalidare le cacheline coinvolte nel buffer SUBITO DOPO la conclusione del trasferimento.
## Cache Write-Back
La cache write back porta problemi anche ai trasferimenti in uscita, poiché se una cacheline è dirty il contenuto in RAM non è consistente con il contenuto in cache.
### Soluzione software
Sia per Ingressi che per Uscite: il programmatore può ordinare al controllore cache di eseguire una write back di tutte le cacheline coinvolte nel buffer, SUBITO PRIMA di avviare il trasferimento.

> Nota che durante il trasferimento DMA il software non deve modificare nessuna cacheline coinvolta nel trasferimento, nemmeno byte non coinvolti nel buffer. 
> Il modo più facile per assicurare ciò è avere buffer di dimensioni multiple di cacheline, allineati alla dimensione della cacheline.
### Soluzioni hardware
#### Uscita
- Miss oppure Hit NON Dirty: normale lettura in Ram.
- Hit Dirty: adesso vorremmo che o il controllore eseguisse una write-back prima che il dispositivo legga dalla RAM, oppure vorremmo che il dispositivo legga direttamente dalla cache.
  ==Per implementare una di queste due soluzione necessitiamo però di modificare il protocollo di accesso alla RAM==
#### Entrata (con snarfing)
- Miss: normale scrittura in Ram.
- Hit NON Dirty: snooping con invalidazione della cacheline.
- Hit Dirty: snooping *con snarfing* (nota che molti controllori non implementano lo snarfing).
#### Protocollo di accesso alla RAM modificato (necessario se non disponiamo dello snarfing)
Dividiamo l'accesso alla RAM in più fasi distinte:
1. una prima fase a cui la RAM non partecipa, qui il dispositivo comunica alla cache a quali indirizzi desidera accedere, il controllore cache risponde con il segnale hit/miss e l'eventuale stato del bit Dirty.
   Questa fase è detta di *snooping* (impropriamente perché non si svolge in segreto)
2. una o più fasi che dipendono dall'esito della fase di snooping.
##### Uscita
- Cache Miss oppure Cache Hit NON dirty: normale lettura
- Hit Dirty: una soluzione possibile è che il dispositivo cede il controllo al controllore cache, il quale esegue una *write-back*. Il dispositivo può anche leggere i dati mentre transitano sul bus (snooping con snarfing), altrimenti dopo la write-back può eseguire una normale lettura come nel caso di Hit NON Dirty.
##### Entrata (senza snarfing)
Se il controllore non implementa lo snarfing possiamo utilizzare il protocollo di accesso alla RAM modificato come per una uscita:
- Cache Miss: scrittura normale
- Hit Non Dirty: snooping con invalidazione della cacheline
- Hit Dirty: abbiamo più soluzioni possibili:
	- il dispositivo DMA cede il controllo alla cache, la quale esegue una write-back, successivamente il dispositivo scrive in RAM.
	- il dispositivo DMA cede il controllo alla cache, la cache quindi comunica la cacheline Dirty SOLO al dispositivo DMA, infine il dispositivo scrive sulla cacheline comunicatagli e la scrive in RAM (soluzione emulata dalla nostra macchina QEMU).
### Ottimizzazioni per il trasferimento di Intere Cacheline
Queste ottimizzazioni sono possibili se il dispositivo DMA vuole SCRIVERE intere cacheline.
#### Hardware
Se il dispositivo DMA vuole sovrascrivere una intera cacheline e la Cache viene informata, è sufficiente che la cache invalidi la cacheline, come se non fosse dirty, e la fase di snooping non è più necessaria.

Aggiungiamo quindi al protocollo del BUS una istruzione "**write and invalidate**", che il DMA può usare ogni volta che desidera scrivere una intera cacheline.

Una ulteriore ottimizzazione è scomporre il trasferimento in diverse operazioni, al più due normali scritture all'inizio e alla fine (se il buffer non è allineato e/o multiplo di cacheline), e più *write and invalidate* in mezzo.
#### Software
Se il processore dispone di una istruzione di invalidazione cache SENZA write back possiamo utilizzarla SUBITO PRIMA di un trasferimento di intera cacheline in DMA.

Anche in questa soluzione software possiamo scomporre un generico trasferimento in più operazioni, quelle intermedie che coinvolgono intere cacheline, ed eventualmente normali scritture all'inizio e/o fine del trasferimento (se il buffer non è allineato e/o multiplo di cacheline).
# Interazione con la memoria virtuale
Poiché il dispositivo DMA non ha alcun modo di accedere alla MMU, non ha modo di utilizzare indirizzi virtuali, dobbiamo quindi utilizzare i seguenti accorgimenti:
- al dispositivo va comunicato l'indirizzo *fisico* del buffer
- se il buffer attraversa più pagine non tradotte in frame contigui, l'operazione va scomposta in più operazioni, ognuna che riguarda frame contigui
- la traduzione degli indirizzi coinvolti non deve cambiare durante il trasferimento

Alcuni dispositivi possono essere programmati per eseguire autonomamente più operazioni in successione, specificando per ognuna indirizzo del buffer e dimensione, altrimenti va automatizzata in software la programmazione di trasferimenti uno dopo l'altro.