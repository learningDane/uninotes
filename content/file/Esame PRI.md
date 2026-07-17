#uni 

| SIZE | # HOSTS | SUBNET MASK | BITMASK |
| ---- | ------- | ----------- | ------- |
| /22  | 1024    | 252.0       | 3.255   |
| /23  | 512     | 254.0       | 1.255   |
| /24  | 256     | 255.0       | 255     |
| /25  | 128     | 255.128     | 127     |
| /26  | 64      | 255.192     | 63      |
| /27  | 32      | 255.224     | 31      |
| /28  | 16      | 255.240     | 15      |
| /29  | 8       | 255.248     | 7       |
| /30  | 4       | 255.252     | 3       |
| /31  | 2       | 255.254     | 1       |
| /32  | 1       | 255.255     | 0       |

# Router
## Configurazione di Base
```bash
# disabilita la ricerca di comandi
no ip domain-lookup

line console 0
password cisco
login
exit
	
line aux 0
password cisco
login
exit
	
line vty 0 15
password cisco
login
exit

# imposta la password per fare `enable`
enable secret PASSWORD
# imposta la crittazione delle password
service password-encryption

# imposto le interfacce utilizzate
interface INTERFACCIA
no sh # accende l'interfaccia
ip address INDIRZZO_IP MASK # assegna un indirizzo IP all'interfaccia e gli comunica la sua subnet
exit
```
## Vlan
```bash
--- [ SETTAGGIO VLAN SU ROUTER, PER SWITCH VEDI DOPO ] ---
# encapsulation, dividere interfaccia in subinterfacce vlan:

--- [ ESEMPIO CON VLAN 10 ] ---
interface fa0/0.10 # seleziono la subinterfaccia fa0/0.10 (VLAN 10)
encapsulation dot1Q 10
ip address INDIRIZZOIPSUBINTERFACCIAVIRTUALE
exit
```
## Ospf
```bash
# creo processo ospf
router ospf 1
router-id 1.1.1.1
# specifichiamo quali interfacce danno su reti stub e quindi devono essere passive
passive-interface INTERFACCIA_VERSO_RETE_STUB # per reti stub
# su ogni router, per ogni rete a cui è collegato, indichiamo a che area appartiene
network IP_SUBNET BIT_MASK area AREA_SUBNET
...

--- [ se abbiamo un router ASBR dobbiamo inserire manualmente la rotta verso Internet pubblico e poi comunicare agli altri router nel AS che questo router ha una rotta standard verso Internet pubblico: ] ---

# Inseriamo manualmente una rotta default verso il router che effettua il forward verso la rete pubblica
ip route 0.0.0.0 0.0.0.0 IP_ROUTER_FORWARDER

# SE ASBR: Notifichiamo gli altri Router della rotta default
default-information originate
```
## DHCP
```bash
# indico quali indirizzi non sono assegnabili
ip dhcp exclude-adress INDIRIZZO_DA_ESCLUDERE
# creo una pool di indirizzi assegnabili
ip dhcp pool NOME_POOL
network IPSOTTORETE MASCHERASOTTORETE
# settare il default-gateway da notificare agli host
default-router IP_DEF-GATEWAY_SOTTORETE
# settare il DNS server da notificare agli host
dns-server IP_SERVER


# se non è questo router il server dhcp:
interface INTERFACCIA # indirizzo della rete dalla quale arrivano richieste dhcp
ip helper-address INDIRIZZO_IP_SERVER_DHCP # indirizzo del server dhcp
```
## NAT
Il NAT va settato sull'ASBR.
1. definisci una pool di indirizzi per le traduzioni
2. definisci quali indirizzi tradurre
3. traduzione dinamica: collega la lista di indirizzi da tradurre alla pool di traduzione e specifica se è OVERLOAD (ovvero se utilizzare il numero di porta per la traduzione)
4. aggiungi traduzioni statiche
5. (SE APPLICO ALTRE ACL:) specifica quali interfacce sono INSIDE e quali OUTSIDE
6. SICUREZZA: blocca pacchetti provenienti da indirizzi non tradotti in modo che non escano dalla rete privata
7. SICUREZZA: blocca pacchetti provenienti dall'esterno con destinazione un indirizzo privato
```bash
# definiamo se una interfaccia da verso la rete privata o quella pubblica, ovvero chi è INSIDE e chi è OUTSIDE
# in pratica definiamo per quali reti viene effettuata la traduzione
interface INTERFACCIA
	ip nat inside # questa interfaccia da verso la rete privata
# definiamo le reti collegate a quelle per cui effettiamo la traduzione
interface INTERFACCIA
	ip nat outside 

# definiamo una pool di indirizzi pubblici IN CUI  tradurre gli indirizzi privati
ip nat pool NOMEPOOL IPINIZIO IPFINE netmask MASCHERA

# creiamo una ACL standard, per definire quali indirizzi tradurre
ip access-list standard NOME_LISTA
	# definiamo quali indirizzi tradurre
	permit INDIRIZZO BITMASK # permettiamo questi indirizzi
	deny any # blocca tutti gli altri indirizzi

# configuriamo il NAT DINAMICO con OVERLOAD (ind_pub < ind_priv), anche chiamato PAT (Port Address Translation)
# ip nat inside source: traduce IP provenienti da rete interna
# list NOME_LISTA: specifica QUALI indirizzi TRADURRE
# pool NOMEPOOL: specifica che pool di indirizzi usare per le traduzioni
# differenzia le connessioni tramite il numero di porta
ip nat inside source list NOME_LISTA pool NOMEPOOL overload

# aggiungiamo una traduzione statica
ip nat inside source static IP_DA_TRADURRE IP_TRADUZIONE

--- [ QUANTO SOPRA BASTA PER IL NAT DI BASE] ---
--- [ PER ALTRE RESTRIZIONI VEDI ACL] ---
```
## ACL
NOTA: le ACL funzionano in ordine!
```bash
# definiamo se una interfaccia da verso la rete privata o quella pubblica, ovvero chi è INSIDE e chi è OUTSIDE
# in pratica definiamo per quali reti viene effettuata la traduzione
interface INTERFACCIA
	ip nat inside # questa interfaccia da verso la rete privata
# definiamo le reti collegate a quelle per cui effettiamo la traduzione
interface INTERFACCIA
	ip nat outside 

# blocchiamo i pacchetti provenienti da indirizzi privati non tradotti
# definiamo una ACL per definire gli indirizzi dai quali bloccare le traduzioni
ip access-list standard INSIDE-OUT
	deny INDIRIZZO BITMASK # INDIRIZZO BITMASK: indirizzi della rete privata
	permit any

# blocchiamo i pacchetti proveniente dalla rete pubblica con destinatari indirizzi privati non tradotti
ip access-list extended OUTSIDE-IN
	# una ACL extended permette di specificare altre cose oltre al solo IP di provenienza
	deny ip any INDIRIZZO BITMASK # blocca ogni pacchetto con destinatario INDIRIZZO BITMASK
	permit ip any any

###############################################
# SINTASSI ACL EXTENDED:
ip access-list extended NOME_ACL
 [permit | deny] protocol sorgente/wildcard [porta] destinazione/wildcard [porta] [opzioni]
###############################################
 
 # applichiamo le ACL all'interfaccia che dà sulla rete pubblica
 interface INTERFACCIA_OUT
	 ip access-group OUTSIDE-IN in # applica la ACL ai pacchetti in INGRESSO
	 ip access-group INSIDE-OUT out # applica la ACL ai pacchetti in USCITA
```

