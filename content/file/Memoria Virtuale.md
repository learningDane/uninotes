#uni 
La memoria virtuale è un'astrazione che ci permette di ottenere:
- Isolamento tra processi
- semplicità nel collegamento dei programmi
- semplicità nel caricamento/scaricamento dei processi
- possibilità di condivisione di memoria
"Nascondiamo" la memoria fisica, effettiva, ai processi, e introduciamo la memoria virtuale in modo del tutto trasparente dal punto di vista di questi ultimi.
# Paginazione
Dividiamo la memoria virtuale, in *regioni naturali*, dette **pagine**, di dimensione $4 \ KiB$.
Facciamo altrettanto con la memoria fisica, la dividiamo in **frame** della stessa dimensione delle pagine.
Introduciamo adesso un modo per tradurre gli indirizzi virtuali in indirizzi fisici, ovvero un modo di trovare in memoria fisica, in quale frame abbiamo caricato una pagina.

> Si ricorda che nei processori [[Intel]]/[[AMD]] di architettura [[AMD64]] solo gli $x$ bit meno significativi possono effettivamente assumere un valore qualsiasi, dove $x$ vale $48$ o $57$ a seconda del modello. I $64-x$ bit più significativi devono essere tutti uguali al bit numero $x-1$ (contando da $0$). Noi consideriamo il caso con $x=48$.

Ogni indirizzo è composto di:
- **numero di pagina** (o di **frame** se parliamo di indirizzi fisici)
- **offset** all'interno della pagina o del frame: i $12$ bit meno significativi

> Traduzione da indirizzo virtuale ad indirizzo fisico: ![[traduzioneIndirizzo.svg]]
# MMU
Per eseguire questa traduzione introduciamo un nuovo dispositivo, tra [[CPU]] e [[Cache]], la **memory management unit** (**MMU**). Questa intercetta gli indirizzi (virtuali) generati dalla CPU e li traduce, utilizzando la **tabella di corrispondenza** *attiva*, in indirizzi fisici.
## Funzioni aggiuntive
La tabella di corrispondenza può essere usata per associare ad ogni pagina ulteriori informazioni oltre al numero di frame. 
Le entrate delle tabelle che si trovano nell'architettura AMD64 sono le seguenti:
- un flag **P**, presence
	- la `activate_p()` si occupa di porre a zero tutti i bit P di tutte le pagine delle quali il programma non ha bisogno
- un flag **R/W** 
	- indica se il frame è disponibile in lettura e scrittura o in sola lettura (per esempio la sezione .text, anche se l'[[Architettura di Von Neumann]] fu introdotta apposta per permettere questa operazione, viene spesso impedita per questioni di sicurezza, tipicamente viene completamente vietata per i processi utente)
- un flag **U/S** 
	- siccome i processi utente possono comunque avere bisogno di saltare a codice in memoria sistema, nelle tabelle di corrispondenza dei processi utenti devo anche rendere disponibile parte della memoria M1 (memoria sistema), devo però proteggere questi frame da accessi in modalità utente, setto quindi il relativo bit U/S.
- due flag **PWT** (page write trough) e **PCD**(page cache disable), per comandare la [[Cache]].
	- settare PWT è utile quando si ha a che fare con la memoria video: la CPU desidera che quando effettua una scrittura questa avvenga subito per permettere la visualizzazione a video, ma invece di leggere dalla memoria video è più veloce leggere dalla cache.
- due flag **A** e **D**, utili per lo [[Swap]]
	- la MMU setta il bit A di una entrata quando la utilizza (ovvero accede ad un indirizzo in quella pagina)
	- la MMU setta anche il bit D se l'operazione effettuata è una scrittura
	- l'idea è che quando carico una pagina in memoria, resetto ogni A e D, in questo modo posso tenere di conto di quali pagine vengono utilizzate di più con A (addirittura possiamo introdurre la paginazione su domanda, sfruttando l'[eccezione](Eccezioni.md) trap di tipo *page fault*), mentre con D riconosco, al momento di rifare una swap-out, quali pagine sono effettivamente state modificate e caricare solo quelle sul dispositivo di swap, siccome quelle non modificate sono già presenti, questo permette di risparmiare costosi (in termini di tempo) accessi al dispositivo di swap.
