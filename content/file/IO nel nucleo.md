#uni 
Per imporre la mutua esclusione e la sincronizzazione procediamo come segue:
- impediamo agli utenti di parlare direttamente alle periferiche (settiamo IOPL=SISTEMA nei FLAGS dei processi utente, questo impedisce anche le istruzioni `sti` e `cli`)
- forniamo delle **primitive** per svolgere le operazioni di I/O sotto il controllo del sistema

Le primitive avranno una generica forma come segue:
```c++
/// Lettura
extern "C" void read_n(natl id, char* buf, natq quanti);


/// Scrittura
extern "C" void write_n(natl id, const char* buf, natq quanti);
```
# Realizzazione con primitiva e Driver
Assumiamo che le periferiche siano in grado di trasferire un byte alla volta, generando una richiesta di interruzione per ognuno.

L'interfaccia di ogni periferica avrà un registro di controllo **CTL** e un registro buffer **RBR**.
La lettura da **RBR** funziona da risposta alla richiesta di interruzione, fino a che l'interfaccia non riceve risposta non genera altre richieste di interruzione.

> La primitiva ha lo scopo di avviare l'operazione di IO e bloccare il processo.
> Il driver ha il compito di trasferire effettivamente i byte e sbloccare il processo al termine dell'operazione.

Per gestire la mutua esclusione e la sincronizzazione dobbiamo fare uso dei semafori, ==la primitiva quindi non può essere atomica e dunque non deve salvare e caricare lo stato del processo all'entrata ed all'uscita del sistema==.
Immaginiamo quindi che sia il processo stesso ad eseguire la primitiva.

```asm
.global read_n
read_n:
	int $IO_TIPO_RN
	ret
```

```asm
# NON salviamo e carichiamo lo stato !
# ricordati la IRETQ !
.extern c_read_n
a_read_n:
	call c_read_n
	iretq
```

```c++
struct des_io {
	ioaddr iRBR, iCTL;
	char* buf;
	natq quanti;
	natl mutex; // init a 1, per mutua esclusione dei processi sulla periferica
	natl sync; // init a 0, per la sincronizzazione tra il processo che richiede l'operazione e la conclusione dell'operazione stessa
}

extern "C" void c_read_n(natl id, natb *buf, natl quanti)
{
	/// Controllo Cavallo di Troia
	if (!c_access(begin, quanti, true, true)) {
		abort_p(); // NON c_abort_p: ci troviamo in una primitiva NON ATOMICA, dobbiamo dunque, salvare lo stato, chiamare c_abort_p ed infine caricare lo stato.
	}
	
	des_io *d = &array_des_io[id];
	
	sem_wait(d->mutex);
	d->buf = buf;
	d->quanti = quanti;
	outputb(1, d->iCTL); // abilito interruzioni
	sem_wait(d->sync);
	sem_signal(d->mutex);
}
```

Passiamo ora al driver.
Dobbiamo ovviamente conoscere il tipo dell'interruzione generata e caricarne il gate nell'IDT, in modo che punti a a_driver.
```asm
.extern c_driver
a_driver_i:
	call salva_stato
	movq $i, %rdi # ogni interfaccia genera una interrupt diversa, in questo modo la comunichiamo alla funzione c++
	call c_driver
	call apic_send_EOI
	call carica_stato
	iretq
```

La parte C++ del driver la facciamo generica (usiamo i per differenziare).
Il driver usa le risorse del processo che ha interrotto, in particolare usa la sua pila sistema e la sua memoria virtuale (poiché non stiamo cambiando il valore di cr3).
```c++
/*! @brief Driver che viene eseguito a seguito di una richiesta di interruzione da parte di una interfaccia.
 * 
 * Questo driver è generico, per questo necessitiamo di passargli l'id del dispositivo che ha mandato la richiesta (vedi a_driver).
 */
extern "C" void c_driver(natl id)
{
	des_io *d = &array_des_io[id];
	
	d->quanti--;
	if (d->quanti == 0) {
		outputb(0, iCTL); // disabilito interruzioni del dispositivo, va fatto prima della lettura del byte, perché questa dal dispositivo viene interpretata come una risposta alla richiesta di interruzione e potrebbe mandare un'altra INTR mentre stiamo gestendo quella attuale.
		/// parte intermedia di sem_signal, non possiamo chiamare sem_signal() perché fa salva_stato e carica_stato, ma il driver non ha un descrittore di processo. Di Conseguenza IL DRIVER DEVE ESSERE ATOMICO, per questo motivo non possiamo nemmeno usare c_sem_signal, poiché dobbiamo saltare i test che quella funzione include, in particolare fallirebbe il test di validità del semaforo, poiché questo è stato inizializzato dal livello sistema, mentre formalmente il livello attuale è utente, poichè non è stata invocata tramite una INT.
		/// {
		des_sem *s = &array_dess[d->sync];
		s->counter++;
		if (s->counter <= 0) {
			des_proc* lavoro = rimozione_lista(s->pointer); // estraggo un processo bloccato
			inspronti();
			inserimento_lista(pronti, lavoro);
			esecuzione(); // se il processo sbloccato ha prio maggiore, andrà in esecuzione, nota che non sto bloccando il driver!
		}
		/// }
	}
	char c = inputb(d->iRBR); // leggo il byte
	*d->buf = c; // Nota che è ancora attiva la VM di un processo a caso che questo driver ha interrotto, quindi il buffer deve essere dichiarato in utente/condivisa! Ovvero basta che non sia stata dichiarata nello stack del processo che ha iniziato il trasferimento, che è in utente/privata. Il buffer quindi deve essere allocato nello heap, o dichiarato globale, NON variabile locale.
	d->buf++; // aumento il puntatore
}
```
Va anche caricato il gate per il driver, in particolare questo gate deve avere:
- DPL = SISTEMA, poiché non deve essere chiamabile dall'utente tramite INT.
- L = SISTEMA
- I/T = INTERRUPT, poiché ==il driver deve essere atomico poiché manipola le code dei processi==.