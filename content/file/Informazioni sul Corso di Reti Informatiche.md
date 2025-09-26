#uni 
Prerequisiti:
- linguaggio ad alto livello: [[C]]/[[C++]]/[[Java]]
- [[Calcolatori Elettronici]]

Consigliato seguire [[Reti Informatiche]] in parallelo con [[Sistemi Operativi]].
Sviluppiamo una sottoparte di sistemi operativi, quella di networking.

# Programma
1. Applicazioni di rete
	1. paradigmi client-server e peer-to-peer (p2p)
2. Applicazioni client-server
	1. web, file transfer, email, dns
3. applicazioni peer-to-peer
	1. ricerca di contenuti, distribuzione di file, bitTorrent
4. programmazione di applicazioni di rete
	1. interfaccia a socket, client e server basati su rocket
---
### Reti a connessione diretta
- collegamento punto-punto
	- framing, errori, trasferimento dati, controllo di flusso, protocollo PPP
- reti locali
	- accesso multiplo, reti locali, reti locali ethernet
- Reti a commutazione di un pacchetto
- switch
- ethernet basata su switch
- circuito virtuale e datagram
- reti packet-switched a copertura geografica
---
### Interconnessione di reti (internet)
- protocollo IPv4
	- instradamento dei datagram, assegnazione indirizzi, protocollo DHCP, traduzione indirizzi (NAT), risoluzione di indirizzi IP (protocollo ARP), cenni ad IPv6
- routing
	- algoritmi Link-state e distance vector, protocolli di routing intra-as (OSPF) e inter-as (BGP)
- protocolli di trasporto (UDP, TCP)
	- multiplexing/demultiplexing dei datagram, trasferimento affidabile dei dati, controllo del flusso, controllo della congestione
---
### Sicurezza
- minacce alla sicurezza
- riservatezza della comunicazione
	- crittografia a chiave simmetrica e asimmetrica
	- distribuzione e certificazione delle chiavi
- integrità dei messaggi
	- message authentication code
	- firma digitale
	- autenticazione della controparte
- sicurezza a livello applicazione (PGP)
- sicurezza a livello middleware (TLS)
- sicurezza a livello IP (IP-sec)
- difesa di sicurezza (firewall, IDS)
---
### Unix
	me lo sono perso
---
- Progetto di una applicazione distribuita
	- client-esrver o p2p
	- a partire dalle specifiche
- Realizzazione
	- svolgimento individuale
- Da discutere in sede di esame
---
# Esame
- discussione del progetto (è praticamente un pretest, conta poco il voto)
- prova orale a cui si accede dopo una valutazione sufficiente al progetto
	su argomenti svolti durante il corso