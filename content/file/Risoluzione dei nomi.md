#uni 
- Adesso sappiamo che, per comunicare, un host ha bisogno di:
	– Indirizzo IP
	– Maschera di rete
	– Indirizzo del default gateway
- Vorremmo usare dei nomi simbolici invece degli indirizzi IP, che sono usati dai router:
	- ”localhost” invece di 127.0.0.1
	- ”hostB” invece di 192.168.1.3
	- ”www.google.it” invece di… boh!
- Domain Name System ([[DNS]])

Il file `/etc/hosts` contiene un elenco di associazioni indirizzo/nome risolti staticamente, ricavati a partire dal nome.

Il file `/etc/resolv.conf` contiene l'indirizzo delle macchine dedicate alla risoluzione dei nomi nella rete attuale. Contiene quindi gli indirizzi IP dei server DNS che l'host può contattare

Il comando `nslookup www.apple.com` contatta il server DNS che restituisce le informazioni necessarie alla risoluzione del nome, in particolare l'indirizzo (gli indirizzi,[[IP]] e IPv6) è nel campo "Address".
# Name service switch (NSS)
Questo meccanismo consente ai sistemi [[Unix]] di ricavare nomi di "cose" da diverse fonti.
Il file `/etc/nsswitch.conf` specifica le fonti da usare e l'ordine in cui usarle.
Il file `/etc/hosts` serve invece per la risoluzione statica.