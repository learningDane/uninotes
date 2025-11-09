#uni 
[[Comandi Unix Network]] 
Unix nasce nel 1969.
Ne escono 3 derivati:
- BSD (1977)
	- Darwin (MacOS)
- GNU (1984)
	- GNU/Linux
- Solaris (1992)
# Caratteristiche di Unix
Unix è Case sensitive!
- multitasking
- multiutente
- portabile
- modulare
# Redirezione IO
I processi hanno tre canali di input/output standard:
- stdin: input da tastiera
- stdout: output da schermo
- stderr: messaggi di errore su schermo
Possiamo reindirizzare l'output dei comandi dentro file o altro:
- `>` invia stdout ad un file, se il file non esiste viene creato, se esiste viene sovrascritto
- `2>` invia stderr in un file
- `&>` invia sia stdout sia stderr in un file
- `>>, 2>>, &>>` stessa cosa ma non sovrascrive, concatena
- `comando > fileSTDOUT 2> fileSTDERR` scrive stdout in un file e stderr in un altro

- `<` recupera l'input da un file
# Pipeline
Il simbolo `|` collega l'output di un comando all'input del successivo
# Comandi Unix di base
- `shutdown` di default solo root può lanciarlo
	- `-h now` halt
	- `-r now` reboot
- `cd` change directory
- `echo "contenuto" > file.txt` sostituisce il contenuto con quello nuovo.
  Per aggiungere invece bisogna usare `echo "contenuto" >> file.txt`
- `pwd` print working directory, mostra il percorso assoluto attuale
- `ls` elenca elementi cartella attuale
	- `-l` long (più informazioni per ogni file)
	- `-a` all (anche file nascosti)
- `man` mostra il manuale contenente la descrizione esaustiva del comando specificato, la sintassi, le opzioni, i messaggi di errore
	- `man man` è il manuale di man, che è diviso in sezioni
	- `man comando` è il manuale del comando
	- `man 3 comando` va alla al manuale della funzione c di comando
	- non solo per comandi: anche funzioni del kernel, funzioni delle librerie [[Header file]], file di configurazione..
- `whatis` informazioni di base su argomento
- `apropos` serve per ricercare una parola in nomi e descrizioni, che comandi ho per fare una determinata cosa
- `mkdir nome` fa cartella
- `rmdir cartella` rimuove cartella, ma solo se è vuota
- `cp src dest`
	- `cp src1 src2 dst_dir` copia tutti i file dentro un cartella
- `mv src dest` 
- `touch nome_file` aggiorna il timestamp di accesso e modifica di un file, se il file non esiste lo crea
- `cat file1 file2` concatena il contenuto dei file e li stampa a video nello *standard output*, se è un solo file ne stampa solo il contenuto
- `rm file1 file2` rimuove file
	- `rm -r nome_cartella` cancella la cartella e tutto il suo contenuto
	- `rm -d` rimuove cartelle vuote
	- `rm -f` force: non prompta, ignora file non esistenti
- `less` visualizza file interattivamente un po' alla volta
- `head/tail` permetto di visualizzare solo la prima/ultima parte di uno o più file
	- `-c` specifica numero di byte
	- `-n` specifica numero di righe (di default 10)
- `sort`
- `su` *switch user* serve per accedere al terminale di un altro utente, se non specifico argomento, si accede al terminale di root, chiede la password dell'utente con il quale si vuole accedere
- `sudo comando` serve per lanciare un comando come un altro utente, se non specifico che utente, si intende root, l'utente attuale deve far parte del gruppo **sudoers**, viene chiesta la password dell'utente corrente
- `chmod modalità target` modalità: 777=111111111 -> rwxrwxrwx, 600=110000000 -> rw-------
# Utenti e Gruppi
Ogni **utente** nei sistemi Unix è identificato da un **username** ed un **UID numerico** (user ID, partono da 1000).
Ogni utente deve appartenere ad almeno un gruppo (normalmente il *primary group*).
Ogni **gruppo** è identificato da un **group name** ed un **GID numerico** (group ID).
### Comandi vari
```shell
passwd
# permette di cambiare la password (sfrutta il permesso SUID)

id [username]
# visualizza UID, gruppo principale e altri gruppi dell'utente corrente o di quello selezionato

groups [username]
# visualizza i nomi dei gruppi dell'utente corrente o di quello selezionato

su [username]
# switch user, permette di accedere al terminale di un altro utente, o di root

sudo -u username comando
# permette di eseguire un comando con i privilegi di un altro utente
# viene chiesta la password dell'utente correte
# l'utente attuale deve far parte del gruppo sudo
```
### Gestione utenti
Per aggiungere o rimuovere utenti è necessario avere i privilegi di root.
```shell
adduser username

deluser username
```
### Permessi di accesso al filesystem
Per ogni file (directory) sono definiti:
- utente proprietario: **owner**
- gruppo proprietario: **group owner**

