#uni 
Kea è un server DHCP [[open soure]] ([[Configurazione DHCP]]).

The username is `kea-api`, and the password will be expected to be in `/etc/kea/kea-api-password`.
file di configurazione: /etc/kea/kea-dhcp4.conf

Per consultare lo stato del server e controllare eventuali errori:
- sudo systemctl status kea-dhcp4-server.service
- sudo journalctl -u kea-dhcp4-server -b

Se si vuole configurare un server DHCP, dopo le
modifiche al file di configurazione, va riavviato il
servizio: `systemctl restart kea-dhcp4-server.service`

# File di configurazione
"interfaces-config"
- Sezione che configura su quali interfacce di rete il server DHCP ascolta.

"interfaces"
- Elenco delle interfacce in cui il server DHCP riceve e invia pacchetti DHCP.
	- `["eth0"]` per ascoltare su eth0
	- `["eth0/192.168.10.1"]` per vincolare all’IP 192.168.10.1 su eth0.
	- `["*"]` per tutte le interfacce, sconsigliato se la macchina ha molte interfacce di rete.

"control-socket"
- Abilita il canale di controllo locale, per inviare comandi a runtime (config-reload, statistic-get, ecc.) senza riavviare il demone.

"lease-database"
- dove e come il server salva gli assegnamenti di indirizzi IP
- "memfile" imposta il salvataggio su file /var/lib/kea
- "lfc-interval": intervallo per la compattazione periodica dei file di lease

"expired-leases-processing"
- `reclaim-timer-wait-time`: ciclo che ogni 10s individua lease scaduti
- `flush-reclaimed-timer-wait-time`: ogni 25s rimuove in blocco dal file i lease scaduti da più di `hold-reclaimed-time`
- `hold-reclaimed-time`: tiene i lease scaduti per 1 ora prima di eliminarli
- `max-reclaim-leases`: per ogni ciclo processa al massimo 100 lease, evita picchi di CPU
- `max-reclaim-time`: 250
- `unwarned-reclaim-cycles`: dopo 5 cicli in cui restano ancora tanti lease scaduti, logga un warning

timer che vengono notificati dal server al client:
- "renew-timer": dopo 900s il client prova a rinnovare con il server che gli ha dato il lease
- "rebind-timer": dopo 1800s se il rinnovo non riesce, il client ritenta in broadcast verso qualunque server
- "valid-lifetime": durata del lease in secondi

"option-data"
- opzioni globali. La gerarchia è: `globale<classe<subnet<host`. Un livello più specifico sovrascrive quello più generico

Classi per applicare opzioni o comportamenti a gruppi di client che soddisfano una condizione
- test: espressione valutata su ogni pacchetto

Le assegnazioni di indirizzi sono per subnet. Opzioni specifiche della subnet:
- routers è il default gateway. Se non impostato, i client avranno IP ma non sapranno dove instradare il traffico esterno