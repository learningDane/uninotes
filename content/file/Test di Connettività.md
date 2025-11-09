#uni 
# ICMP
**Internet Control Message Protocol** è un protocollo della suite IP definito per lo scambio di messagi controllo, errore e diagnostica, infatti non trasporta dati applicativi.
Serve per il rilevamento dei malfunzionamenti, ma non effettua nessuna correzione degli errori.

Un pacchetto ICMP è incapsulato in un pacchetto IP e contiene:
- **Type** (8bit) che identifica la categoria del messaggio
	- 0: echo reply
	- 3: destination network (code:0)/host (code:1) unreachable
	- 8: echo request
	- 11: time to live expired
	- 30: traceroute
- **Code** (8bit): dettaglio specifico del tipo
- checksum per il controllo dell'integrità ([[Direct Connection Networks#Internet Checksum (review)]])
- data: variabili secondo il tipo
### Ping
Serve per testare connettività, invia uno o più messaggi ICMP di tipo echo request (type 8) e attende messaggi di tipo 0.
Il pacchetto ICMP tipo 8 include:
- intestazione ICMP (tipo 8, code 0)
- identificatore e numero di sequenza
- dati
Il pacchetto viene incapsulato in un pacchetto IP e inviato al destinatario, il quale, se attivo e configurato a rispondere, genera un pacchetto ICMP tipo 0, code 0. Il tempo tra l'invio e la ricezione è misurato e mostrato come RTT (round trip time). Il comando ping normalmente invia più richieste, calcolando i valori min, avg, max e mdev.

##### Possibili errori
- network unreachable
- 100% packet lost
- unknown host (non è stato possibile risolvere il nome dell'host specificato)
##### Opzioni
- -c count
- -i interval
- -s packet size
- -f flood ping: invia pacchetti il più velocemente possibile, come una sorta di stress test
- -W: tempo massimo (in secondi) che ping aspetterà per una risposta prima di considerare il pacchetto perso
- -t Time to Live: può essere utilizzato per tracciare i numero di hop che il pacchetto attraversa, identificando problemi legati al routing
- -q quiet: visualizza solo le statistiche finali
##### Limiti
ICMP può essere bloccato da firewall per ridurre attacchi, anche se può portare a far venire meno altre funzioni vitali di gestione della rete.
Inoltre ICMP misura solo la raggiungibilità a livello IP, non la disponibilità del servizio applicativo.
Non distingue tra congestione di rete, filtri o host realmente spento.
### Traceroute
Consente di conoscere il percorso che un pacchetto IP effettua per raggiungere un’host destinatario.
Ogni pacchetto IP ha un campo TTL che i router decrementano di 1, quando arriva a 0 il router scarta il pacchetto e invia al mittente un messaggio ICMP TTL exceeded.
Traceroute sfrutta questo meccanismo: invia verso le destinazione pacchetti UDP (chiamati Sonde) con il campo TTL crescente.

Asterisco indica che la risposta non è arrivata entro il timeout.
##### Modalità di invio delle sonde
- UDP con numero di porta alto, che sarà quasi sicuramente chiusa: gli hop intermedi rispondono con ICMP time exceeded, l'host finale, non avendo un processo in ascolto su quella porta, risponde con ICMP destination unreachable, code port unreachable, questa risposta indica che il pacchetto è arrivato a destinazione.
- ICMP echo (request)
- TCP SYN: utile quando ICMP o UDP sono filtrati