Quindi per ogni file ci sono tre classi di utenti:
- owner
- utente appartenente al group owner
- **others**

A ciascuna classe di utenti vengono applicati permessi specifici; i *permessi per file* sono:
- r - read
- w - write
- x - execute (binario o script)

> il permesso di scrittura non permette di cancellare un file: per la cancellazione di un file valgono i permessi della directory

I *permessi per directory* sono:
- r - permette di leggere il contenuto
- w - permette di modificare il contenuto
- x - permette di attraversare una cartella (senza permesso non possiamo fare `cd` su quella cartella)
##### Rappresentazione simbolica dei permessi
I permessi possono essere visualizzati con
```shell
ls -l
```
output:
```shell
-rw-r--r-- 1 studenti studenti   10 ott  9 13:17 esempio.txt
drwxr-xr-x 2 studenti studenti 4096 ott  9 13:19 subDir
#--- permessi owner
#   --- permessi group owner
#      --- permessi others
# - vuol dire file
# d vuol dire directory
# i permessi sono in ordine: owner - group owner - others
```
##### Rappresentazione ottale
Per ogni classe di utenti specifica i permessi tramite una cifra in base 8. Alla cifra si somma:
- 4 se è permessa la lettura
- 2 se è permessa la scrittura
- 1 se è permessa l' esecuzione
e.g. 7->111 = rwx
e.g. 5->101 = r-x
- 777 = sono garantiti tutti i permessi a tutti gli utenti
- 750 = owner ha tutti i permessi, group owner non può modificare, others non hanno nessun permesso.
##### Cambiare i permessi
```shell
# rappresentazione ottale
chmod XXX filename

# rappresentazione simbolica
chmod [who] [how] [which] filename
# [who]={u,g,o} # owner,group owner, others
# [how]={+,-,=}
chmod -R # applica il cambiamento in modo recursivo a tutti i file e cartelle contenuti nella directory
```
Può essere eseguito solo dal proprietario del file (o con -R proprietario di tutti i file nella cartella).
##### Permessi aggiuntivi
- **SUID** - durante l'esecuzione il processo acquisisce i privilegi del proprietario del file, non di chi lo esegue.
- **SGID** - durante l'esecuzione il processo acquisisce i privilegi del gruppo proprietario del file, non di chi lo esegue.
esempio: il comando `passwd` ha il permesso SUID.
Per impostate SUID si mette `s` al posto della `x` nei permessi owner.
Per impostare SGID si mette `s` al posto della `x` nei permessi group owner.

Per la rappresentazione ottale si utilizza un'ulteriore cifra
prima delle 3 cifre relative alle classi di utenti. Questa cifra
ottale è ottenuta come somma di
- 4 se è attivo il permesso SUID
- 2 se è attivo il permesso SGID
##### Privilegi di un processo
I privilegi di un processo dipendono da:
- **effective user ID** (**EUID**)
- **effective group ID** (**EGID**)
Normalmente quando un processo viene eseguito, i suoi EUID ed EGID corrispondono direttamente all'UID e al gruppo principale dell'utente che ha eseguito il processo stesso.
Per permettere ad un comando/script di essere eseguito con
privilegi diversi rispetto a chi lo esegue, è possibile impostare
nel file i permessi SUID e SGID.
### Comandi chown e chgrp
```shell
[root] chown username file
# permette di impostare username come nuovo proprietario di file
```
## File di Configurazione
### /etc/passwd
Questo è un file con informazioni pubbliche sugli utenti
	- si può aprire in editing con `vipw`
