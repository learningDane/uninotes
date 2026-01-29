#uni 
Per gestire le interruzioni esterne introduciamo l'**APIC** (Advanced Programmable Interrupt Controller), che si trova nei sistemi Intel ed emulato nella nostra macchina QEMU.
L'APIC possiede 24 piedini di ingresso, alla quale si collegano le interfacce.
Questo controllore permette la gestione *vettorizzata* delle richieste di interruzione, ovvero ogni sorgente di interruzione è associato un **tipo** numerico, comunicato alla CPU insieme alla richiesta. La CPU utilizza questo tipo per consultare una tabella, la IDT, che associa i tipo agli indirizzi delle routine.

La **IDT** è una tabella che il programmatore può scrivere ovunque in memoria (salva poi l'indirizzo nel registro **IDTR**) e associa ad ogni **tipo** di interruzione la relativa **routine di servizio**. 
Il programmatore inizializza l'APIC dove desidera, poi con l'istruzione `lidtr` carica nel registro IDTR l'indirizzo dove l'ha caricata.

La [[CPU]] è collegata alla APIC con ==INTR== (interrupt request) in entrata ed ==INTA== (interrupt acknowledge) in uscita.
- La tastiera è collegata al piedino 1 della APIC (INT quando RBR è pieno o TBR si svuota dopo una scrittura)
- il timer è collegato al piedino 2 della APIC (INT quando il contatore 0, se programmato, termina il conteggio)
- l'HDD è collegato al piedino 14 della APIC (INT quando il buffer è pieno dopo una operazione di lettura o vuoto dopo una operazione di scrittura)
- Nota che tastiera e hard disk generano interruzioni solo se queste sono state abilitate nell'interfaccia.
Inoltre la APIC è collegata al BUS, sul quale comunica il tipo di interrupt alla CPU.

INTR e INTA servono per implementare un *protocollo di handshake*:
1. quando l'APIC vuole inviare una richiesta di interruzione attiva INTR
2. la CPU, se `IF==1`, dopo ogni istruzione controlla INTR, se lo trova attivo, setta INTA. (le richieste arrivate mentre `IF==0` verranno servite non appena IF torna ad 1)
3. quando l'APIC trova INTA ad 1, passa il tipo alla CPU sul BUS e disattiva INTR
4. quando la CPU vede INTR disattivo, legge il tipo e disattiva INTA

Nella APIC il programmatore può decidere per ogni piedino, tramite il relativo registro interno:
- il tipo su 8bit
- se il riconoscimento di una nuova richiesta deve essere riconosciuta *sul fronte* o *sul livello* 
- se il segnale di ingresso deve essere considerato attivo alto o basso
- se le richieste devono essere ignorate o meno (*mascherate*)

La APIC ha i seguenti registri:
- **IRR** (Interrupt Request Register a 256 bit (un bit per ogni tipo = $2^8$)
- **ISR** (In Service Register) a 256 bit
- **EOI** (End Of Interrupt)

---
*Riconoscimento sul fronte*:
La APIC (parlando di ***riconoscimento sul fronte***) ciclicamente:
1. ad ogni fronte di un piedino, setta il relativo bit in **IRR** (interrupt request register)
2. se il bit relativo nel registro **ISR** è disattivo, la APIC comincia la handshake alla CPU per comunicarle la interrupt ed il tipo
3. quando il processore accetta la interrupt, comunica il tipo sul BUS e sposta il bit da IRR a ISR

Adesso la APIC suppone che il processore stia eseguendo la routine di servizio, finché il bit di ISR relativo ad un piedino è settato, nuove richieste in arrivo non vengono inoltrate, setta solo il relativo bit in IRR.
Il processore comunica alla APIC che la routine è terminata scrivendo un valore qualsiasi nel registro **EOI** della APIC. A seguito di ciò la APIC resetta il bit relativo al tipo della interrupt nel registro ISR, a questo punto nuove interruzioni su quel piedino (o interruzioni già presenti se il bit di IRR relativo è già settato) ricominciano ad essere inoltrate alla CPU.

Essenzialmente IRR tiene conto delle interrupt in attesa e ISR tiene conto delle interrupt attive.

---
*Riconoscimento sul livello*:
Se un piedino è invece configurato per il ***riconoscimento sul livello***, IRR diventa ininfluente, quando l'APIC riconosce un segnale sul piedino e il relativo bit di ISR è disattivo, setta il bit e si comporta con il processore come per il riconoscimento sul fronte, *se invece il relativo bit di ISR era già attivo, la richiesta viene ignorata fino a quando una EOI non resetterà il relativo bit di ISR*.

Il riconoscimento sul livello è utile per alcuni dispositivi/situazioni, l'idea è che la scrittura in EOI (che azzera il bit di ISR) deve arrivare DOPO che il processore ha comunicato alla relativa periferica che la richiesta è stata presa in carico, dunque, se all'arrivo dell'EOI la richiesta è ancora attiva, deve trattarsi di una nuova richiesta.
Con il riconoscimento sul fronte invece se una richiesta di interruzione arriva sul piedino $i$ mentre il relativo bit di IRR è già attivo, la richiesta viene ignorata perché la APIC riconosce solamente il fronte e quindi all'arrivo della EOI la APIC vedrà il collegamento $i$ settato ma non agirà di conseguenza perché aspetta un fronte.

---
# Gestione annidata delle interruzioni
Per gestire il caso di più interruzioni simultanee normalmente si preferisce la gestione annidata, ovvero una interruzione più importante di una interruzione attiva, entra in esecuzione e blocca l'interruzione attuale.

Il tipo di interruzione viene interpretato dall'APIC anche come priorità: *i 4 MSb sono la priorità dell'interruzione (crescente)*.
Quando una nuova richiesta viene registrata in IRR, se questa ha priorità più alta di ogni interruzione attiva in ISR, la APIC sposta il bit relativo in IRR in ISR come al solito e comincia l'handshake con la CPU, che accetta l'interruzione annidata.
Quando il processore scrive in EOI, l'APIC resetta il bit a 1 più significativo in ISR, supponendo che il processore stia gestendo le interrupt secondo la disciplina LIFO, dopodiché ricontrolla le priorità di IRR e ISR e agisce di conseguenza.

Quando la APIC controlla la classe di priorità ovviamente guarda solamene ai 4 bit MSb, ignorando quelli bassi, tuttavia quando poi comunica il tipo alla CPU comunica tutto il byte.
# Condivisione delle richieste di interruzione
Per molto tempo è stata pratica comune collegare più periferiche allo stesso piedino della APIC, per esempio con una porta OR. 

Per far funzionare questo metodo però dobbiamo impostare il riconoscimento sul livello invece che sul fronte: se impostassimo il riconoscimento sul fronte richieste contemporanee di due periferiche si maschererebbero a vicenda, con il livello invece la periferica inizialmente mascherata manterrà il suo collegamento settato finché la CPU non interagirà direttamente con lei.
È inoltre necessario che ogni dispositivo collegato ad un piedino condiviso, presenti un registro dal quale si evinca se abbia inviato una richiesta di interruzione, poiché questi dispositivi hanno tutti lo stesso tipo, questo è l'unico modo per differenziare il comportamento della routine.

La porta OR permette la condivisione se il piedino è configurato come attivo alto, se vogliamo un piedino configurato come attivo basso dobbiamo utilizzare sulle interfacce condivise una uscita *open-collector*, collegate al piedino in configurazione *wired-or*.
In questo modo le interfacce normalmente tengono l'uscita in alta impedenza e il livello alto è dato dalla resistenza, detta di *pull-up*, collegata alla tensione di alimentazione ($V_{CC}$), quando una interfaccia vuole comunicare una interruzione, collega la sua uscita a massa, portando tutta la linea al livello basso.