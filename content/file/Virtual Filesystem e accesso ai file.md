#uni 
Tutti i dischi e le relative partizioni vengono rese accessibili (**montati**) mediante un unico **filesystem virtual**.
# Mount
Il comando per rendere accessibile un filesystem in una determinata posizione del filesystem virtuale è mount:
```shell
sudo mount /dev/sdb1/mnt/usb
sudo umount /mnt/usb

mount -t vfat /dev/sdb1/mnt
```
Il file di configurazione con le informazioni relative al montaggio del filesystem all'avvio è: `/etc/fstab`.
# Filesystem in Unix
I sistemi [[Unix]] ([[Linux]]) sono caratterizzati dall'**omogeneità**:
- ogni risorsa del sistema è rappresentata come un file
- esistono 3 tipi di file:
	- file ordinario: informazioni allocate in memoria di massa
	- file speciale: dispositivo fisico
	- directory: insieme di file: il contenuto di una directory è costituito da una serie di record che descrivono il contenuto della directory.

Una parte del disco è dedicata alla `i-List`, la lista di tutti i descrittori di file (`i-node`), ciascun `i-node` viene riferito e identificato mediante un `i-number`.
L'`i-node` descrive le caratteristiche del file:
- tipo (ordinario, speciale, firectory)
- permessi (owner, group owner, permessi)
- dimensione
- link: numero di nomi che riferiscono al file (hard links)
- vettori di indirizzamento: permettono di accedere al contenuto
- etc..

Quando viene creato un file di nome "fileName":
1. viene creato il descrittore (`i-node`), a cui viene associato un `i-number` "N" e aggiunto alla `i-list`
2. al contenuto della directory viene aggiunto un nuovo record:
   `<fileName, N>`
Dopo la creazione il file ha un solo nome ("fileName"): un hard link al descrittore del file
## Collegamenti (link)
Il filesystem permette di definire più hard link associati ad un `i-node`: nomi alternativi per lo stesso file.
È anche possibile definire collegamenti simbolici (**soft link**): nomi alternativi per fare riferimento ad uno stesso hard link.

Gli hard link puntano allo stesso `i-node`.
Il descrittore del file `i-node` viene eliminato solo se il numero di hard link che vi fanno riferimento è zero.
I soft link puntano ad uno stesso hard link.
Se elimino o sposto l'hard link, il soft link non è più in grado di accedere al file.
### comando ln
```shell
# creazione hard link
ln target link_name

# creazione link simbolico (soft link)
ln -s target link_name
```
## Strutture dati per l'accesso ai file
Il meccanismo adottato per l'accesso ai file è di tipo sequenziale:
ad ogni file aperto è associato un *I/O pointer* riferimento per la lettura/scrittura sequenziale sul file.
Le operazioni di lettura/scrittura provocano l'*avanzamento del riferimento*.