```passwd
username:x:UID:GID:,,,:cartellaHome:/bin/bash
```
- `x` indica che la password è cifrata e si trova in `/etc/shadow` 
- `cartellaHome` indica il percorso assoluto della cartella personale home, server per impostare la variabile d'ambiente $HOME
- la shell può impostata a `/sbin/nologin` o `/bin/false` per indicare che non è possibile fare il login con tale utente
### /etc/shadow
Questo è un file contenente informazioni sensibili.
- si può aprire in editing con `vipw -s` 
```shadow
utente:$hashing algorithm$salt$hash(salt+password):ultimaModifica:etàMin:etàMax:avviso:::
```
- ultimaModifica della passowrd, contando i giorni dal 1970
- età min e max: durata minima e massima della password
- salt: caratteri casuali
- periodo di avviso: quanti giorni prima della scadenza della password viene notificato l'utente
- periodo di inattività: giorni dopo la scadenza della passwordd in cui questa è ancora accettata
- scadenza: data scadenza dell'account
- campo riservato: riservato per utilizzo futuro

su linux `sha512sum`
su macOS `shasum -a 512`

> quando l'utente inserisce la password, il sistema vi aggiunge il salt, e calcola l'Hash, che confronta con l'Hash salvato in `/etc/shadow`.

## Gestione dei Gruppi
Per aggiungere o rimuovere gruppi servono i privilegi root.
- addgroup
- delgroup
- newgrp
- gpasswd
	- solo root può aggiungere/rimuovere gli amministratori
	- se la passoword non è impostata, solo i membri del gruppo possono averne i privilegi
	- se la password è impostata, gli utenti del gruppo non ne necessitano, invece gli altri utenti possono acquisire temporaneamente i privilegi del gruppo tramite il comando `newgrp` 
	- le password di gruppo sono intrinsecamente poco sicure, in quanto conosciute da più utenti. Quindi se succede qualcosa usando quella password, non è possibile imputarlo ad una persona.
```shell
# aggiungere un utente ad un gruppo
gpasswd -a utente gruppo

# rimuovere un utente da un gruppo
gpasswd -d utente gruppo

# definire i membri di un gruppo
gpasswd -M utente1, utente2, ... gruppo

# definire gli amministratori di un gruppo
gpasswd -A utente1, utente2, ... gruppo

# impostare/cambiare la password di un gruppo
gpasswd gruppo

# rimuovere la password di un gruppo
gpasswd -r gruppo

newgrp gruppo
# con questo comando, il gruppo specificato diventa il nuovo gruppo primario dell'utente per la sessione di login corrente
```
### File di configurazione dei gruppi
#### /etc/group
File contentente informazioni pubbliche sui gruppi.
Si può aprire con il comando `vigr`.
```group
groupname:x:GID:lista,utenti
```
- `x`: vuol dire password esistente e salvata in gshadow
- altri simboli (`*` o `!`) (o campo vuoto) vogliono dire password non esistente
- lista utenti: separati da virgola, non contiene l'utente per il quale il gruppo è il **primary group**, poiché questa informazione è già in `/etc/passw
#### /etc/gshadow
File con informazioni sensibili (password e amministratori).
```gshadow
nomeGruppo:passwordcifrata:GID:amministratori:membri
```
Gli amministratori possono cambiare la password e aggiungere/rimuovere utenti al/dal gruppo.
# Processi in Unix
Unix è una famiglia di sistemi operativi multiprogrammati.
Il processo Unix mantiene spazi di indirizzamento separati per dati e codice.
Lo spazio di indirizzamento dei dati è privato, la comunicazione fra processi avviene tramite scambio di messaggi.
Lo spazio di indirizzamento del codice è invece condivisibile, più processi possono eseguire lo stesso codice.

