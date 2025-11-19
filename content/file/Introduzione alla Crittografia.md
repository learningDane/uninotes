#uni 
Crittografia = "scrittura nascosta".
___Crittografia___: metodi di cifratura, per rendere incomprensibile per chiunque non sia il destinatario.
___Crittoanalisi___: metodi di interpretazione.
___Crittologia___: studio della comunicazione su canali sicuri e relativi problemi (crittografia+crittoanalisi).

>Alice spedisce un messaggio in chiaro $m$, sotto forma di testo cifrato $c$, che deve essere incomprensibile al crittoanalista EVE ("eavesdropping) in ascolto sul canale e facilmente decifrabile da Bob (complessità polinomiale).

MSG: insieme dei messaggi (testi in chiaro)
CRITTO: insieme dei crittogrammi (testi cifrati)

Cifratura del messaggio: operazione con cui si trasforma MSG in CRITTO (dominio MSG, codominio CRITTO).
Decifrazione del messaggio: operazione con cui si trasforma CRITTO in MSG.
La funzione $C$ di cifratura deve essere iniettiva, altrimenti non sarebbe invertibile: critti diversi portano a messaggi diversi.

>La sicurezza dipende dalla conoscenza del metodo: ==Cifrario ad uso ristretto==.

La classificazione dei metodi crittografici va in base al livello di segretezza:
- Cifrari per uso ristretto: le funzioni di cifratura $C$ e di decifrazione $D$ vengono tenute segrete.
- Cifrari per uso generale: fondati sull'uso di una chiave segreta.

==Cifrari ad uso generale==: le regole sono pubbliche, solo la chiave $k$ rimane segreta. La chiave è un pezzo di informazione aggiuntivo conosciuta solo da Alice e Bob, senza del quale è impossibile decifrare il messaggio.
	$c=C(m,k)$ , $m=D(c,k)$.
C'è una chiave per ogni coppia di utenti.
I cifrari che usano la stessa chiave per cifrare e decifrare si dicono ___simmetrici___.
Vantaggi:
- tenere segreta la chiave è più facile che tenere segreto l'intero processo.
- tutti possono impiegare le funzioni pubbliche C e D, basta creare una chiave.
- se la chiave viene scoperta basta cambiare la chiave.

Se la segretezza dipende unicamente dalla chiave allora il numero delle chiavi deve essere così grande da essere praticamente immuni da ogni tentativo di brute-force. Inoltre la chiave segreta deve essere scelta in modo casuale.
Anche se soddisfo queste condizioni non è detto che sia sicuro, per esempio la cifratura monoalfabetica (riordino casualmente le lettere dell'alfabeto) non è sicura, è facilmente attaccabile con una analisi statistica della frequenza dei caratteri.
Le due regole di cui sopra sono condizioni necessarie, non sufficienti.

Il crittoanalista può avere:
- Comportamento passivo: si limita as ascoltare la comunicazione
- comportamento attiva: disturba attivamente la comunicazione, modifica il crittogramma ecc..
Attacchi:
- Cipher text attack: solo testo noto, rileva sul canale una serie di crittogrammi
- Known Plain-Text Attack: testo in chiaro noto, conosce una serie di coppie $(m_{i},c_{i})$.
- Chosen Plain-Text Attack: testo in chiaro scelto, il crittoanalista si procura una serie di coppie relative a messaggi in chiaro da lui scelti (oracolo per cifratura).
- Chosen Cipher-Text Attack: testo cifrato scelto, il crittoanalista si procura una serie di coppie relative a crittogrammi da lui scelti (oracolo per decifrazione).
- Bruteforce Attack
- Man in-the-Middle (Attivo): il crittoanalista si installa sul canale di comunicazione e si finge Bob agli occhi di Alice e Alice agli occhi di Bob.
# Livelli di Sicurezza
Un cifrario inattaccabile (perfetto) offre una sicurezza incondizionata, nasconde l'informazione con certezza assoluta, non può essere decifrato senza conoscere la chiave, niente Bruteforce.
Attacco possibile solo se la chiave non è scelta bene.
Un crittogramma decifrato senza chiave appare come una stringa casuale e quindi non offre nessuna informazione sul vero messaggio o sulla vera chiave.
Questi cifrari esistono ma sono estremamente complessi e vengono utilizzati solo in contesti militari.
Nessuna informazione sul testo in chiaro può filtrare dal crittogramma.
Si deve a [[Claude Shannon]] nel 1945, pubblicato nel 1949 per motivi di segretezza militare.

Esempio:
	One-Time Pad, utilizzato per le comunicazioni tra casa bianca e Cremlino nella Hot Line a partire dal 1967.
	Assolutamente sicuro ma:
	- richiede una nuova chiave segreta per ogni messaggio
	- perfettamente casuale
	- e lunga come il messaggio da scambiare
	Come si genera e scambia la chiave?

I cifrari diffusi non sono perfetti ma sono dichiarati sicuri perché sono rimasti inviolati dagli attacchi degli esperti e per violarli è necessario risolvere problemi matematici considerati estremamente difficili: ==sicurezza computazionale==.
# AES
Cifrari di oggi:
___Advanced Encryption Standard (AES)___:
- standard per comunicazione riservate non classificate
- pubblicamente noto e realizzabile in hardware su computer di ogni tipo
- chiavi brevi: 128 o 256 bit
- simmetrico
- ogni carattere del crittogramma dipende da tutti i caratteri del testo in chiaro e della chiave (se cambio un solo bit del messaggio, il crittogramma cambia completamente).

Scambio della chiave:
Nel 1976 viene pubblicato "New directions in criptography" dove si presenta un protocollo per scambiarsi le chiavi segrete su un canale insicuro.
Protocollo DH (Diffie-Hellman + Merkle) (Turing Award 2015 per Diffie e Hellman).

Crittografia a chiave pubblica: protocollo asimmetrico dove la chiave per cifrare è pubblica, quella per decifrare no.
- $K_{B}[pub]$ per cifrare: pubblica
- $K_{B}[priv]$ per decifrare: nota solo a Bob
Ogni utente ha una coppia di chiavi.

Affinché la cifratura a chiave pubblica sia buona la funzione di cifratura deve essere una funzione ==one-way trap-door==:
- cifra è computazionalmente facile
- decifrare senza chiave è computazionalmente difficile

La crittografia a chiave pubblica è uno schema di comunicazione molti a uno.
Nono è richiesto uno scambio segreto delle chiavi: il ricevente pubblica la sua chiave di cifratura, ma non quella di decifratura.

Svantaggi:
- questi sistemi sono molto più lenti di quelli simmetrici
- esposti ad attacchi di tipo chosen plain-text
# Cifrario RSA
Nel 1977 Rivest, Shamir e Adleman propongono un sistema a chiave pubblica con funzione one-way trap-door. Turing Award 2002.
# Cifratura Ibrida
Si usa un cifrario a chiave segreta (per esempio AES) per le comunicazioni di massa.
Si usa anche un cifrario a chiave pubblica per scambiare le chiavi segrete relative al primo, senza incontri fisici tra gli utenti.
La trasmissione dei messaggi lunghi avviene quindi ad alta velocità, mentre è lento lo scambio delle chiavi segrete.
In questo modo non siamo nemmeno suscettibili ad attacchi chosen plain-text, perché EVE non ha la chiave di cifratura.