Le strutture dati per l'accesso ai file sono gestite dal kernel e sono:
- **tabella dei file aperti di processo**: è nella User structure del processo (descrittore del processo), ogni elemento (file descriptor) è un riferimento all'elemento corrispondente nella *tabella di file aperti di sistema*
- **tabella dei file aperti di sistema**: contiene un elemento per ciascun file aperto nel sistema. Se due processi aprono lo stesso file allora ci saranno due entry separate. Ogni elemento contiene un I/O pointer al file e un riferimento all'`i-node` del file (che viene tenuto in memoria principale, nella **tabella dei file attivi**). Formalmente contiene:
		- byte offset
		- flags (O_RDONLY, O_RDWR ecc)
		- puntatore a i-node (nella TFAT)
		- contatore di riferimenti (per sapere quando rimuovere l'elemento)
		- ...
- **I/O pointer e i-node** permettono di trovare l'indirizzo fisico in cui effettuare la prossima lettura/scrittura sequenziale
- **STDIN, STDOUT e STDERR** sono descrittori di default, generati automaticamente al momento dell'esecuzione del programma

Il processo figlio eredita dal padre una copia della User Structure, quindi anche una copia dei file descriptor, in questo caso i due processi hanno descrittori che *puntano allo stesso elemento della Tabella di File di Sistema*, e quindi condividono l'I/O pointer nell'accesso sequenziale al file.
## Primitive per l'accesso ai file
open, read, write, close sono chiamate di sistema non bufferizzate, la libreria standard del [[C]] mette e disposizione funzioni bufferizzate: fopen, fread, fwrite, fclose... , alcune funzioni permettono la lettura/scrittura formattata (fscanf, fprintf, ...).
Quando si legge un file con fread(), una quantità maggiore di dati rispetto a quella richiesta potrebbe essere salvata nel buffer.
Quando si legge un file con read(), al più la quantità di dati chiesta viene letta.
### open
```c
#include <fcntl.h>
int open(const char* path, int flags)
```
- `const char* path`: path del file da "aprire"
- `int flags`: modalità di accesso, ci sono varie macro definite in `fcntl.h>`: se compatibili fra loro, più macro possono essere messe in OR.
  Esempi di macro: O_RDONLY, O_WRONLY, O_RDWR (lista completa in `man 2 open`)
- *ritorna il file descriptor* 
Dopo l'apertura, l'I/O pointer viene posizionato all'inizio del file se non è utilizzata la modalità O_APPEND (in tal caso, I/O parte dalla fine del file)
### close
```c
#include <unistd.h>
int close(int fd)
```
- `int fd` è il file descriptor che si vuole chiudere
- ritorna 0 se la chiusura è riuscita
- ritorna -1 se ci sono stati errori
### read
```c
#include <sys/types.h>
#include <sys/uio.h>
#include <unistd.h>
ssize_t read(int fd, void* buf, size_t count)
```
- `int fd`
- `void*buf`: puntatore al buffer in cui scrivere i dati letti
- `size_t count`: numero massimo di byte da leggere (intero positivo)
- ritorna il numero di byte letti (valore negativo in caso di errore (ssize_t è signed int))
### write
```c
#include <unistd.h>
ssize_t write(int fd, const void* buf, size_t count)
```
- `int fd`
- `const void *buf`: puntatore al buffer da cui leggere i dati da scrivere nel file
- `size_t count`: numero di byte da scrivere (intero positivo)
- ritorna il numero di byte scritti (valore negativo in caso di errore). Potrebbe essere meno di count, ad esempio se è terminato lo spazio disponibile
# Comunicazione a scambio di messaggi: pipe
I processi possono comunicare sfruttando il meccanismo delle pipe: è una comunicazione indiretta, senza naming esplicito e realizza il concetto di **mailbox** nella quale si possono accordare messaggi in modo FIFO. Utilizza un buffer di dimensioni predefinite (1048576 Byte di default). 
La pipe è un canale monodirezionale: ci sono due estremi, uno per la lettura e uno per la scrittura, a ciascun estremo è associato un file descriptor.
```c
#include <unistd.h>
int pipe(int fd[2])
```
- `int fd[2]`: vettore di due interi: conterrà i descrittori della pipe: la funzione pipe salva in `fd[0]` l'estremo della pipe per la lettura e in `fd[1]` l'estremo da usare per la scrittura
- ritorna zero se ha successo, -1 altrimenti
I figli ereditano gli stessi gli stessi file descriptor (una copia) e possono utilizzarli per comunicare con il padre e gli altri figli.
Per la comunicazione di processi che non si trovano nella stessa gerarchia si utilizzano altri strumenti, ad esempio i socket.
## Comportamento di read su pipe
La read su estremità della pipe è bloccante se il buffer è vuoto e c'è almeno uno scrittore attivo.
Restituisce EOF (0) se il buffer è vuoto e tutti gli scrittori hanno chiuso il file descriptor.
## Comportamento di write su pipe
La write su estremità della pipe è bloccante se il buffer è pieno e restituisce errore se non ci sono lettori attivi.
## Nota bene
Chiudere gli estremi non utilizzati.
Chiudere `pipefd[1]` nei lettori.
Chiudere `pipefd[0]` negli scrittori.

Questo evita [[Deadlock]] e comportamenti inattesi.