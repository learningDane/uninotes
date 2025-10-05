#uni 
# Esercizi Assembler
Scrivete il file **es1.s** con il vostro editor preferito. Il comando per assemblare e collegare il primo esercizio è:
```bash
g++ -o es1 -fno-elide-constructors es1.s prova1.cpp
```
Per confrontare output:
```shell
./es1 | diff - es1.out
```
### Debug
Aggiungendo l'opzione **-g** al comando **g++** verranno aggiunte le informazioni di debug negli eseguibili.
# Assembly and C related
Open the shell in x86_64 emulation mode.
```bash
arch -x86_64 bash
```

stampare traduzione non ottimizzata da C a assembly
```shell
gcc -O0 filte.c -o filte.o # the -fverbose-asm also generates "comments"
objdump -d filte.o
```

compilare senza linking:
```C
extern int somma(int a, int b); //basta la firma della funzione

int main() {
ecc
}
```
```shell
# va fatto singolarmente su tutti i filte che vuoi compilare senza linking e poi linkare dopo
gcc -c filte.c -o filte.o
```
linkare:
```shell
gcc filte1.o filte2.o -o filtefinale.o
```
### C++
```bash
_ZnumeroCaratteriNomeFunzione+input

extern int somma(int,int);
#diventa
_Z5sommaii

>>c++filt -n _Z5somma #restituisce:
somma

>>c++filt -n _Z5sommaii #restituisce:
somma(int,int)
# c sta per char, i sta per int, P sta per puntatore, R sta per riferimento, N sta per nested
>>c++filt -n _Z5somma5punto #restituisce:
somma(punto)

>>c++filt -n _Z5sommaPi #restituisce:
somma(int*)

>>c++filt -n _Z5sommaRi #restituisce:
somma(int&)

>>c++filt -n _ZN2cl5sommaE #restituisce:
cl::somma #ovvero la funzionoe somma della classe cl

#S_ significa la prima cosa che ho tradotto come argomento di questa funzione
>>c++filt -n _Z5somma5puntoS_ #restituisce:
somma(punto,punto)

# S_ è il primo, S0_ è il secondo, S1_ è il terzo ecc
>>c++filt -n _Z5somma5puntoS_2stPS0_PS_ #restituisce:
somma(punto,punto,st,st*,punto*)
```
# Istruzioni per gli esempi di IO
Per compilare un esempio:
```bash
cd cartellaEsempio
compile
```
Per caricarlo nella macchina virtuale:
```bash
boot
```
Per caricarlo nella macchina virtuale ed usare il debugger:
```bash
boot -g
# poi aprire un altro terminale nella stessa cartella e lanciare debug:
debug
```
# Istruzioni per l'uso del Nucleo
### Scrivere un programma utente
I programmi utente vanno scritti in C++ nel file _utente/utente.cpp_ e compilati. Nello scrivere i programmi utente tenete presente che potete usare esclusivamente le funzioni di libreria dichiarate in _utente/lib.h_ e le primitive di sistema dichiarate in _include/sys.h_ e _include/io.h_. È possibile anche usare le funzioni di _libce.h_ che non accedono direttamente all'I/O o ai registri privilegiati del processore. Alcuni programmi di esempio si trovano nella directory _utente/examples_. Per provare gli esempi copiate il relativo file rinominandolo in _utente/utente.cpp_.

Una volta preparato il file *utente/utente.cpp* va compilato con:
```bash
make
```
Se tutto funziona, verranno creati (o ricreati) i file:
- _build/sistema_: il modulo sistema, risultato della compilazione di _sistema/sistema.s_ e _sistema/sistema.cpp_, caricabile dal boot loader;
- _build/utente_: il modulo utente, risultato della compilazione di _utente/utente.cpp_, _utente/utente.s_ e _utente/lib.cpp_;
- _build/io_: il modulo I/O, risultato della compilazione di _io/io.cpp_ e _io/io.s_;
In ogni caso, se lanciate _make_ (*gmake* su mac)senza aver fatto modifiche, il programma capirà che non è necessario ricompilare niente e ve lo dirà.
### Avviare il sistema
Lanciare lo script _boot_ nella directory _nucleo_:
```bash
boot
# oppure boot -g per debuggare e in un altro terminale digitare debug
```
Lo script avvia la macchina virtuale in modo che esegua il boot loader. Il boot loader abiliterà il modo a 64 bit, caricherà il programma _build/sistema_ e salterà all'etichetta _start_ (importata da libce). I messaggi che si vedono sul terminale da cui si è lanciato _boot_ sono i messaggi che arrivano dalla porta seriale della macchina virtuale. I primi sono inviati dal boot loader; poi, quando il boot loader salta al nucleo, i messaggi che si vedono sono quelli che, nel codice del nucleo, sono passati alla funzione _flog_.
### Utilizzo del debugger
Verrà avviato il debugger _gdb_ insieme ad alcune estensioni utili per il debugging del nucleo. A questo punto è possibile inserire breakpoint, eseguire le istruzioni una alla volta, esaminare le variabili etc.