Unix adottauna politica di assegnamento della CPU ai processi basata sulla divisione di tempo (time sharing - round robin - [[Algoritmi di Scheduling]]).
## Stati di un processo
Un processo può essere in diversi stati:
- init
- pronto
- running
- zombie
- terminato
- sleep/bloccato
- swapped
## Immagine di un processo Unix
Il descrittore di un processo (**PCB**: process control block) è suddiviso in due strutture dati distinte:
- **process structure**: informazioni indispensabili e quindi sempre in memoria
	- PID
	- Stato
	- Riferimento ad aree dati e stack
	- Riferimento (indiretto) al codice
• PID padre
• Priorità
• Riferimento al prossimo
processo
• Puntatore alla User
Structure
• ...
- **user structure**: informazioni utili solo quando il processo è in memoria
	- Copia registri CPU
• Info su risorse allocate
• Info su gestione eventi
asincroni (segnali)
• Directory corrente
• Utente proprietario
• Gruppo proprietario
• Argc, argv, path, …
• ...
## System Call per i processi
- *fork*: creazione di processi
- *exit*: terminazione
- *wait*: sospensione in attesa della terminazione dei figli
- *exec*: sostituzione di codice e dati
### PID e PPID
```c++
pid_t getpid() // restituisce il PID del processo
pid_t getppid() // restituisce il PID del processo padre
```
### fork
Ogni processo è in grado di creare dinamicamente processi.
Il processo creato (**figlio**) ha uno spazio dati separato, ma condivide con il processo **padre** il codice.
```c++
pid_t fork(void)
/*
non richiede parametri
restituisce:
- al padre: il PID del figlio, valore negativo se fallisce
- al figlio: zero
```
Il figlio condivide il codice del padre ed ==eredita dal padre una copia delle aree dati globali, stack, heap e user structure, ottiene anche lo stesso valore di PC (program counter - rip) e di tutti gli altri registri==. 

> Quindi dopo la fork, padre e figlio partono dalla stessa istruzione (la fork). Il loro comportamento viene differenziato sfruttando il valore di ritorno della fork.

### Terminazione dei processi
Esistono due tipi di terminazione:
- volontaria: `exit()`
- involontaria:
	- azioni illegali
	- interruzioni causate dala ricezione di segnali
#### exit
```c++
void exit(int status)
/*
chiamata senza ritorno (ovviamente)
permette di comunicare al padre lo stato di terminazione
*/
```
#### wait
```c++
pid_t wait(int *status)
/*
il padre può ottenere lo stato di terminazione del figlio mediante la syscall wait
wait ritorna il PID del figlio che è terminato
status è l'indirizzo della variabile dove verrà salvato lo stato di terminazione del figlio

wait sospende il padre se tutti i figli sono ancora in esecuzione
ritorno immediato con informazioni di terminazione se almeno un figlio è terminato (zombie)
ritorno con valore negativo se non ci sono figli
*/
```
##### variabile status
Contiene informazioni su come il figlio è terminato. 
Se il byte meno significativo di `*status` è zero, allora la terminazione è stata volontaria, in questo caso il byte più significato contiene lo stato di terminazione.
###### Macro per gestire status
Sono definite in `<sys/wait.h>`
- `WIFEXITED(status)` : ritorna vero se terminata volontariamente
- `WEXITSTATUS(status)` : ritorna lo stato di terminazione
### Sostituzione di codice
Un processo può sostituire il programma (codice e dati) che sta eseguendo utilizzando una syscall della famiglia `exec()`:
```c++
execl(char *path, char *arg0, ... , char *argN, NULL)
	/* lista di parametri di lunghezza variabile, terminata dal puntatore nullo
	path: percorso assoluto del comando, ad esempio "/bin/ls"
	arg0: nome del programma da eseguire
	arg1-N: argomenti del comando
	*/
execle()
execclp()
execv()
execve()
execvp()
```
Queste syscall sono senza ritorno se hanno successo
## Sincronizzazione basata sui segnali
I processi Unix aderiscono al modello ad ambiente locale: hanno uno spazio di indirizzamento privato e non hanno condivisione di variabili.
I processi possono solo sincronizzarsi (imposizione di vincoli temporali) e scambiare messaggi, mediante system calls.
### I segnali
I segnali sono **interrupt software**: permettono la notifica di eventi asincroni da parte di un processo a uno o più processi.

