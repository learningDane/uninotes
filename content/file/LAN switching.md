#uni 
Un HUB inoltra ogni pacchetto che riceve su tutte le sue interfacce (salvo quella dalla quale ha ricevuto il pacchetto), questo vuol dire che il broadcast domain coincide con il collision domain.

**Learning Switching** : uno switch non si comporta come un HUB: le collisioni su uno switch sono limitate ad un singolo link. Uno switch impara dinamicamente il collegamento tra indirizzo MAC e porta e lo inserisce nella **MAC address Table**.

La MAC address Table riporta:
- MAC address
- port id
- Vlan id
- tipo:
	- statico
	- dinamico
- ageing
- STP state

Processo di Forwarding:
1. ricevo frame su porta x
2. errori di ricezione?
	1. si: scarto
3. no: la porta x è in stato di forwarding?
	1. no: scarto
4. si: la destinazione è nella MAC address table?
	1. no: flooding, tranne che su x
5. si: la destinazione è sulla porta x?
	1. si: scarto
6. no: forward sulla porta

Processo di Learning:
1. indirizzo sorgente è nella MAC table?
	1. no: aggiungi entrata nella MAC table
2. la porta di ricezione è la stessa di quella nella MAC table?
	1. no: aggiorna entrata
3. resetta ageing time
# config
```ciscoIOS
interface fa0/18
switchport mode access
switchport access vlan 99 # permette alla interfaccia di comportarsi come facente parte di vlan 99
```
# Verifying Configuration
```CiscoIOS
show interfaces [interface-id]
show startup-config
show running-config
show flash:
show version
show history
show ip [interface | http | arp]
show mac-address-table
```
# SSH
Serve indirizzo IP per switch: vlan
```ciscoIOS
configure terminal
ip domain-name mydomain.com
crypto key generate rsa
1024
end
show ip ssh
username admin secret password
line vty 0 15 # tutte le linee da 0 a 15
transport input ssh
login local

exit
ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 5

show ip ssh
```
# Security
```ciscoIOS
line console 0
password ..
login

line vty 0 15
password ..
login

enable secret ..

service password-encryption
```