#uni 
# Dispositivi
- Una HUB è un dispositivo di livello 1, funziona solo da ripetitore per rigenerare un segnale.
- Uno switch funziona a livello 2. Non ha indirizzo IP.
# Colori Connessioni
- arancione: porta collegata ma non operativa
- verde: scambia dati
# Come viene mandato un pacchetto
io sono 192.168.1.10/24, voglio mandare un pacchetto a 192.168.1.11/24, controllo se la destinazione è sul mio link o su un altro link:
- mio link: l'indirizzo MAC del mio pacchetto è quello della destinazione
- altro link: l'indirizzo MAC del mio pacchetto è quello del router  del link della destinazione
Utilizzando la maschera confronto il mio IP e quello della destinazione, se siamo sulla stessa sottorete avvio il protocollo ARP sul mio link, scopro l'indirizzo MAC e finalmente invio.

## ARP
1. SRC manda ARP frame in broadcast
2. switch riceve ARP, è un broadcast quindi lo inoltra (si salva MAC+IP di SRC)
3. DST riceve il frame ARP, risponde a DST con il suo MAC
4. switch riceve il pacchetto ARP REPLY, lo inoltra a DST (si salva MAC+IP di DST)
5. DST riceve il ARP REPLY, si salva MAC+IP di DST
6. DST può ora inviare i pacchetti a DST
## TCP