La ricezione di un segnale ha tre possibili effetti sul processo:
- viene eseguita una funzione di gestione (**handler**) definita dal programmatore
- viene eseguita un'azione predefinita dal sistema operativo (**default handler**)
- il segnale viene **ignorato** 
Nei primi due casi il processo si comporta in modo asincrono rispetto al segnale: l'esecuzione viene interrotta per eseguire l'handler, dopo la gestione, se il processo non è terminato, riprende dall'istruzione successiva all'ultima eseguita prima dell'istruzione.

La lista dei segnali è definita nel file di sistema **signal.h**, ciascun segnale è identificato da un intero e da un nome simbolico.
Per aprire la pagina del manuale sui segnali: `man 7 signal`.
#### Alcuni segnali
| Nome segnale | # segnale | Descrizione segnale                                                                                                                  | default handler     |
| ------------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------- |
| **SIGHUP**   | 1         | Hang up (il terminale è stato chiuso)                                                                                                | termina il processo |
| **SIGINT**   | 2         | Interruzione del processo. CTRL+C da terminale.                                                                                      | termina il processo |
| SIGQUIT      | 3         | Interruzione del processo e core dump. CTRL+\ da terminale.                                                                          |                     |
| **SIGKILL**  | 9         | Interruzione immediata. Questo segnale non può essere ignorato ed il processo che lo riceve non può eseguire operazioni di chiusura. |                     |
| SIGTERM      | 15        | Terminazione del programma.                                                                                                          |                     |
| **SIGUSR1**  | 10        | Definito dall’utente                                                                                                                 | termina il processo |
| **SIGUSR2**  | 12        | Definito dall’utente                                                                                                                 | termina il processo |
| SIGSEGV      | 11        | Errore di segmentazione.                                                                                                             |                     |
| **SIGALARM** | 14        | Il timer è scaduto                                                                                                                   | ignora              |
| SIGCHILD     | 17        | Processo figlio terminato                                                                                                            | ignora              |
| SIGSTOP      | 19        | Ferma temporaneamente l'esecuzione del processo: non può essere ignorato                                                             |                     |
| **SIGSTP**   | 20        | sospende l'esecuzione del processo. CTRL+Z da terminale                                                                              |                     |
| SIGCONT      | 18        | Il processo può continuare, se era stato fermato da SIGSTOP o SIGSTP                                                                 |                     |
### System Call per i segnali
#### signal
Permette di definire la funzione che dovrà gestire il segnale con identificativo `sig`.
```c
typedef void (*sighandler_t)(int);
sighandler_t signal(int sig, sighandler_t handler)
```
Handler può valere anche `SIG_IGN` (ignora il segnale) o `SIG_DFL` (ripristina azione di default).

Restituisce un puntatore al precedente handler del segnale, `SIG_ERR` in caso di errore.

Pagina del manuale: `man 2 signal`.
##### Figlio
Il figlio eredita dal padre le informazioni relative alla gestione.
Eventuali signal eseguite dal figlio non hanno effetto sul padre
##### exec
Le syscall exec non mantengono le associazioni segnale-handler, fatta eccezione per i segnali ignorati, continueranno ad essere ignorati.
#### kill
```c
int kill(pid_t pid, int sig)
```
Invia il segnale `sig` al processo `pid`.
- pid > 0 -> segnale viene inviato a pid
- pid == 0 -> segnale inviato a tutti i processi nello stesso process group del chiamante (tutti i figli del chiamante)
- pid == -1 -> segnale inviato a tutti i processi a cui il chiamante può inviare segnali
- pid < -1 -> il segnale viene inviato ai processi il cui `process group` è `-pid` 
#### pause
```c
int pause(void)
```
Il processo si sospende, va in stato `sleeping` fino alla ricezione di un (qualsiasi) segnale.
Ritorna `-1` se il gestore non termina l'esecuzione del processo.
#### sleep
```c
unsigned int sleep(unsigned int seconds)
```
Il processo chiamante va in stato `sleep` fino a che:
- sono passati `seconds` secondi
- arriva un segnale che non viene ignorato

