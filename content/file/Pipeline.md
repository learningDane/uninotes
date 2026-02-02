#uni 
La **pipeline** è la prima tecnica che permette di velocizzare l'esecuzione di un flusso di istruzioni.

 Pensiamo alla CPU come ad una sequenza di moduli ([[Rete Combinatoria]]):
 - **P**: Prelievo
 - **D**: Decodifica
 - **O**: prelievo Operandi
 - **E**: Esecuzione
 - **S**: Scrittura risultato
Tra ogni coppia di modulo inseriamo inoltre un **registro di pipeline** che alla fine di ogni periodo di clock registra il risultato dello stadio della pipeline che lo precede, e all'inizio del clock successivo lo rende disponibile allo stadio della pipeline che lo segue.

Una istruzione passa da questi 5 stadi, uno per clock, questo vuol dire che mentre l'istruzione è in uno di questi stadi, gli altri moduli rimangono inutilizzati, l'idea è allora quella di processore 5 istruzioni contemporaneamente, in modo che ogni modulo sia in ogni momento in utilizzo, teoricamente moltiplicando per 5 il numero di istruzioni completate per unità di tempo (nel nostro caso 5 è il *numero di stadi della pipeline*, anche detta *profondità della pipeline*).

Necessitiamo ovviamente che il periodo di clock sia maggiore dei tempi di attraversamento di ogni rete combinatoria, più il tempo di setup dei registri:
$$\Delta=\max\{\Delta _P, \Delta_D, \Delta_O,\Delta_E,\Delta_S\} + t_\text {setup}$$
# Le Alee
Studiamo ora i problemi che potrebbero presentarsi a seguito dell'introduzione della pipeline.

Introduciamo il concetto di **bolla** (o **stallo**):
A monte di ogni registro di pipeline introduciamo un multiplexer pilotato dal **controllore di pipeline**, questo controllore decide per ogni clock che valore fornire in entrata al registro di pipeline, tramite il multiplexer. Il multiplexer ha in entrata:
1. il valore proveniente dallo stadio a monte del registro (di fatto il multiplexer "si trova tra registro e stadio a monte")
2. il valore in uscita dal registro stesso
3. una costante che codifica una "bolla"
Quando uno stadio riceve in entrata una bolla dal registro a monte, non esegue niente, semplicemente passa la bolla in uscita, al registro a valle, *la bolla quindi si propaga*.

Chiamiamo mP il multiplexer a valle dello stadio P, e così via.

> Ogni tipo di alee può essere risolto con l'introduzione di abbastanza bolle, poiché al limite se introduciamo 4 bolle nel ciclo di esecuzione di una istruzione torniamo al processore senza pipeline, che sicuramente funziona.
## Alee Strutturali
*Le alee strutturali si verificano quando due stadi diversi della pipeline accedono contemporaneamente alla stessa risorsa*.

Se per esempio in pipeline vi sono due istruzioni, una nello stadio S vorrebbe scrivere un risultato in memoria, l'altra vorrebbe prelevare un operando, nello stadio O, sempre in memoria, tramite l'uso delle bolle (quante necessarie, in questo caso una sola) blocchiamo la seconda istruzione nello stadio D, fino a che la prima istruzione non esce dallo stadio S.
Per fare questo, nel clock in cui lo stadio S vuole eseguire l'accesso in memoria, al multiplexer mP (ovvero quello che gestisce il registro a monte di D) diamo in entrata il valore che aveva appena calcolato, al multiplexer mD invece diamo in entrata una bolla, così facendo lo stadio D non eseguirà nessuna operazione (solamente porrà in uscita la costante bolla) e lo stadio S potrà eseguire indisturbato la scrittura.

> Ogni volta che ad un multiplexer il controllore da in entrata il valore in uscita al registro a valle di esso, al multiplexer immediatamente successivo deve dare in entrata la costante bolla, che poi si propagherà fino allo stadio S.

Notiamo però che poiché le istruzioni stesse si trovano in memoria, abbiamo (almeno) un'alea strutturale ad ogni clock in cui un qualsiasi stadio vuole accedere alla memoria. Introduciamo quindi due cache separate una per le istruzioni ed una per i dati.

Un'altra tecnica per ridurre le Alee Strutturali è quella di avere set di istruzioni pensati direttamente per la loro elaborazione in pipeline.
Per esempio pensando ai processori RISC ([[Architettura RISC]]):
- le istruzioni di load e store completano l'accesso in memoria nello stadio E, dunque non entrano mai in conflitto tra loro e con altre istruzioni (che abbiamo detto non accedono mai alla memoria).
- inoltre avere una grandezza prefissata per le istruzioni significa che lo stadio P può autonomamente calcolare l'indirizzo della prossima istruzione da prelevare, senza aspettare che quella attuale venga codificata.
## Alee sui Dati
*Le Alee sui Dati si presentano quando una istruzione potrebbe leggere un dato diverso da quello che avrebbe letto in un processore senza pipeline*.