# Trie-MMU
Se calcoliamo quanto spazio occupa **una** singola tabella di corrispondenza otteniamo:
$$\begin{matrix} \text{Numero di pagine}=\frac{2^{48}}{2^{12}}=64\text{Gi pagine}
\\
\text{Dimensione di una tabella}=64\text{Gi} \times 8 \text{B}=512 \text{GiB} \end{matrix}$$
Ovviamente è una dimensione improponibile per anche solo una tabella.

Introduciamo quindi la **Trie-MMU**, un dispositivo dotato di una memoria interna (atta a memorizzare una particolare struttura dati, la *trie*, che contenga in maniera non ridondante ogni tabella di corrispondenza) e di un registro **cr3**, che serve ad individuare la tabella di corrispondenza attiva ad ogni istante.
## Trie
La struttura dati utilizzati dalla Trie-MMU è una **bitwise trie**, una variante della trie.

I trie sono strutture dati ad albero che permettono di mappare chiavi di tipo stringa in valori.
Gli archi dell'albero sono contrassegnati con i caratteri delle chiavi e il valore associato ad ogni chiave si trova nella foglia che si raggiunge partendo dalla radice e seguendo il percorso indicato dalla chiave.

Generalmente nei trie il valore associato alla chiave può trovarsi anche in un nodo intermedio, non necessariamente in una foglia. Questo non accade nel bitwise trie che interessa a noi.
### Implementazione
Un modo di implementare un trie è di avere in ogni nodo dell'albero un puntatore ad array di 128 entrate, ciascuna delle quali contiene il puntatore al prossimo nodo in base al codice ASCII del prossimo carattere della chiave.
Se un nodo contiene un puntatore nullo indica che il trie non contiene chiavi con il corrispondente prefisso.

L'inserimento di una nuova associazione chiave/valore nel trie comporta una ricerca, ma creando eventuali nodi mancanti fino alla foglia che deve contenere il valore.
# Paginazione Reale
Quanto abbiamo visto fin'ora è una versione semplificata della paginazione, osserviamo ora l'implementazione della paginazione adottata nei processori reali [[AMD64]].

La MMU non può essere un dispositivo con registro e memoria interna, sarebbe troppo complicato, offre invece semplicemente un modo in hardware di effettuare la ***table walk***.

Il numero di pagina viene diviso in 4 sezioni da 12 bit ognuna, ovvero 3 cifre in base 8. Ognuno dei 4 livelli del trie viene identificato da una di queste sezioni.
Il registro **%cr3** (che è nel processore!) contiene l'indirizzo della tabella di livello 4, che contiene i 512 descrittori di tabelle di livello 3.

Un descrittore di tabella, composto da 8 byte (64 bit), contiene in ordine:
- il bit P
- il bit R/W
- il bit U/S
- (bit 3-4 - al posto di PCD e PWT)
- il bit A
- (bit 6 - al posto di D)
- un bit PS
- (bit 8-11)
- ==l'indirizzo della tabella di livello inferiore (su 40 bit)==
- (i bit 63-52 che nella architettura [[AMD64]] non possiamo cambiare liberamente)
Questa è la struttura dei record delle tabelle di livello 4,3 e 2.

La struttura delle tabelle di livello 1 è leggermente diversa, in quanto *non contiene identificatori di tabelle ma identificatori di pagine*, che contengono in ordine:
- bit P
- bit R/W
- bit U/S
- bit PWT
- bit PCD
- bit A
- bit D
- (bit 11-7)
- ==numero di frame (su 40 bit)==
- (bit 63-52)
## Traduzione
> Traduzione da indirizzo virtuale a fisico, con pagine da 4 KiB: ![[traduzionevera4KiB.svg]]

Notiamo che la moltiplicazione è ovviamente solamente una concatenazione con 3 bit a zero, mentre la somma è anch'essa una sola concatenazione poiché abbiamo detto che le tabelle sono **allineate naturalmente**.

