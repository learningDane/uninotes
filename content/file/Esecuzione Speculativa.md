#uni 
L'esecuzione speculativa è una tecnica che permette di evitare lo stallo dello stadio di emissione quando incontra una istruzione che dipende per il controllo da istruzioni ancora in esecuzione, velocizzando il flusso di istruzioni.

L'idea è quella di cercare di indovinare il prossimo indirizzo (tramite l'uso del BTB/BTP), e nel caso in cui la pipeline calcoli un indirizzo diverso da quello speculato, annullare gli effetti delle istruzioni che non dovevano essere eseguite, proprio come abbiamo visto nella soluzione di alee sul controllo nella pipeline sequenziale. 

A differenza della soluzione già vista però ora abbiamo introdotto l'*esecuzione fuori ordine*, questo vuol dire che non abbiamo più la certezza che quando una istruzione di salto viene completata, e l'indirizzo è sbagliato, le istruzioni che non dovevano essere eseguite non sono arrivate in tempo allo stadio S e quindi nessun cambiamento è stato fatto.

Vediamo allora come possiamo annullare l'effetto di istruzioni erroneamente eseguite.
# Stadio di Ritiro
Introduciamo lo **stadio di ritiro**, dopo lo stadio di esecuzione. Gli effetti delle istruzioni vengono resi permanenti solamente in questo stadio, fino ad allora possono sempre essere annullati.

> Nello stadio di esecuzione le istruzioni possono essere eseguite in qualsiasi ordine, nello stadio di ritiro invece queste vengono ritirate nell'ordine in cui sono state emesse, ovvero l'ordine originale del programma.

Così facendo quando viene ritirata una istruzione di salto, con predizione errata, basta annullare tutte le istruzioni successive e comunica allo stadio P l'indirizzo corretto.

Lo stadio di ritiro usa un **Reorder Buffer** (**ROB**), organizzato come una coda FIFO, lo stadio di esecuzione quando emette una istruzione (quindi la inserisce in una stazione di prenotazione) la inserisce anche in coda al ROB.

Ogni entrata del ROB ha un flag che dice se l'istruzione è stata completata o meno, quando una istruzione viene completata, aggiorna il suo flag nel ROB.

Lo stadio di ritiro monitora la testa del ROB e quando vede che l'istruzione in testa è stata completata la ritira:
- se l'istruzione è operativa rende permanente il suo effetto
- se è una istruzione di salto:
	- se è un salto predetto correttamente non fa altro
	- se è un salto predetto erroneamente svuota il ROB e comunica allo stadio P l'indirizzo corretto.
## Annullamento delle istruzioni
### Istruzioni operative
Prevediamo per ogni registro logico `x` ricordiamo due registri fisici:
- un registro speculativo `S(x)`: contiene il risultato dell'ultima istruzione emessa non ancora ritirata sul registro `x`
- un registro NON speculativo `N(x)`: contiene il risultato dell'ultima istruzione ritirata sul registro `x`

Lo stadio di rinomina, quando riceve una istruzione:
- sostituisce i registri source con i loro registri speculativi
- sceglie un nuovo registro fisico non utilizzato e lo fa diventare il nuovo registro speculativo del registro destinazione

Nel ROB insieme all'istruzione viene anche salvato quale sia il suo registro (logico) destinazione.

Lo stadio di ritiro:
- se l'istruzione viene ritirata: il registro speculativo del registro destinazione diventa il suo registro non speculativo
- se l'istruzione viene annullata: aggiorna la tabella dello stadio di rinomina in modo che il registro speculativo del registro destinazione contenga il valore del suo registro non speculativo
### Istruzioni di accesso alla memoria
Imponiamo che le istruzioni di scrittura non vengano effettivamente eseguite (e quindi rimangano nello store buffer) fino a quando non vengano ritirate.

Lo stadio di ritiro in caso di salto predetto male, oltre al ROB, svuota anche lo store buffer.

Le istruzioni di lettura in memoria non danno problemi, anzi un vantaggio dell'esecuzione speculativa è anticipare le istruzioni di lettura e quindi caricare in cache le cacheline mancanti.
### Gestione delle eccezioni
Quando una istruzione genera una eccezione, questa non viene sollevata immediatamente, in quanto la CPU deve sapere se questa istruzione doveva essere eseguita davvero oppure no.

Allora quando lo stadio di esecuzione rileva una eccezione nell'esecuzione di una istruzione, lo segna in un campo della corrispondente entrata nel ROB, sarà lo stadio di ritiro a sollevare l'eccezione ed annullare tutte le istruzioni successive, solamente se l'istruzione verrà ritirata.

È probabile che in caso di fault, lo stadio di ritiro stesso immetta nello stadio di esecuzione una sequenza di istruzioni che svolgono le operazioni necessarie alla messa in esecuzione della routine di gestione:
- accesso alla IDT
- cambio di Pila
- salvataggio 5 qword
- etc
- salto all'indirizzo della routine di gestione dell'eccezione
# Pipeline con esecuzione speculativa
![[pipelineEsecuzioneSpeculativa.svg]]