Per esempio (RISC):
```asm RISC
add r1, r2, r3
sub r3, r4, r5
```
La `sub` in un processore con pipeline non leggerebbe il risultato della `add`, perché processata prima di arrivare alla fase S di quest'ultima.

Anche questa categoria di alee può essere risolta con l'utilizzo di bolle, ma non sarebbe efficiente.

Introduciamo invece un **circuito di bypass**, che fornisce in entrata al multiplexer mO (quello a valle della rete O) direttamente il risultato dello stadio E, in questo modo non dobbiamo aspettare che la `add` scriva il risultato nello stadio S e non dobbiamo inserire bolle.
## Alee sul Controllo
*Le Alee sul Controllo si verificano quando il processore con pipeline potrebbe eseguire istruzioni diverse da quelle eseguite in un processore senza pipeline*.

Questo può succedere su istruzioni di salto condizionato o istruzioni di salto indiretto.

Il problema è che l'indirizzo dell'istruzione da prelevare diventa noto solo quando ormai l'istruzione di salto si trova più avanti nella pipeline.

L'idea è cercare di indovinare subito con più accuratezza possibile quale sarà l'indirizzo a cui saltare, se alla fine dell'elaborazione dell'istruzione di salto abbiamo indovinato bene, non abbiamo dovuto inserire bolle, altrimenti tanto nessun cambiamento ha fatto in tempo a propagarsi fino alla memoria (stadio S) e possiamo semplicemente trasformare le operazioni eseguite nella pipeline in bolle.

La strategia più semplice per indovinare è una **previsione statica**: decidere se saltare o meno in base alle decisioni passate (per esempio se il salto è all'indietro probabilmente siamo in un ciclo e salteremo indietro altre volte).

Una strategia più complicata consiste nel disporre di un nuovo dispositivo di cache chiamato **Branch Target Buffer**, che memorizza informazioni sui salti che sono stati osservati in passato, il controllore decide se memorizzare in IP il valore predetto o il valore calcolato dalla pipeline. Il valore predetto è o il valore precedente di IP, incrementato di 4, oppure il valore contenuto nel BTB, se presente.

Una strategia semplice (ma inefficace) per le previsioni del BTB è semplicemente di ricordare cosa quella stessa istruzione aveva fatto le scorse volte che era stata eseguita, purtroppo però per esempio in caso di ciclo sbaglia più spesso del necessario.

Un metodo più efficace è quello di usare due bit organizzati come un contatore per saturazione, il contatore è inizialmente 0, ogni volta che quel salto viene effettuato il contatore viene incrementato, altrimenti viene decrementato. Il BTB  predirrà che il salto non verrà fatto se il contatore è negativo, fatto altrimenti.

I predittori moderni basano le loro previsioni sulla storia degli ultimi salti, memorizzata in degli shift-registers in cui ogni bit rappresenta l'esito di un salto.

Le istruzioni `ret` sono istruzioni di salto indiretto e per sapere a quale indirizzo saltano bisogna aspettare il completamento dell'istruzione in pipeline. 
Possiamo però sfruttare il fatto che le `ret` sono normalmente ad una `call`, molti processori allora hanno un **Return Address Stack** (**RAS**), che è un buffer interno del processore, organizzato a pila: ogni istruzione `call` inserisce l'indirizzo di ritorno in cima alla pila, ed ogni istruzione `ret` estrae un indirizzo dalla pila (pila LIFO). Questa è comunque una previsione perché il RAS ha una dimensione limitata ed inoltre l'uso di una `ret` non deve essere per forza legato ad una call.

> Branch Target Buffer: ![[BTB.svg]]
# Architettura con Pipeline
> Esempio di pipeline: ![[pipeline.svg]]

# Pipeline nei primi processori Intel
Intel finalmente introdusse una pipeline a 5 stadi nell'[[Intel]] 80486 del 1989. 

Per gestire la complessità del set di istruzioni, lo stadio di fetch preleva sempre 16 byte allineati naturalmente, e mantiene sempre un buffer di due di questi blocchi da 16 byte, poiché una istruzione potrebbe trovarsi a cavallo tra due blocchi.

Lo stadio di decodifica è composto in due fasi: D1 e D2, D1 decodifica al più 3 byte e comunica informazioni su come decodificare il resto a D2.

Un'altra complicazione è che le istruzioni Intel richiedono tempi molto diversi fra loro e alcune istruzioni possono richiedere anche 3 cicli di clock solamente nella fase di esecuzione.

Il 486 riuscì comunque ad andare a circa il doppio della velocità del suo predecessore anche a parità di frequenza di clock, competendo con i processori RISC ([[Architettura RISC]]) dell'epoca.