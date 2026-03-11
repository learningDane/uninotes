#uni 
# Introduzione
I router sono computer specializzati nel mandare pacchetti sulle reti. Sono responsabili per l'interconnessione di reti e trovare il percorso migliore verso la destinazione per un pacchetto. Inoltre sono responsabili per il forwarding dei pacchetti.

Le reti locali (quindi i loro router) sono interconnesse tramite ethernet o WAN (tipicamente punto-punto).

Forwarding:
I router guardano l'IP di destinazione del pacchetto ricevuto, controllano se sulla loro routing table vi è una entrata per esso, al quale in caso è associata l'interfaccia verso la quale il pacchetto va reindirizzato.

Come viene riempita la tabella di routing:
1. con entry statiche: correlazione tra IP di destinazione e "next stop"
2. protocolli di routing: inter-area o intra-area
# Il sistema operativo
Cisco IOS: **Cisco Internetwork Operating System** è il sistema operativo presente sui router CISCO, diventano uno standard di fatto.

Un'alternativa è il Juniper Network Operating System (**Junos**).

Questi sistemi operativi forniscono:
- security
- addressing
- interfaces
- routing
- QoS
- Managing Resources

I servizi offerti dal Cisco IOS sono accessibili tramite CLI, alla quale ci si connette tramite:
- Un secondo host connesso fisicamente al router tramite porta di console (necessario in caso di prima configurazione o disaster recovery)
- Un secondo host connesso tramite virtual terminal
	- tramite Telnet (tipicamente disabilitato)
	- tramite SSH
Normalmente ci sono anche porte Ausiliarie.
# Interfaccia
Cisco IOS (e la maggior parte delle alternative) utilizza una **interfaccia modale**, in una determinata modalità è disponibile solo un sottoinsieme dei comandi ed un certo livello di privilegio.

Le modalità:
1. User EXEC: esaminazione non dettagliata del router
2. Privileged EXEC: più dettagli sul router, debug e test, manipolazione file
3. Global Configuration (config): da qui si accedono ai modi di configurazione:
	- Interface (config-if)
	- Routing Engine (config-router)
	- Line (config-line)
1 e 2 sono dette **modalità primarie**.

Prompt Structure:
```prompt
Router> //user
Router# //user privileged
Router(config)#
Router(config-xxxx)#
```
Nel caso di accesso ad uno switch, al posto di `Router` vi sarà `Switch`.

Cambio modalità:
```prompt
Press RETURN to get started.

User Access Verification
Password:
router>
router>enable
Password:
router#
router#disable
router>
router>exit
```

> Diagramma cambio modalità: ![[Pasted image 20260309153806.png]]

Ciascuna delle diverse modalità ha un set di comandi esclusivo.
# Comandi
```prompt
show
	version
	flash
	interface
	processes
	memory
	stacks
	buffers
	startup-config
	running-config
	arp
	ip interface
	ip interface brief
	ip interface (interface slot)/(port number)
	
Switch(config)#line console 0
switch(config-line)#password tua_password
switch(config-line)#login

# per disattivare questa configurazione:
switch(config-line)#no password tua_password

switch(config)#line vty 0 4
ecc

# enable secret password
router(config)#enable secret cisco

# versione NON criptata
router(config)#enable password cisco

router(config)#banner motd # day banner da mostrare #
# di solito si mette tipo controllo accessi per motivi legali
```
# Naming dei Router
Esiste RFC 1178: "Choosing a name for your computer"

Best practices:
- no spazi
- solo caratteri alfanumerici
- abbastanza corto
Il default per un router è `Router`.