#uni 
Il primo standard ("di fatto") per quanto riguarda l'espansione del bus era quello del PC AT, chiamato **ISA**, per *Industry Standard Architecture*.

Aveva però problemi e limitazioni e per risolverli furono proposto tanti standard ma l'unico che ebbe successo fu lo standard **PCI**, per *Periferal Component Interconnect*, della [[Intel]], proposto nel 1992.

Questo standard stabilisce i collegamenti del bus e il protocollo che le periferiche devono adottare su di esso.

Definisce 3 spazi di indirizzamento:
- **spazio di memoria**
- **spazio di I/O**
- **spazio di configurazione**

Quest'ultimo fu introdotto per risolvere il problema della non sovrapponibilità degli indirizzi a cui rispondo le varie interfacce di I/O: le periferiche che rispettano questo standard non possono autonomamente decidere a quali indirizzi rispondere, ma devono contendere dei comparatori programmabili, in modo che questi indirizzi siano scelti dal software, all'avvio del sistema, appunto tramite questo spazio di configurazione.

All'avvio il sistema consulta i registri disponibili nello spazio di configurazione, scoprendo per ogni dispositivo varie informazione, come il tipo, il numero di indirizzi necessari eccetera.

Una peculiarità di questo standard è che non è legato al processore: prevede infatti un dispositivo, detto **ponte ospite-PCI** (o anche detto **North Bridge**), che fa da tramite tra il **bus locale** (quello dove risiede il processore) e il **bus PCI**.

Inoltre questo standard prevede un **albero** di bus, la cui radice è il bus PCI a cui è collegato il ponte ospite-bus; gli altri bus sono collegati all'albero tramite **ponti PCI-PCI**, fino ad un massimo di 256 bus.

Ad ogni bus si possono collegare *32 dispositivi*, e ciascun dispositivo può contenere fino ad *8 **funzioni***, alcune funzioni possono fare da ponte verso altri tipi di bus (ponte PCI-ISA, PCI-ATA, PCI-USB ecc).

Nella nostra macchina il ponte opsite-PCI risponde a tutte le operazioni nello spazio di I/O ed alcune nello spazio di memoria. Il ponte ha alcuni registri nello spazio di I/O del processore e risponde direttamente alle operazioni che li indirizzano, per il resto traduce tutte le operazioni sul bus locale nelle analoghe sul bus PCI, dialogando con l'obiettivo per conto della CPU o del controllore cache.

Una volta configurati i dispositivi, dal punto di vista della CPU è come se questi dispositivi siano direttamente sul bus locale, la traduzione è del tutto trasparente.
# Operazioni di lettura e scrittura
Ciascuna operazione (lettura o scrittura in uno dei tre spazi) è detta **transazione**, è iniziata da un dispositivo detto **iniziatore** che cerca di operare su un altro dispositivo detto **obiettivo**, ogni dispositivo può essere sia iniziatore che obiettivo (in transazioni diverse ovviamente), questo permette tra le altre cose il DMA.

Una transazione si svolge in più fasi:
1. una **fase di indirizzamento**: qui l'iniziatore specifica il tipo di operazione e l'indirizzo del primo byte da leggere/scrivere. Tutti i dispositivi nello spazio specificato confrontano l'indirizzo specificato con i propri comparatori, solo uno troverà una corrispondenza, sarà l'obiettivo della transazione
2. una o più **fasi di scambio dati** 
## Collegamenti del bus
Questi sono i principali collegamenti del bus (i segnali che terminano con `#` sono attivi bassi):
- **`FRAME#`**: out per iniziatore, delimita l'inizio e la fine della transazione
- **`DEVSEL#`**: in per iniziatore, attivato dall'obiettivo che riconosce l'indirizzo specificato
- **`C/BE#[3:0]`**: out per iniziatore: codificano il tipo di operazione nella fase di indirizzamento e poi fungono da byte enable nella fase di trasferimento dati
- **`AD[31:0]`**: in/out per tutti, codificano l'indirizzo nella prima fase e i dati nella seconda
- **`TRDY#`**: in per iniziatore, per handshake
- **`IRDY#`**: out per iniziatore, per handshake
- **`STOP#`**: in per iniziatore, serve all'obiettivo per terminare prematuramente una transazione
- **`CLK`**: in per tutti, tutti i dispositivi campionano i loro ingressi sul fronte di salita di questo segnale
## Protocollo
1. L'iniziatore pilota `C` e `AD` con il tipo di operazione e l'indirizzo iniziale
2. l'iniziatore attiva `FRAME#` 
3. se un dispositivo riconosce il tipo di operazione e l'indirizzo attiva `DEVSEL#`, se nessun dispositivo attiva `DEVSEL#` entro un certo numero di clock l'iniziatore termina l'operazione con un errore
4. comincia lo scambio dei dati:
	Se è una lettura:
	1. l'obiettivo pilota `AD` e segnala la validità dei dati attivando `TRDY#` 
	2. attende che l'iniziatore riceva i dati e quindi attivi `IRDY#` 
	3. disattiva `TRDY#` 
	Se è una scrittura vale l'opposto.
	*Ogni fase dati trasferisce al più 4 byte allineati naturalmente* 
