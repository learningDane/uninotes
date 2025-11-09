#uni 
La [[CPU]] è collegata alla **APIC** con INTR (interrupt request) in entrata ed INTA (interrupt acknowledge) in uscita.
- La tastiera è collegata al piedino 1 della APIC
- il timer è collegato al piedino 2 della APIC
- l'HDD è collegato al piedino 14 della APIC
Inoltre la APIC è collegata al BUS, sul quale comunica il tipo di interrupt alla CPU.

La **IDT** è una tabella che il programmatore può scrivere ovunque in memoria (salva poi l'indirizzo nel registro **IDTR**) e associa ad ogni **tipo** di interruzione la relativa **routine di servizio**. 

Nella APIC il programmatore può decidere per ogni piedino:
- il tipo su 8bit
- se il riconoscimento di una nuova richiesta deve essere riconosciuta sul fronte o sul livello
- se il segnale di ingresso deve essere considerato attivo alto o basso
- se le richieste devono essere ignorate o meno (*mascherate*)

La APIC ha i seguenti registri:
- IRR a 256 bit (uno per ogni tipo = $2^8$)
- ISR a 256 bit
- EOI

La APIC (parlando di ***riconoscimento sul fronte***) ciclicamente:
1. ad ogni fronte di un piedino, setta il relativo bit in **IRR** (interrupt request register)
2. se il bit relativo nel registro **ISR** è disattivo comunica la interrupt al processore
3. quando il processore accetta la interrupt, comunica il tipo sul BUS e sposta il bit da IRR a ISR
INTR e INTA vengono utilizzate per un handshake come segue:
4. quando l'APIC vuole inviare una richiesta di interruzione setta INTR, poi attende INTA
5. il processore, se il flag IF è settato, dopo ogni istruzione controlla il valore di INTR, quando lo trova settato, setta INTA
6. l'APIC vedendo INTA settato, comunica al processore il tipo di interruzione, poi resetta INTR
7. quando il processore vede INTR disattivo legge il tipo dal BUS ed infine resetta INTA, completando l'handshake
Adesso la APIC suppone che il processore stia eseguendo la routine di servizio. Il processore comunica alla APIC che la routine è terminata scrivendo un valore qualsiasi nel registro **EOI** della APIC. A seguito di ciò la APIC resetta il bit relativo al tipo della interrupt nel registro ISR.

Essenzialmente IRR tiene conto delle interrupt in attesa e ISR tiene conto delle interrupt attive.

Se un piedino è invece configurato per il ***riconoscimento sul livello***, IRR diventa ininfluente, quando l'APIC riconosce un segnale sul piedino e il relativo bit di ISR è disattivo, setta il bit e si comporta con il processore come per il riconoscimento sul fronte, se invece il relativo bit di ISR era già attivo, la richiesta viene ignorata fino a quando una EOI non resetterà il relativo bit di ISR.
Il riconoscimento sul livello è utile per alcuni dispositivi/situazioni, l'idea è che la scrittura in EOI (che azzera il bit di ISR) deve arrivare DOPO che il processore ha comunicato alla relativa periferica che la richiesta è stata presa in carico, dunque, se all'arrivo dell'EOI la richiesta è ancora attiva, deve trattarsi di una nuova richiesta.
Con il riconoscimento sul fronte invece se una richiesta di interruzione arriva sul piedino $i$ mentre il relativo bit di IRR è già attivo, la richiesta viene ignorata perché la APIC riconosce solamente il fronte e quindi all'arrivo della EOI la APIC vedrà il collegamento $i$ settato ma non agirà di conseguenza perché aspetta un fronte.
# Gestione annidata delle interruzioni
Per gestire il caso di più interruzioni simultanee normalmente si preferisce la gestione annidata, ovvero una interruzione più importante di una interruzione attiva, entra in esecuzione e blocca l'interruzione attuale.

Il tipo di interruzione viene interpretato dall'APIC anche come priorità: i 4 MSb sono la priorità dell'interruzione (crescente). Quando una nuova richiesta viene registrata in IRR, se questa ha priorità più alta di ogni interruzione attiva in ISR, la APIC sposta i bit in ISR come al solito e comincia l'handshake con la CPU, che accetta l'interruzione annidata.
Quando il processore scrive in EOI, l'APIC resetta il bit a 1 più significante in ISR, supponendo che il processore stia gestendo le interrupt secondo la disciplina LIFO, dopodiché ricontrolla le priorità di IRR e ISR e agisce di conseguenza.

Quando la APIC controlla la classe di priorità ovviamente guarda solamene ai 4 bit MSb, ignorando quelli bassi, tuttavia quando poi comunica il tipo alla CPU comunica tutto il byte.
# Condivisione delle richeiste di interruzione
Per molto tempo è stata pratica comune collegare più periferiche allo stesso piedino della APIC, per esempio con una porta OR. Per funzionare però questo metodo dobbiamo impostare il riconoscimento sul livello invece che sul fronte:
se impostassimo il riconoscimento sul fronte richieste contemporanee di due periferiche si maschererebbero a vicenda, con il livello invece la periferica inizialmente mascherata manterrà il suo collegamento settato finché la CPU non interagirà direttamente con lei.
# Implementazione software delle routine
Abbiamo visto che per ogni tipo di interruzione vi è un record nella IDT che gli associa un indirizzo a cui saltare dove il processore trova la routine di sistema relativa; il salto viene effettuato via software salvando l'attuale contenuto di RIP nello stack, sovrascrivendo il registro con l'indirizzo contenuto nella IDT ed anche salvando nello stack il registro dei Flag.
Una volta finita la routine come fa il processore a tornare al sottoprogramma principale? Una RET non basta poiché non dobbiamo solamente ripristinare RIP, utilizziamo quindi l'istruzione **IRETQ**, che si occupa di tutto quanto.
# Eccezioni
Le prime 32 entrate della IDT, sono riservate per le eccezioni.
Con questo termine indichiamo condizioni speciali, o errori, che il processore rileva durante la sua normale esecuzione.

Le eccezioni sono classificabili come segue:
- **trap**: vengono sollevate *tra* l'esecuzione di una istruzione e la successiva (penso che sia legato al cambiamento di `%rip`)
- **fault**: vengono sollevate *durante* l'esecuzione di una istruzione
- **abort**: possono verificarsi in qualsiasi momento e indicano errori particolarmente gravi