L'indirizzo fisico di un record di una tabella di livello $i$ è dunque: $$\big[ \text{indirizzo della tabella  di livello } i \text{ : } \text{indice di livello } i \text{ : } 3'b000\big]$$
quindi un indirizzo fisico è su: 36 bit + 12 bit + 3 bit = 40 bit di numero di frame + 12 bit di offset = 52 bit, contro i 48 bit di un indirizzo virtuale.
## Funzioni aggiuntive
Oltre alla traduzione la MMU:
- controlla tutti i bit P, se anche solo un bit è a zero, la MMU smette di tradurre e solleva una eccezione di *page fault* 
- controlla tutti i bit R/W, se anche solo un bit non permette la scrittura, l'operazione è disabilitata
- controlla tutti i bit U/S, se anche solo un bit non lo permette, l'operazione (lettura o scrittura) è disabilitata
- passa al controllore cache le informazioni contenute nei bit PWD e PCD nel descrittore di livello 1
- pone a 1 tutti i 4 bit A incontrati
- in caso di scrittura pone a 1 il bit D nella tabella di livello 1 (i descrittori di livello maggiore non hanno il bit D)
## Risparmio di Memoria
Il risparmio di memoria deriva dal fatto che le tabelle sono allocate unicamente se servono, in maniera dinamica, e in condizioni normali saranno sempre un numero limitato.
## Traduzioni per il sistema
Quando la CPU opera in modalità sistema vorremmo che potesse usare direttamente gli indirizzi fisici, idealmente vorremo che la MMU smettesse di tradurre gli indirizzi in modalità sistema, questo però non possiamo farlo, allora carichiamo in memoria alcune tabelle, contenente le **traduzioni identità** di tutta la memoria fisica. Queste tabelle ovviamente avranno il flag U/S settato a sistema, e saranno caricate all'inizio della memoria M2.
Questa "finestra" sulla memoria fisica viene caricata in memoria prima dell'inizializzazione della MMU.

> Se fosse così semplice, come abbiamo detto, queste traduzioni occuperebbero $512 \text{GiB}$ in memoria, invece possiamo sfruttare il meccanismo delle [[#Pagine grandi]].
## Pagine grandi
Abbiamo detto che i descrittori di tabelle contengono il bit **PS**, questo bit può essere settato ad uno nei descrittori di tabella di livello 3 e di livello 2.

Quando in un descrittore di tabella di livello 2 settiamo il bit PS, al posto del puntatore alla tabella di livello 1 troviamo un campo **F** nei bit 21-51: la MMU utilizza ora come offset all'interno della pagina i primi **21** bit: otteniamo quindi una pagina di $2^{21}=2 \text{MiB}$ invece dei soliti $4 \text{KiB}$.
In questo modo abbiamo eliminato la relative tabella di livello 1, risparmiando il relativo spazio.
# Memoria Fisica in Memoria virtuale
Decidiamo di mettere le tabelle del Trie nella memoria M2, poiché come le pagine utente, le tabelle sono grandi 4KiB e devono essere allineate naturalmente, ogni tabella occupa dunque esattamente un frame di M2, possiamo quindi utilizzare una stessa lista di frame liberi sia per l'allocazione delle tabelle che delle pagine.
Il modulo sistema deve allora poter accedere a tutta M1 e a tutta M2, deve quindi poter accedere a tutta la memoria fisica, indipendentemente da quale sia il TRIE attivo.

idealmente vorremmo avere una MMU che si disattiva ogni volta che il processore gira a livello sistema, ma non è possibile.
Creiamo allora una serie di traduzioni "identità", che traducano ogni indirizzo in se stesso, inseriamo infine queste traduzioni nello spazio di indirizzamento di ogni processo.
Questo insieme di traduzioni prende il nome di **finestra FM**, ovviamente questa finestra è accessibile solo da livello sistema (U/S = sistema).

Questa finestra deve essere creata prima di attivare la memoria virtuale: all'avvio del sistema.
# TLB
Vorremmo evitare di dover fare fino a 4 accessi in memoria (table walk) per ogni operazione in memoria, introduciamo quindi il **TLB** (**translation lookaside buffer**), una cache specifica per la MMU.

Questa cache "ricorda" le traduzioni più recenti (traduzioni contenute nei descrittori di livello 1)