5. quando sia `TRDY#` e `IRDY#` sono attivi sullo stesso fronte di salita del clock finisce una fase di scambio dati
6. se `FRAME#` è attivo quando `IRDY#` è attivo l'iniziatore sta chiedendo una nuova fase di scambio dati (evitando di dover rieseguire la fase di indirizzamento)
7. l'obiettivo può terminare prematuramente una transazione attivando `STOP#` (per esempio dispositivi senza la possibilità di incrementare l'indirizzo specificato devono terminare ogni transazione dopo ogni fase di dati)

> esempio di lettura e di scrittura sul bus pci: ![[esempioTransazioniBusPci.svg|1000]]
# Spazio di configurazione
Lo standard PCI prevede uno spazio di configurazione di 64 parole ($64*4 \text{ byte}$)per ogni funzione, ogni dispositivo deve avere almeno una funzione. 
In questo spazio ciascuna funzione rende accessibili i propri registri di configurazione. Non tutti i registri menzionati devono essere sempre presenti, quelli obbligatori (a parte per il bus opsite-PCI) sono quelli a sfondo grigio:

> Spazio di configurazione di ogni funzione PCI: ![[spazioDiConfigurazioneFunzionePCI.svg |400]]

- **Vendor ID**: (lettura) codice che identifica il produttore della funzione, assegnato ad ogni produttore dal PCI SIG (PCI special Interest Group)
- **Device ID**: (lettura) codice che identifica la funzione, assegnato dal produttore
- **Command**: (lettura/scrittura) permette di abilitare o disabilitare varie capacità della funzione. Il *bit 0 abilita la funzione a rispondere alle transazioni nello spazio di I/O*, il *bit 1 a quelle in memoria*, sono di default 0. Il *bit 2 abilita la funzione a comportarsi da bus master*, se capace. ==Se una funzione non ha registri nello spazio di memoria o di I/O o non ha la capacità di comportarsi da Bus Master, il corrispondete bit vale 0 e non può essere scritto==.
- **Status**: (lettura) descrive alcune capacità della funzione e lo stato di alcune eventi, principalmente legati ad errori
- **Class Code**: (lettura) codice che identifica in modo generico il tipo di funzione
- **Revision ID**: (lettura) numero di revisione della funzione, assegnato dal produttore
- **Header Type**: (lettura) tipo di header, deve essere 0 per tutte le funzioni che non siano ponti PCI-PCI o PCI-CardBus
## Transazioni nello spazio di configurazione
Solo il North Bridge (ponte ospite-PCI) può essere iniziatore di transazioni nello spazio di configurazione.

Il ponte ha un collegamento **`IDSEL`** verso ogni dispositivo PCI e ogni slot di espansione, quando il ponte vuole accedere ad un determinato registro in questo spazio di indirizzamento, attiva l'`IDSEL` del relativo dispositivo e gli passa il numero (da 0 a 7) della funzione desiderata, oltre all'offset del registro e i byte enable necessari.

Il resto della transazione è simile a quelle già viste, in particolare il ponte usa:
- `AD[7:0]` per passare l'offset, con `AD[1:0]` sempre a 0
- `AD[10:8]` per passare il numero della funzione