Limitare il traffico a solo HTTP e HTTPS:
```bash
--- [ ATTENZIONE, QUESTI SONO SOLO SPUNTI ] ---
ip access-list extended LAN-IN
	permit tcp any any established
	exit

ip access-list extended LAN-OUT
	# per permettere il DHCP: permetto il traffico udp da qualsiasi IP se proviene dalla porta 68 (BOOTP client) verso qualsiasi IP se sulla porta 67 (BOOTP server)
	permit udp any eq bootpc any eq bootps
	permit udp any eq bootps any eq bootpc # speculare per copiare e incollare
	
	permit tcp any any eq www # permette HTTP (potrebbe anche essere 80)
	permit tcp any any eq 443 # permette HTTPS
	exit
```
## VPN - GRE TUNNEL
1. Assegna una Subnet punto-punto per gli indirizzi IP delle interfacce Tunnel dei due router, servono 2 indirizzi IP quindi serve un blocco /30 - .252
```bash
--- Router A ---
interface Tunnel0
tunnel mode gre ip
ip address IP_INTERFACCIA_TUNNEL_A 255.255.255.252
tunnel source IP_INTERFACCIA_A_verso_B
tunnel destination IP_INTERFACCIA_B_verso_A
 
 
--- Router B ---
interface Tunnel0
tunnel mode gre ip
ip address IP_INTERFACCIA_TUNNEL_B 255.255.255.252
tunnel source INTERFACCIA_B_verso_A
tunnel destination IP_INTERFACCIA_A_verso_B
```
## ISP
```bash
interface se0/0/0
no sh
i 255.255.255.x
exit

ip route LAN_DESTINATARIA SUBNETMASK INTERFACCIA_DESTINAZIONE

--- [ all'esame' ] ---
ip route IP_LAN_PRIVATA SUBNET INTERFACCIA_VERSO_LAN
```
# Switch
Ordine:
1. conf di base?
2. VLAN:
	1. assegna VLAN a interfacce:
		1. interface range fa0/10-30
		2. switchport...
	2. VLAN di management:
		1. interface vlan 99
		2. ip address indirizzo mask
		3. no sh
		4. exit
		5. ip default-gateway indirizzo
	3. spanning tree (configurare gli switch connessi al router-on-a-stick come Root Bridge):
		1. spanning-tree vlan 10 root primary
		2. spanning-tree vlan 30 root secondary