_gdb_ fornisce un help in-linea che si può richiamare tramite il comando **help**. Alcuni comandi utili:
- **break**: (abbreviabile in **b**) inserisce un breakpoint in un punto del programma. L'istruzione a cui fermarsi può essere specificata come un numero di riga nel file corrente, oppure con la sintassi _nome-file:numero-di-riga_. Al posto del numero di riga si può usare anche un nome di funzione. Si noti che _gdb_ tenta di inserire il breakpoint dopo il prologo della funzione. Se la funzione non ha un prologo standard (come alcune delle nostre che manipolano lo stato del processore a basso livello), _gdb_ si confonde e inserisce il breakpoint in punti che non hanno molto senso. In genere non è un probema, ma se si vuole fermarsi alla primissima istruzione di una funzione di questo tipo conviene usare la sintassi con il numero di riga, oppure la sintassi **break ***_indirizzo_, dove _indirizzo_ è l'indirizzo dell'istruzione.
- **continue, step, step-instruction, next, finish, advance**: (abbreviabili in **c**, **s**, **si**, **n**, **fin**, **adv**). Vari modi per proseguire l'esecuzione.
    - Con **c** si prosegue fino al prossimo breakpoint (o fino alla terminazione),
    - con **s** si esegue una istruzione del linguaggio sorgente e
    - con **si** una istruzione del linguaggio macchina.
    - Con **n** si esegue una istruzione, ma senza entrare in eventuali funzioni che l'istruzione chiama.
    - Con **fin** si prosegue fino alla fine della funzione corrente.
    - **adv** richiede un parametro che è il punto del programma fino a dove si vuole avanzare (va specificato come per i breakpoint).
    Si noti che **n** usa una euristica per capire quando l'esecuzione di una funzione è terminata tenendo conto di eventuali chiamate ricorsive. Questa euristica fallisce per la nostra _carica_stato_. Se si vuole scavalcare una _call carica_stato_ conviene usare **adv** _numero-linea_, specificando il numero della linea (del file sorgente) successiva alla _call_. Il numero di linea può anche essere specificato come un numero relativo alla linea corrente (per es. **adv +1**).
- **print** (abbreviabile in **p**): stampa il risultato di una espressione (per esempio, il contenuto di una variable definita nel programma). L'espressione può anche contenere chiamate a funzioni definite nel programma. Si noti che le funzioni vengono eseguite nel contesto corrente della macchina virtuale. Nel nostro caso, se siamo nel contesto utente, chiamare funzioni di livello sistema potrebbe casare una eccezione di protezione nella macchina virtuale.
- **watch** _espressione_: permette di fermare l'esecuzione ogni volta che _espressione_ cambia valore; si noti che l'esecuzione si ferma subito dopo che l'espressione ha cambiato valore, quindi l'istruzione responsabile del cambiamento non sarà quella mostrata dall'instruction pointer, ma quella immediatamente precedente.
- **cond** _numero-del-breakpoint_ _espressione_: modifica un breakpoint esistente in modo che l'esecuzione si fermi solo quando _espressione_ è vera; si può ottenere lo stesso effetto anche quando si crea il breakpoint, aggiungendo "**if** _espressione_" dopo il normale comando di **break**.
- **set**: consente di assegnare valori a variabili del programma o di gdb (si veda avanti). La sintassi è **set** _variabile_ **=** _espressione_. L'espressione può essere specificata come per **print**.
- **call**: consente di chiamare una funzione definita nel programma. La funzione va chiamata con sintassi C++, incluse le parentesi aperte e chiuse nel caso di funzioni senza argomenti. Valgono le stesse considerazioni fatte per **print**.

