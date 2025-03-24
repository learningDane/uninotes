#uni
Il modello dei dati è l'insieme di costrutti utilizzati per organizzare i dati di interesse e descriverne la dinamica.

La componente fondamentale di ogni modello dei dati sono i suoi meccanismi di strutturazione, anche detti ___costruttori di tipo___.

Questo modello dei dati fornisce ai programmi applicativi una ___vista astratta dei dati___, così facendo possiamo modificare la struttura dei dati senza dover cambiare i programmi.
# Principali tipi di Modelli

- ==Modelli Concettuali==:
	- permettono di rappresentare i dati in modo indipendente da ogni sistema
		- cercano di descrivere i concetti del mondo reale
		- sono utilizzati nelle fasi preliminari di progettazione
	- il più diffuso è il modello [[Modello Entity-Relationship]] (ER).

 - ==Modelli logici==:
	- adottati nei DBMS esistenti per l'organizzazione dei dati
		- utilizzati dai programmi
		- indipendenti dalle strutture fisiche
	- tre modelli logici __tradizionali__: 
		- [[Modello Logico Relazionale]] (basato su valori, rappresenta anche le relazioni)
		- ___Reticolare___ e ___Gerarchico___ (utilizzano riferimenti espliciti fra record, ovvero puntatori). 
	- modelli più recenti: a oggetti, basato su [[XML]] e [[NoSQL]], quest'ultimo in particolare sta riscuotendo molto successo ultimamente perché risolve il problema della scalabilità, ma non lo tratteremo.
