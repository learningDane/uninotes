#uni 
# Note
- Permettiamo al numero di gettoni di scendere sotto zero (la sem_wait può sempre essere eseguita), in questo modo conta quanti processi sono in attesa di quel semaforo.
# Utilizzo
## Mutua esclusione
## Sincronizzazione
# Primitive incluse nel Nucleo didattico
Qui troviamo alcune delle primitive disponibili nel nucleo didattico.
## Primitive per la gestione di processi
```C++
des_proc* des_p(natl id)
	// restituisce un puntatore al descrittore del processo di identificatore `id`, oppure `nullptr` se tale processo non esiste
	
void schedulatore()
	// sceglie il prossimo processo da mettere in esecuzione (cambia il valore della variabile `esecuzione`)
	
void inserimento_lista(des_proc*& p_lista, des_proc* p_elem)
	// inserisce p_elem nella lista p_lista, mantenendo l'ordinamento basato sul campo precedenza (a parità di precedenza, p_elem viene messo per ultimo)
	
des_proc* rimozione_lista(des_proc*& p_lista)
	//estrae l'elemento in testa alla p_lista e ne restituisce un puntatore (nullptr se la lista è vuota)
	
void inspronti()
	//inserisce il des_proc puntato da esecuzione in testa alla coda pronti
	
void c_abort(p)
	//distrugge il processo puntato da esecuzione e chiama schedulatore()
	
void delay(natl n)
	// sospende il processo per n cicli di timer 0 (50ms)
```
## Primitive per i semafori
```c++
natl sem_ini(natl v)
	//crea un nuovo semaforo inizializzato con v gettoni, restituisce l'identificatore del semaforo (0xFFFFFFFF se non è stato possibile crearlo)
	
void sem_wait(natl sem)
	// se c'è un gettone, lo prende, altrimenti blocca il processo
	
void sem_signal(natl sem)
	// inserisce un gettone nel semaforo sem, se vi sono processi bloccati a causa di una wait in attesa di gettoni, ne risveglia uno
```
# Realizzazione delle Primitive
