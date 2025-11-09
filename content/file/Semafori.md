#uni 
# Primitive per i semafori
```c++
natl sem_ini(natl v)
	//crea un nuovo semaforo inizializzato con v gettoni, restituisce l'identificatore del semaforo (0xFFFFFFFF se non è stato possibile crearlo)
	
void sem_wait(natl sem)
	// se c'è un gettone, lo prende, altrimenti blocca il processo
	
void sem_signal(natl sem)
	// inserisce un gettone nel semaforo sem, se vi sono processi bloccati a causa di una wait in attesa di gettoni, ne risveglia uno
```
# Realizzazione dei Semafori
sistema.cpp
```c++
struct des_sem {
	int counter;
	des_proc* pointer;
}

alloca_sem() // alloca un indice appartenente ad una delle due parti dell'array, in base al livello di privilegio del processo che ha chiamato la primitiva (ora salvato nella pila di sistema)
```
- `counter` è il numero di gettoni nel semaforo
- `pointer` punta alla lista di processi bloccati in attesa del semaforo a seguito di una `sem_wait` 
# Estensioni del debugger per i semafori
```shell
sem # mostra lo stato di tutti i semafori allocati
sem waiting # mostra lo stato di tutti i semafori la cui coda non è vuota
	# viene eseguito automaticamente ogni volta che il debugger riacquisisce il controllo
```
Lo stato dei semafori è mostrato in forma $\{ counter \ , \ lista \ processi \}$.
# +readers , 1 writer
La scrittura è bloccante per tutti, la lettura blocca solo la scrittura
```c++
sem wrt = 1;
// sem mutex = 1;
int readers = 0;

proc writer{
	wait(wrt);
	
	<scrittura>
	
	signal(wrt);
}

proc reader {
	// wait(mutex);
	readcount++;                   //   |
	if (readcount==1) wait (wrt);  //   | sezione critica
	// signal(mutex)
	
	<lettura>
	
	// wait(mutex)
	readcount--;                    //  |
	if(readcount==0) signal(wrt);  //   | sezione critica 
	// signal(mutex)
}

/*
quindi aggiungo un altro semaforo mutex, per la variabile condivisa `readcount`
*/
```
posso avere
- al più un lettore bloccato su wrt
- più scrittori bloccati su wrt
- più lettori bloccati su mutex