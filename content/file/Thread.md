#uni 
Un Thread ("processo leggero") è un flusso di esecuzione indipendente all'interno di un processo. 
Ad un singolo processo possono essere associati più thread.
I thread condividono le risorse e lo spazio di indirizzi (o parte di esso) con gli altri thread dello stesso processo.
La creazione, la distruzione, e il cambio, dei threads sono meno onerose rispetto all'equivalente per i processi.

Vantaggi dell'approccio multithreading:
- interazioni più semplici ed efficienti basate su risorse comuni
- passaggio di conteso fra thread meno oneroso

Svantaggi:
- va gestita la concorrenza fra thread: **thread safety**
	- le risorse vanno accedute in mutua esclusione

# Thread in Linux
[[Linux]] supporta nativamente, a livello di kernel ([[Unix]]), il concetto di thread:s- il thread è l'unità di scheduling e può essere eseguito in parallelo con altri thread
- il processo tradizionale dei sistemi [[Unix]] può essere visto come un thread che non condivide risorse con altri thread
## Libreria pthread
Lo standard [[Posix]] definisce la libreria `phtread` per la programmazione di applicazioni multithreaded portabili.
Questa libreria va incluse `#include<pthread.h>`, inoltre va specificato l'uso della libreria al compilatore: `gcc <opzioni> files -lpthread -std=c99`.
Pagina del manuale: `man pthreads`.
## Identificatori del thread
Un thread ha un ID, di tipo `pthread_t`.
```c
pthread_t pthread_self(void) // funzione per conosce ID del thread
```
`pthread_t` è un tipo "opaco".
Per confrontare due thread è necessaria la seguente funzione:
```c
pthread_equals(tid1, tid2)
```
Un tipo opaco nasconde il modo in cui è effettivamente realizzato (struct). Possiamo quindi utilizzarlo e modificarlo solo attraverso le funzioni di libreria.
## Creazione di un thread
Il [[Linux]] l'esecuzione di un programma determina la creazione di un primo thread che esegue il codice del main.
Il thread iniziale può poi generare una gerarchia di thread:
```c
int pthread_create(pthread_t*thread, const pthread_attr_t* attr, void* (*start_routine)(void*), void*arg);
```
- `pthread_t* thread` è il puntatore ad identificatore di thread, dove verrà scritto l'ID del thread creato
- `const pthread_attr_t* attr`L: attributi del thread, NULL per utilizzare i valori default
- `void*(*start_routine)(void*)`: puntatore alla funzione che contiene il codice del nuovo thread.
- `void*arg`: puntatore che viene passato come argomento a `start_routine`
- il valore di ritorno e *zero* in assenza di errore, altrimenti diverso da zero
## Terminazione e join
### pthread_exit
Un thread può terminare la sua esecuzione con:
```c
void pthread_exit(void* retval);
```
1. l'esecuzione del thread termina e il sistema libera le risorse allocate
2. quanto un thread padre termina prima dei thread figli:
	- se non ha chiamato questa funzione i figli vengono terminati
	- se ha chiamato questa funzione i figli continuano la propria esecuzione
`void*retval` è il valore di ritorno del thread (exit status), consultabile da altri thread che utilizzano la `pthread_join`.
### pthread_join
Un thread può bloccarsi in attesa della terminazione di u nthread specifico:
```c
int pthread_join(pthread_t thread, void** retval)
```
- `pthread_t thread`: ID del thread di cui attendere la terminazione
- `void ** retval`: puntatore dove verrà salvato l'indirizzo restituito dal thread con la `pthread_exit`. Può essere impostato a NULL
- ritorna zero in caso di successo, altrimenti un codice di errore (ad esempio se fa un join su se stesso)
## pthread Mutex
Una variabile mutex permette di proteggere l'accesso a variabili condivise su cui operano più thread.
Nella libreria è definito il tip `pthread_mutex_t` che rappresenta implicitamente lo stato del mutex e la coda dove verranno sospesi i processi in attesa che il mutex sia libero.
È un semaforo binario.

```c
pthread_mutex_t M; // mutex da inizializzare
int pthread_mutex_init(pthread_mutex_t* M, const pthread_mutexattr_t* mattr)
```
- `const pthread_mutexattr_t* mattr` puntatore ad una struttura con attributi di inizializzazione. Con NULL vengono utilizzati i valori di default, quindi mutex libero