Ritorna zero se è passato il tempo previsto, altrimenti il tempo rimasto dopo l'arrivo di un segnale.
#### alarm
```c
usigned int alarm(unsigned int seconds)
```
Provoca la ricezione di un segnale `SIGALRM` dopo `seconds`.
- di default il processo viene terminato
- si può avere un solo alarm, quindi se lancio due `alarm`, l'ultimo sovrascrive il primo
- se seconds è zero viene eliminato un eventuale allarme invocato precedentemente
Ritorna zero se non c'era un allarme programmato, altrimenti ritorna il numero di secondi mancanti all'ultimo allarme programmato.
### Invio di segnali da terminale
```shell
kill [options] pid [pid2..]
```
Il comando kill permette l'invio di segnali a processi da terminale. Il segnale inviato di default è `SIGTERM`.
`kill -l` mostra l'elenco dei segnali disponibili.
```shell
kill -SEGNALE pid
	# invia il segnale SEGNALE al processo pid
```
Un utente normale può inviare segnali solo ai processi di cui è proprietario.
## Visualizzazione processi - process status
```shell
ps [opzioni]
```
Il comando **ps** permette di visualizzare uno snapshot attuale dei processi in esecuzione.
```shell
-u utente # visualizza i processi dell'utente specficato
u # formato output utile all'analisi dell'utilizzo delle risorse
a # processi di tutti gli utenti
x # anche processi che non sono stati generati da terminali
o # mostra solo i campi specificati di seguito
-O # mostra i campi specificati di seguito, oltre a quelli di default
```
### Stati principali
```shell
S # sleep
T # bloccato
R # running
Z # zombie

man ps # per vedere tutti i possibili stati
```
# Gestione File
## find
Questo comando è uno strumento molto potente per trovare file, permette di effettuare la ricerca combinando dei testi sulle proprietà dei file:
- filename
- filetype
- owner
- permessi
- timestamp
La ricerca **non** è influenzata dal *contenuto* del file.
Rende inoltre possibile eseguire comandi (*actions*) sui file trovati.
```shell
find [path1 path2 ...] [espressione]
```
La ricerca viene effettuata solamente sui percorsi specificati. I percorsi vanno separati da spazio.
### return
Nome e path dei file trovati
### Espressioni
L'espressione descrive come vengono trovati i file, e quali azioni devono essere eseguiti su di essi.
Le espressioni sono composte da una sequenza di elementi:
- test: valutazione di una proprietà di un file, rende un valore booleano
- azioni: azioni da effettuare sui file trovati, ritornano true se hanno successo
- opzioni globali: influenzano l'esecuzione di test o azioni. Ritornano sempre true
- opzioni posizionali: influenzano solo le azioni o i test che seguono. Ritornano sempre true

