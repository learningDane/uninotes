#uni 
Ogni modifica fatta con `ip` è temporanea, dura fino al reboot.
Per abilitare/disabilitare un'interfaccia (man ip-link)
- `sudo ip link set <interface name> up`
- `sudo ip link set <interface name> down`
	- sudo!
Per aggiungere un indirizzo IP ad una interfaccia:
- `sudo ip addr add 10.0.3.17/24 brd 10.0.3.255 dev <interface name>`
Per rimuovere un indirizzo IP da una interfaccia:
- `sudo ip addr del 10.0.3.17/24 dev <interface name>`
Per rimuovere tutti gli IP dall'interfaccia:
- `flush?`
In [[Ubuntu]] la configurazione di rete è gestita da due tool:
- [[Netplan]]
  fornisce un'interfaccia di configurazione per le interfacce basata su file [[YAML]].
- [[Network Manager]] (o systemd-networkd, consigliato per distribuzioni server, per configurazioni di rete meno dinamiche)