Se al `IDSEL` è collegato un dispositivo, risponde attivando `DEVSEL#` (entro un certo numero di clock).
## Accesso allo spazio di configurazione via software
Sebbene l'iniziatore in questo spazio sia il ponte ospite-pci, questo svolge le transazioni in nome della CPU.

La CPU però non possiede istruzioni dedicate per l'accesso allo spazio di configurazione: ==il ponte mette a disposizione due registri a 32 bit nello spazio di I/O della CPU==, tramite questi registri essa accede indirettamente allo spazio di configurazione:
- **CAP**: **Configuration Address Port**, all'indirizzo `0xCF8`, permette di selezionare funzione ed offset della parola a cui accedere
- **CDP**: **Configuration Data Port**, all'indirizzo `0xCFC`, permette di accedere alla parola selezionata tramite CAP

> Utilizzo di CAP: ![[CAPregister.svg]]

Se l'operazione in CDP è di lettura, se nessun dispositivo risponde, il bus pone tutti i bit ad 1 in CDP, facendo sapere alla CPU che non vi è nessun dispositivo collegato (nessuno attiva `DEVSEL#` in tempo).
Siccome nessun produttore ha Vendor ID uguale a `0xFFFF`, all'avvio il software prova a leggere il vendor ID della funzione 0 (che è l'unica obbligatoria) di ogni dispositivo, quelli per cui si ottiene `0xFFFF` non sono collegati.
### I base Address Register
Lo scopo dello spazio di configurazione è quindi quello di scoprire i dispositivi PCI collegati ed infine assegnargli i propri indirizzi a cui devono rispondere, per fare questo nello spazio di configurazione di ogni funzione vi è, se serve, uno o più **Base Address Register**, o **BAR**, uno per ogni **blocco** di indirizzi. Il produttore deve stabilire per ogni funzione di quanti blocchi di indirizzi necessita e per ogni blocco la lunghezza, l'organizzazione interna e se deve trovarsi nello spazio di I/O o di memoria. 
Per ogni blocco deve prevedere un BAR nello spazio di configurazione della funzione, il software di inizializzazione sceglierà con questo registro l'indirizzo di partenza di ogni blocco, in modo da evitare conflitti con i blocchi di altre funzioni.

Non tutti i bit dei BAR sono scrivibili, i primi $b$ bit non sono scrivibili e determinano la dimensione del blocco, pari a $2^b$ byte.
Inoltre il bit 0 ci da informazioni su dove deve essere reso disponibile il blocco, se il bit 0 è 1, il blocco deve essere assegnato nello spazio di I/O, se invece è 0 allora il blocco deve essere assegnato nello spazio di memoria.
Nota che nel caso di blocco nello spazio di memoria, la dimensione minima del blocco è di 16 byte, nel caso di blocchi nello spazio di I/O invece è 4 byte.

==I blocchi possono essere assegnati solo a regioni allineate naturalmente alla loro dimensione==, il software di inizializzazione sceglierà la regione e ne scriverà il numero nei bit scrivibili del BAR.

Dopo aver assegnato il blocco, il software di inizializzazione deve settare il corretto bit nel registro COMMAND dello spazio di configurazione (in base a se è in memoria o I/O). D'ora in poi la funzione risponderà agli indirizzi assegnati
# Le interruzioni
Lo standard PCI tralascia molti dettagli relativi alle interruzioni, poiché queste dipende dal particolare sistema in uso.

Ogni dispositivo ha fino a quattro piedini di uscita per le richieste di interruzione: `INTA#`, `INTB#`, `INTC#`, `INTD#`, ogni funzione può essere collegata ad al più un piedino e più funzioni possono essere collegate allo stesso piedino. Il produttore scrive in `Intr. Pin` il piedino a cui è collegata una particolare funzione (0 vuol dire nessun piedino delle interruzioni, 1 vuol dire `INTA#` ecc).

Lo standard non definisce come collegare i piedini dei dispositivi ai piedini del controllore delle interruzioni, nel nostro caso il software di inizializzazione ci scrive in `Intr. Line` il piedino dell'APIC a cui una funzione è collegata e possiamo quindi limitarci a leggere questo.