Gli elementi di una espressione sono collegati da **operatori**:
- -o indica OR
- -a indica AND (se non specifichiamo un operatore, AND è implicito)
- ! per negare
### Elementi
#### test
```shell
-name pattern # scrivere pattern tra apici '' (oppure usare il carattere di escape) per evitare che la shell espanda i metacaratteri tipo *
-type [dfl] # directory, regular file, symbolic link
-size [+-]n[ckMG] # n: quantità di spazio ckMG: unità di misura
-user user # user specficiato come username o UID, cerca per proprietario
-group group
-perm [-/]mode # -mode: almeno permessi indicati, /mode: almeno uno dei permessi, mode: tutti i permessi
```
#### azioni
```shell
-delete # ritorna true in caso di successo (niente errori)
# SE SCRIVI -delete PRIMA DEI TEST VENGONO ELIMINATI TUTTI I FILE
-exec command ; # tutti gli argomenti specificati dopo command vengono considerati come argomenti, fino a ; (\;)
# la stringa {} è utilizzata per indicare il nome del file attualmente processato
# il comando viene eseguito a partire dal percorso di partenza del comando find
-execdir # per eseguire il comando a partire del path del file trovato
```
### esempi
```shell
find path -perm/u=w,g=w # cerca file che possono essere scritti da almeno uno fra owner e group owner
```
## locate
```shell
locate [options] file1...
```
Questo comando ricerca il/i file specificato/i.
Sfrutta un database aggiornamento periodicamente dal sistema (l'aggiornamento può essere forzato da `updatedb`, richiede privilegi di root).
Questo comando va installato `sudo apt install plocate` (lo suggerisce la shell se cercate di usarlo).
### differenze rispetto a find
- find da sempre risultati aggiornati
- plocate va installato
- locate è più facile e veloce
- find permette di definire test e azioni
## Ricerca di testo nei file
### grep
Questo comando (**general regular expression print**) permette di cercare in uno o più file di testo le linee (righe) che corrispondono ad espressioni regolari o stringhe letterali.
```shell
grep [opzioni] [-e] modello [-e modello2] file1 [file2..]
```
Se si vuole specificare più di un modello si deve utilizzare -e prima di ciascun modello incluso il primo.

| opzione | significato                                          |
| ------- | ---------------------------------------------------- |
| -i      | ignora le distinzioni fra maiuscole e minuscole      |
| -v      | mostra le linee che **non** contengono l'espressione |
| -n      | mostra il numero di linea                            |
| -c      | riporta solo il conteggio delle linee trovate        |
| -w      | trova solo parole intere                             |
| -x      | linee intere                                         |
#### regular expressions
È possibile specificare dove la stringa/espressione deve trovarsi all'interno di una riga:
```shell
'^' inizio della riga
'$' in fondo alla riga

# le parentesi quadre permettono di definire set di caratteri ammessi
grep '1[23]:[0-5][0-9]' file

'.' # indica qualsiasi carattere
	'...cept' # può essere accept o except
'*' # indica che l'espressione che procede può essere ripetuta zero o più volte
'\' # è il carattere di escape
```
##### esempi
```shell
'^stringa$' # righe che contengono solo stringa
'^$' # righe vuote
```
## Archiviazione e compressione
### tar
Il comando tar (**Tape ARchive**) permette di archiviare/estrarre una raccolta di file e cartelle
```shell
tar modalità [opzioni] [file1...]
```
Il formato del file creato dipende dalla compressione (eventualmente) utilizzata
- .tar no compr
- .tar.gz compresso con algoritmo gz
- .tar.bz2 compresso con algoritmo bzip2
#### modalità

| simbolo modalità | significato                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------- |
| A                | aggiungi file tar all'archivio (aggiungi i file presenti dentro un tar in un altro archivio) |
| c                | crea un nuovo archivio                                                                       |
| d                | trova le differenze fra l'archivio ed il file sysyem                                         |
| --delete         | cancella file dall'archivio                                                                  |
| r                | aggiungi file all'archivio                                                                   |
| t                | elenca i file di un archivio                                                                 |
| U                | aggiungi i file all'archivio, ma solo se differiscono dalla copia eventualmente già presente |
| x                | estrai file dall'archivio                                                                    |
#### opzioni

| simbolo modalità | significato                                   |
| ---------------- | --------------------------------------------- |
| v                | verbose                                       |
| z                | compressione con `gzip`                       |
| j                | compressione con `bzip2`                      |
| f                | permette di specificare il nome dell'archivio |
### gzip/gunzip e bzip2/bunzip2
Se si devono comprimere file o archivi creati precedentemente con tar, è possible utilizzare:
```shell
gzip file1 file2... #  file elencati vengono compressi e salvati in file con lo stesso nome ed estensione .gz . I file non compressi vengono eliminati
gunzip file1.gz file2.gz .. # estrae i file compressi specificati in file con lo stesso nome(senza estensione relativa alla compressione). I file compressi, dopo essere stati estratti vengono eliminati
bzip2
bunzip2 # stessa roba ma con algoritmo bzi
```
# Librerie Standard
```c++
unistd.h
	pid_t fork(void)
sys/types.h
stdio.h
stdlib.h
```
# Passaggio di parametri a programmi in C
Il main è come segue:
```c++
int main(int argc, char**argv)
// argc è il numero di argomenti
// argv è il vettore argomenti
```
quando nel terminale eseguo:
```sh
./eseguibile argomento1 ... argomentoN
```
- argv[0] è il comando eseguito
- argv[1] è il Path dal quale stiamo eseguendo
- da argv[2] in poi sono gli argomenti passati