Con il comando **set** è possibile anche definire variabili di gdb. Il nome delle variabili di gdb deve cominciare con **$**. Una volta definite possono essere usate come le altre, ma non è possibile prenderne l'indirizzo (quindi, in particolare non possono essere passate come argomento a funzioni del programma che vogliono un riferimento).
# Estensioni per Debugger
Nella cartella _debug/nucleo.py_ sono definite delle estensioni al debugger specifiche per il nucleo.

Le estensioni definiscono alcuni nuovi comandi che si spera facilitino la comprensione del funzionamento del nucleo, e magari anche la soluzione degli esercizi. I comandi sono i seguenti:

- **context**: questo comando viene invocato automaticamente ogni volta che il programma si blocca (per un breakpoint o single-step) e il controllo ritorna a gdb, ma può essere anche invocato esplicitamente. Mostra una serie di informazioni relative allo stato corrente della macchina: 
    - [backtrace]: lo stack delle funzioni chiamate (con la funzione più recente in cima);
    - [sorgente]: 10 righe del file sorgente intorno alla prossima istruzione da eseguire (evidenziata in reverse);
    - [variabili] il contenuto di tutti i parametri della funzione corrente e delle sue variabili locali (si noti che alcune di queste potrebbero mostrare errori fino a quando non vengono inizializzate);
    - [code processi] le liste _esecuzione_, _pronti_ e _p_sospesi_, più lo stato dei semafori la cui coda non è vuota.
    - [esecuzione] alcuni campi del descrittore del processo attualmente puntato da esecuzione;
    - [protezione] lo stato di esecuzione del processore: 
        - il livello di privilegio (utente o sistema);
        - se le interruzioni esterne mascherabili sono abilitate o disabilitate;
        - se le istruzioni io-sensitive sono permesse o vietate;
        - il contenuto del registro cr3;Se il file sorgente corrispondente all'instruction pointer attuale è un file assembly, [variabili] è sostituito da [registri] e [pila]. [registri] mostra il contenuto dei registri generali (in esadecimale) e del registro RFLAGS, decodificato. [pila] mostra la parte superiore della pila corrente. La pila è mostrata a righe di 8 byte, rappresentate in esadecimale con il byte meno significativo a destra. Per ogni riga viene mostrato l'indirizzo della riga, la riga stessa e l'offset del suo byte meno significativo rispetto a RBP. In alcuni casi vengono anche mostrate informazioni aggiuntive sul contenuto della riga, per esempio se si tratta di una delle 5 parole quadruple salvate dal meccanismo delle interruzioni (non sempre il debugger è in grado di capirlo).
- **process**: informazioni sui processi. Sottocomandi;
    - **dump** [_id_]: mostra lo stato salvato del processo _id_ (o del processo puntato da _esecuzione_ se _id_ viene omesso). Lo stato mostra: le cinque parole quadruple salvate in cima alla pila sistema; il contenuto dei registri salvati nel descrittore di processo; la prossima istruzione che il processo eseguirà quando verrà rimesso in esecuzione;
    - **list** [**system**|**user**|**all**]: elenca tutti i processi o solo quelli di sistema o solo quelli utente, in base all'argomento; se l'argomento è omesso viene assunto **all**.
- **semaphore** [**waiting**]: mostra lo stato di tutti i semafori allocati o, se viene passato l'argomento **waiting**, soltanto di quelli la cui coda non è vuota;
- **a_p**: mostra il contenuto delle righe non vuote del vettore _a_p_; per ogni riga non vuota viene mostrata parte del descrittore del relativo processo esterno.

Altri comandi sono forniti dalla libce e possono essere usati anche per il nucleo:

