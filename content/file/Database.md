#uni 
Una Base di Dati è il cuore di un sistema informativo automatizzato, cioè un insieme organizzato di dati utilizzati per rappresentare le informazioni di interesse.
Un Database è l'insieme di dati gestito da un [[DBMS]].

I Database hanno:
- dimensioni enormi, molto maggiori della memoria centrale del sistema di calcolo utilizzato.
- tempo di vita indipendente dalle singole esecuzioni dei programmi che lo utilizzano (__persistenza__ dei dati): i dati rimangono salvati in modo permanente finché non vengono modificati o cancellati.
- diverse tipologie di informazioni e diversi utenti: ogni utente ha diverse autorizzazioni (es. uno studente può vedere i voti ma non modificarli).

Una base di dati è una risorsa integrata, condivisa fra applicazioni e quindi necessita di meccanismi di autorizzazione e controllo della concorrenza e dell'incoerenza.

Il linguaggio usato per interagire con i database è l'[[MySQL]].
# Problemi della condivisione
I possibili problemi possono essere:
- ripetizione di informazioni
- rischio di incoerenza
- cattiva gestione dello spazio di archiviazione
# Privacy di un Database
Un database è una risorsa integrata, condivisa fra applicazioni. Servono meccanismi di autorizzazione e [[Gestione della Concorrenza]].
Si possono definire meccanismi di autorizzazione, ovvero privilegi diversi per utenti diversi. 
# Affidabilità di un Database
Un Database deve essere resistente a malfunzionamenti hardware e software. Un Database è una risorsa pregiata e quindi deve essere conservata a lungo termine.

Serve una gestione delle transazioni: una transazione è un insieme di operazioni da considerare indivisibile (___atomico___), corretto anche in presenza di concorrenza e con effetti definitivi. 
Le transazioni sono atomiche e devono funzionare correttamente anche in presenza di concorrenza.

I risultati di una transazione conclusa positivamente devono essere permanenti e corrisponde ad un impegno (___commit___) a mantenere traccia del risultato in modo definitivo, anche in presenza di guasti e/o di esecuzione concorrente.
# Efficienza di un Database
I database devono cercare di utilizzare al meglio le risorse di spazio di memoria, principale e secondaria, e tempo, di esecuzione e di risposta.
Minore efficienza di un Database  porta ad affrontare spese più grandi per maggiore spazio di archiviazione o a esperienze di utilizzo peggiori. 
Qui è quindi di grande importanza l'[[Ottimizzazione delle Interrogazioni]]. 