## Configurazione di Base
```ciscoIOS
enable
conf t
no ip domain-lookup

line console 0
password cisco
login
exit

line vty 0 15
password cisco
login
exit
	
enable secret cisco
service password-encryption

interface vlan 1
ip address INDIRIZZO MASK
no sh
ex
ip default-gateway INDIRIZZO

interface range fa0/0-10
switchport port mode access
switchport port-security
switchport port-security mac-address sticky
exit

interface range fa0/10-24, gi0/1-2
shutdown
exit
```
## STP
OPZIONALE
```bash
# Imposta uno spanning tree diverso per ogni vlan
spanning-tree mode pvst

# imposta questo switch come root per la VLAN specificata
spanning-tree vlan 10 root primary

# è buona norma impostare anche il secondary root per ridondanza
spanning-tree vlan 30 root secondary

--- [ SULLE PORTE SWITCH-ROUTER ] ---
# puoi attivare portfast, tanto non partecipano al loop
interface INTERFACCIA_SWITCH-ROUTER
spanning-tree portfast
```
## VLAN
```bash
# per link untagged: mode access
# per link tagged: mode trunk
# per link ibridi: mode hybrid
vlan NUMERO
	name NOMEVLAN
	exit

interface fastEthernet 0/4-10
	switchport access vlan NUMERO
	switchport mode access
	exit
	
interface range fastEthernet 0/11-30
	switchport trunk native vlan NUMERO
	switchport trunk allowed vlan 1,2,3,ecc
	switchport mode trunk
	exit
```
## Multi Layer Switch
```bash
# OGNI COSA CHE SU UN ROUTER VUOI IMPOSTARE SU interface INTERFACCIA.VLAN, SU UN MLSC VA FATTO SU interface vlan VLAN

# se imposto un server DHCP devo impostare sul MLSC l'helper-address, questo va fatto nella interfaccia VLAN, non sulla Fastethernet
interface vlan VLAN
ip helper-address INDIRIZZO_IP_SERVER_DHCP

# attivo il routing
ip routing

--- [ Per una interfaccia con VLAN: ] ---
switchport trunk encapsulation dot1q # imposta il metodo di tagging dot1q
interface INTERFACCIA
no sh
switchport mode trunk
switchport trunk native vlan VLAN
switchport trunk allowed vlan VLAN
exit
# Configurazione delle VLAN come se fosse un router
	# su un router dovresti fare `interface INTERFACCIA.VLAN` ecc
	# qua fai solo `interface vlan VLAN`
interface vlan VLAN
ip address INDIRIZZO INTERFACCIA_VLAN
no sh
exit

--- [ SU UNA INTERFACCIA CHE VOGLIAMO CONFIGURARE COME ROUTER: ] ---
interface INTERFACCIA_ESTERNA_ALLA_LAN
no switchport # imposta l'interfaccia come esterna alla LAN, come un router
# configurazione come interfaccia di un router:
ip address INDIRIZZO_INTERFACCIA
no sh
exit
```
# Show
```bash
show vlan brief
show ip interface brief
show arp
show running-config
show interfaces status

--- [ router ] ---
show ip ospf neighbor
show ip ospf database
show ip protocols
show ip nat translations
show access-lists NOMELISTA
show ip route

--- [ switch ] ---
show interface trunk
```

# Note
```bash
interface range 0/0-1 # NON INCLUDE LE SUBINTERFACCE 0/1.10 ecc
RICORDA I DEFAULT GATEWAY PER DISPOSITIVI IMPOSTATI MANUALMENTE
```
## VLAN su Switch
### Porta Access

> La VLAN è implicita nella porta, non la "vede" sul frame

```bash
interface INTERFACCIA
switchport mode access
switchport access vlan VLAN
```
- riceve frame NON taggati
- lo switch associa INTERNAMENTE questi frame alla VLAN per gestirli
- una porta access invia frame senza taggarli
### Porta Trunk
```bash
interface INTERFACCIA
switchport mode trunk
switchport trunk allowed vlan VLAN,VLAN,VLAN
switchport trunk native vlan VLAN_NATIVE
```
- trasmette il frame aggiungendo il tag della vlan associata al frame internamente allo switch
- ⁠quando RICEVE un frame untagged, lo associa alla VLAN_NATIVE di quella porta trunk
- se deve TRASMETTERE un frame associato alla VLAN_NATIVE, lo trasmette senza tag