- **idt** [_gate_]: mostra il contenuto della riga _gate_ della IDT (o di tutte le righe non vuote della IDT, se _gate_ è omesso); per ogni riga mostra:
    - il numero del gate in esadecimale, tra parentesi quadre;
    - se il livello della routine è sistema (_sys_) o utente (_usr_);
    - se il gate è di tipo interrupt (_intr_) o trap (_trap_);
    - l'indirizzo della routine (in esadecimale);
    - tra parentesi tonde, il modulo e il nome della routine separati da due punti (uno, l'altro o entrambi potrebbero essere omessi se non noti).Inoltre, ciascuna riga è colorata in rosso se il gate non è accessibile da livello di privilegio corrente, e verde altrimenti.
- **apic**: mostra il contenuto delle righe non vuote della redirection table e dei registri IRR e ISR dell'APIC. Per ogni riga non vuota della redirection table viene mostrato:
    
    - Il numero del piedino di richiesta dell'APIC, tra parentesi quadre;
    - Se la linea è considerata attiva sul livello alto (_polarity=high_) o basso (_polarity=low_);
    - Se il riconoscimento è sul fronte (_mode=edge_) o sul livello (_mode=level_);
    - Il vettore di interruzione, su due cifre esadecimali;
    - La scritta _masked_ tra parentesi tonde, se le richieste sono mascherate (se sono abilitate non viene scritto niente).
    
    I registri IRR e ISR sono mostrati in esadecimale a gruppi di 16 bit (4 cifre esadecimali) separati da due punti; ogni gruppo rappresenta quindi una classe di priorità. La priorità aumenta da destra a sinistra. 
- **vm** **maps**|**path**|**table**|**tree**: informazioni sulla memoria virtuale. Sottocomandi:
    - **maps** [_id_]: Mostra lo stato dello spazio di indirizzamento del processo _id_ (o di quello puntato da _esecuzione_ se l'argomento è omesso); vengono mostrati gli indirizzi virtuali (in esadecimale e percorso-ottale) di ogni pagina di livello 1 e un riassunto dei relativi byte di accesso, omettendo tutte le pagine i cui byte di accesso sono identici a quelli dell'ultima pagina mostrata; _unmapped_ indica che la pagina non ha una traduzione; altrimenti viene mostrato lo stato dei vari bit (si noti che si tratta dello stato complessivo che si ottiene osservando tutti i byte di accesso nel percorso di traduzione):
        - _S_ oppure _U_: accesso consentito solo da livello sistema o anche da livello utente;
        - _W_ oppure _R_: accesso consentito in lettura/scrittura o solo lettura;
        - _PWD_: Page Write Through settato;
        - _PCD_: Page Cache Disable settato;
        - _PS_: Page Size settato (l'indirizzo fa parte di una pagina di grandi dimensioni);
        - _A_: qualche bit A è settato;
        - _D_: il bit D è settato;Inoltre, ciascuna riga è colorata in rosso se il corrispondente intervallo di indirizzi non è accessibile dal livello di privilegio corrente, in giallo se è accessibile solo in lettura, e in verde se è completamente accessibile.
    - **path** _indirizzo_[**@**_root_]: mostra il percorso di traduzione di _indirizzo_ a partire dalla tabella radice di indirizzo _root_ (o di cr3 se _root_ è omesso). Il comando mostra _root_ e, per ogni tabella presente dal livello 4 a livello 1, mostra le tre cifre ottali usate per accedere al descrittore di quel livello, lo stato dei bit R/W, U/S, A e D e, se l'entità successiva è presente, il suo indirizzo fisico; 
    - **table** _indirizzo_: mostra tutti i descrittori non completamente nulli della tabella che si trova a _indirizzo_; il formato è simile a quello usato dal sotto-comando **path**;
    - **tree** [_indirizzo_]: mostra tutto il sottoalbero presente avente come radice la tabella che si trova a _indirizzo_; il formato è simile a quello usato dal sotto-comando **path**.

Inoltre, alcuni tipi vengono mostrati in modo speciale:
- le variabili di tipo _natb_, _natw_, etc. vengono mostrate sia in decimale che in esadecimale;
- le variabili di tipo _vaddr_ vengono mostrate in esadecimale e _formato-percorso_, in cui l'indirizzo è scomposto in 4 parti, separate da trattini: la prima parte è U (utente) se i 16 bit più significativi sono tutti 1, S (sistema) se sono tutti 0 e ? altrimenti (indirizzo non normalizzato); seguono i quattro indici dei vari livelli (tre cifre ottali ciascuno).
- le variabili di tipo _tab_entry_ sono mostrate in esadecimale e poi decodificate, mostrando i flag attivi del byte di accesso; se il flag _P_ è settato viene mostrata anche una freccia seguita dall'indirizzo fisico a cui l'entrata punta, altrimenti viene scritto _unmapped_.
- i riferimenti a _tab_entry_ vengono mostrati come i _tab_entry_, ma preceduti da una chiocciola;
- i puntatori a _des_proc_ sono mostrati in esadecimale, seguiti da una freccia e alcuni campi del descrittore a cui puntano.