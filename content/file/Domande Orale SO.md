#uni 
# 2026-02-16
## Studente 1
Come funziona la traduzione degli indirizzi con segmentazione?
	Disegno della traduzione con n_segmenti > 3.
Quante tabelle dei segmenti ci sono? Dove stanno? Come viene stabilito il contenuto di STLR e STBR?
	Una tabella dei segmenti per ogni processo.
	Le tabelle stanno in memoria Centrale.
	La tabella è nel descrittore di processo.
Il meccanismo di traduzione dove avviene?
	Nella MMU. (Avvenuti è rimasto su questa question per 20 minuti minimo)
## Studente 2
Descriva il problema dei produttori e consumatori.
	Lo studente prova a spiegare il comportamento degli agenti, il professore vuole che esponga fino in fondo il problema di sincronizzazione.
Questo problema fa riferimento a quale modello di ambiente, locale o globale?
	Modello ad ambiente globale.
Estendendo la capacità del buffer, cosa ottengo?
	Parallelismo. Produzione e consumo (potenzialmente) non bloccante. DISACCOPPIAMENTO TEMPORALE.
Come cambiano le regole di sincronizzazione?
	Il produttore non può inserire se il buffer è pieno, il consumatore non può prelevare se il buffer è vuoto.
Ora elenchiamo le regole di sincronizzazione se abbiamo più produttori e più consumatori.
	Solo uno scrittore alla volta. Più lettori alla volta.
LE SEZIONI CRITICHE DEVONO ESSERE ATOMICHE, i semafori per esempio solo uno strumento per renderle atomiche.
## Studente 3
Come viene gestito un page fault?