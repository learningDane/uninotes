#uni 
Per configurare una interfaccia:
```Cisco IOS
Router(config)#interface type port
Router(config)#interface type slot/port
Router(config)#interface type slot/subslot/port
```

Di default quando un sistema parte le sue interfacce sono spente.

Dobbiamo togliere dalla configurazione il comando `shutdown`.
```Cisco IOS
Router(config-if)#shutdown # per spegnere
Router(config-if)#no shutdown # per accendere
Router(config-if)#exit # per uscire dalla configurazione di questa interfaccia
```
# Interfacce e porte
## Ethernet LAN 
### Standards
![[Pasted image 20260312091941.png]]
### Cabling: Copper TP
I cavi Copper Twisted Pair sono utilizzati per connettere gli host ai dispositivi di rete intermedi e sono terminati con connettori RJ-45.

Unshielded Twisted Pair (UTP) peggio di Shielded Twisted Pair (STP), ma meno costoso.
Straight-Through Cable (T568B) vs Crossover Cable
![[Pasted image 20260312093526.png]]

Questa distinzione non è più necessaria poiché i moderni calcolatori determinano automaticamente che cavo è collegato.

In packet tracer la distinzione invece va eseguita
### Cabling: Fiber Optics
I cavi in fibra ottica sono cavi in fibra di vetro attraversato da un fascio di luce, questi cavi sono enormemente più costosi ma enormemente più prestanti.

Non sono terminati con RJ-45.
# Configuring Ethernet interfaces
```CiscoIOS
Router(config)#interface FastEthernet 0/0
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)#exit
Router(config)#
```
Non serve impostare un indirizzo IP ad una interfaccia di uno switch, poiché questo non è destinazione dei pacchetti.
## WAN connections
Collegare reti geograficamente distanti: connettere due LAN.
- DTE: data terminal equipment: termina la rete del cliente sul link WAN
- DCE: data communication equipment: termina la rete del provider rispetto al cliente. *È responsabile di fornire il clock* ai dispositivi terminali dell'utente.

Per connettere due router connettiamo le interfacce seriali con un cavo seriale di tipo DCE: il primo nodo su cui clicchiamo diventa il DCE per quella connessione, il secondo diventa il DTE per quella connessione
### Configurazione Interfacce Seriali
```CiscoIOS
Router(config)#interface Serial 0/0/0
Router(config-if)#ip address 192.168.11.1 255.255.255.252
Router(config-if)#clock rate 56000 # oppure 64000, sono valori tipici validi per lo standard
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)#

Router(config)#interface fa0/0 # indica fastethernet, s indica seriale s0/0/0
Router(config-if)#description Building B Sales LAN
Router(config-if)#exit

Router#show controllers serial1/0
# mostra anche se è DCE o DTE
```
## Configuration Files
In RAM i have the Active configuration file.
In NVRAM i have the Backup Configuration File and the startup-config.

At the start up the startup-config is copied from NVRAM to RAM and is executed as the running-config.

I cambiamenti alla configurazione sono applicati direttamente alla running-config.

```CiscoIOS
Router#show running-config
```
mostra la completa running-config presente in RAM, che può essere copiata in NVRAM con:
```CiscoIOS
Router#copy running-config startup-config

# oppure
Router#copy startup-config flash:
Destination filename [startup-config]? startup-config.bak

Router#copy running-config flash:
Destination filename [running-config]? running-config.bak

Router#copy flash: starti-config
Source filename []? startup-config.bak

Router#reload
```

Tutte le operazioni di copia di configurazioni sono `safe`, ma non posso a runtime copiare da flash o da NVRAM a RAM: ci sono istruzioni che non vengono eseguite, per esempio `shutdown` e `no shutdown`.

> Per applicare una nuova config, la copio in start-upconfig ed eseguo `reload`.

Le configurazioni posso essere prese da server remoti TFPT:
```CiscoIOS
Router#copy running-config tfptp:
Address or name of remote host []? server.labnet.com
Destination filname [RT-lab-confg]?

Router#copy tftp: startup-config
...
```

Per abilitare TFTP su un server, ci clicco sopra su Packet Tracer, vado in services/TFTP e lo attivo.

Per pulire la configurazione:
```CiscoIOS
Router#erase startup-config
Router#delete flash:
Delete filename []?
```
# Processo di boot-up di un Router
1. Test dell'hardware
	1. POST: power on self test
2. bootstrap loader
3. Cerca e carica Cisco IOS
4. trova e carica la startup-config, se non la trova entra in `setup mode`.
   Questo indica un problema, perché questi dispositivi vengono forniti con una startup-config

Per avere info sul sistema:
```CiscoIOS
Router#show version
```