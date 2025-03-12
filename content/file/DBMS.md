#uni 
Il __Sistema di Gestione di Basi di Dati__ (o [[Database]] management system, __DBMS__) gestisce collezioni di dati:
- __grandi__ $\to$ gestione sofisticata
- __persistenti__ $\to$ in memoria secondaria (lenta) $\to$ limitare accesso a memoria lenta
  tempo di vita indipendente dalle singole esecuzioni dei programmi che le utilizzano
- __condivise__ $\to$ meccanismi di autorizzazione e [[Gestione della Concorrenza]]  
e garantisce:
- __privacy__
- __affidabilità__:
  i [[Database]] sono una risorsa pregiata e vanno protetti, la tecnica fondamentale inerente è la [[Gestione delle Transazioni]]. 
- __efficienza__:
  utilizzare al meglio le risorse di spazio e di tempo
- __efficacia__:
  migliorare la produttività dell'utilizzatore

Nei DBMS esiste una porzione della base di dati che contiene una descrizione centralizzata dei dati. Viene introdotto il concetto di [[Modello dei dati]].
Un DBMS può essere ___monoutente___ o ___multiutente___ a seconda del numero di utenti che possono usufruirne simultaneamente.
# Schema ed Istanza
In ogni base di dati esistono:
- ___schema___: sostanzialmente invariante nel tempo, descrive la struttura della tabella (ovvero del Database).
- ___istanza___: i valori attuali, che possono cambiare anche molto rapidamente, inoltre ci possono essere più istanze diverse.
# Architettura di un DBMS
![[architetturadbms1.svg]]
1. __Schema Esterno__:
	- descrizione di parte della base di dati in un modello logico.
2. __Schema logico__:
	- descrizione della base di dati nel modello logico, ad esempio la struttura della tabella
3. __Schema interno__ (o __fisico__):
	-  rappresentazione dello schema logico per mezzo di strutture memorizzazione, ad esempio record con puntatori, ordinati in un certo modo

# Linguaggi per Basi di Dati
i linguaggi usati sono linguaggi testuali interattivi ([[SQL]]) ovvero comandi in linguaggi testuali immersi in un linguaggio ospite ([[C++]], [[Java]], ecc) con interfacce amichevoli.

Distinzione terminologica:
	- ___data definition language___ (DDL) per la definizione di schemi (logici o fisici)
	- ___data manipulation language___ (DML) per l'interrogazione e l'aggiornamento di (istanze di) basi di dati. 
# Operazioni di aggiornamento
- Operazioni di Inserimento
	- violazione dei vincoli intra-relazionali
	- violazione dell'integrità referenziale
- operazione di cancellazione
	- violazione dell'integrità referenziale
- operazione di modifica
	- modifica = cancellazione + inserimento
# Indipendenza dei Dati
L'accesso ai dati avviene solo tramite il livello esterno (che può coincidere con il livello logico).

__Indipendenza fisica__: il livello logico e quello esterno non dipendono dal livello fisico: il database è utilizzato in maniera indipendente dalla sua implementazione fisica.

__Indipendenza logica__: il livello esterno è indipendente dal livello logico, quindi modifiche alle viste non richiedono modifiche al livello logico e le modifiche al livello logico non impattano su quello esterno.
# Personaggi
Abbiamo diversi personaggi che interagiscono con il [[DBMS]]:
- progettisti e realizzatori di DBMS
- progettisti della base di dati e amministratori della base di dati
- progettisti e programmatori di applicazioni
- utenti:
	- utenti finali: eseguono applicazioni predefinite, ovvero Transazioni.
	- utenti casuali: eseguono operazioni non previste a priori
# Vantaggi e Svantaggi dei DBMS
==Vantaggi==:
	1. dati come risorsa comune e database come modello della realtà
	2. gestione centralizzata con possibilità di standardizzazione ed ___economia di scala___
	3. disponibilità di servizi integrati
	4. riduzione di ridondanze e inconsistenze
	5. indipendenza dei dati
		1. favorisce lo sviluppo e la manutenzione delle applicazioni

==Svantaggi==:
	1. costo dei prodotti e della transizione verso di essi
	2. non scorporabilità delle funzionalità (con riduzione di efficienza)