La wait sul mutex è realizzata con al primitiva:
```c
int pthread_mutex_lock(pthread_mutex_t* M)
```
La signal è realizzata con la primitiva:
```c
int pthread_mutex_unlock(pthread_mutex_t* M)
```
Ritorna zero se tutto corretto, altrimenti diverso da zero.
## Sincronizzazione dei thread
Il mutex è lo strumento che `pthreads` mette a disposizione per la sincronizzazione *indiretta* dei thread: l'accesso in mutua esclusione.

Per la sincronizzazione *diretta* dei thread la libreria definisce le **variabili condizione**.
### Variabili condizione
Una variabile condizione è di fatto una coda nella quale i thread possono sospendersi volontariamente in attesa di una condizione.
```c
pthread_cond_t C;
int pthread_cond_init(pthread_cond_t* C, pthread_cond_attr_t* attr)
```
- `pthread_cond_t* C`: puntatore alla variabile condizione da inizializzare
- `pthread_cond_attr_t* attr`: attributi specificati per la condizione, inizializzata a default se `attr=NULL`.

Un thread può effettuare due operazioni su una variabile condition:
- wait
- signal/broadcast
### Wait
La wait viene utilizzata al verificarsi di una particolare condizione logica.

> La wait su una condition variable è *sempre* bloccante.

```pseudo
while (condizione) {
	wait(condition_variable);
}
```
Utilizziamo while invece di if perché la signal della pthread è di tipo signal & continue: altri thread potrebbero inserirsi e alterare la condizione, è quindi necessario ricontrollare la condizione dopo essere stati svegliati.

La condizione logica è basata su una risorsa condivisa: la verifica della condizione deve essere eseguita in mutua esclusione: la primitiva di wait offerta da `pthreads` permette di associare una variabile mutex ad una variabile condition.

> Dimenticarsi il secondo argomento della wait è un errore molto grave, perché dimostra di non aver capito l'accesso a risorse condivise.
#### Primitiva wait
```c
int pthread_cond_wait(pthread_cond_t* C, pthread_mutex_t* M)
```
Questa chiamata ha due effetti:
- il thread viene sospeso nella coda associata a `C`
- il mutex `M` viene liberato: quando il thread verrà risvegliato proverà nuovamente a fare lock su `M` 
### Signal
Il risveglio di un thread sospeso su una variabile condition `C` avviene mediante la primitiva signal:
```c
int pthread_cond_signal(pthread_cond_t* C)
```
Come conseguenza della signal:
- se esistono thread in coda sulla condition, un thread bloccato *scelto a caso* viene risvegliato
- se non vi sono thread sospesi, non ha alcun effetto

La politica della signal della libreria `pthreads` abbiamo detto è ti dopo *signal & continue*:
- il thread che esegue la signal continua la sua esecuzione e mantiene il controllo del mutex fino al suo esplicito rilascio
- il thread che aveva effettuato la wait ed è stato risvegliato deve verificare nuovamente la condizione (il while!!!)
### Broadcast
Per risvegliare tutti i thread in coda su una condition è possibile usare la funzione:
```c
int pthread_cond_broadcast(pthread_cond_t* C)
```
è utile quando è necessario svegliare un thread specifico.

Per maggiore stabilità la signal/broadcast va invocata DENTRO la sezione critica, ovvero prima della unlock:
- in questo modo siamo sicuro che nel momento in cui la signal/broadcast viene invocata la condizione è rispettata
- il corretto funzionamento è garantito dal while nella chiamata della wait
# Esempio di sincronizzazione esplicita: produttori e consumatori
Dobbiamo realizzare la risorsa condivisa (globale, quindi definita fuori da funzioni):
```c
typedef struct {
	buffer
	indici di read/write nel buffer
	elementi nel buffer
	
	pthread_mutex_t M;
	
	pthread_cond_t FULL; // condition variable buffer pieno
	pthread_cond_t EMPTY; // condition variable buffer vuoto
} risorsa;
```
la risorsa deve essere inizializzata:
```c
risorsa r;
int main() {
	pthread_mutex_init(&r.M, NULL);
	
	pthread_cond_init(&r.FULL, NULL);
	pthread_cond_init(&r.EMPTY, NULL);
	
	//inizializzazione altre risorse (indici buffer etc)
}
```

Il consumatore deve:
- assicurarsi che il buffer non sia vuoto prima di prelevare un dato
- risvegliare il produttore dopo aver prelevato

Il produttore deve:
- assicurarsi che il buffer non sia pieno prima di inserire un dato
- risvegliare un consumatore eventualmente sospeso