#uni 
Il **default gateway** è il router all'interno di una rete verso cui gli host connessi inviano pacchetti destinati a reti non locali.
Il default gateway principale deve essere unico, non ci possono essere più di un default gateway tra cui scegliere, altrimenti si possono presentare problemi:
- routing ambiguo
- asimmetria del traffico
- connettività intermittente
quindi ci deve essere un solo default gateway, o perlomeno una chiara gerarchia tra i default gateway.

# Configurazione
```shell
# per visualizzare la tabella di routing
ip route show
	# default via 192.168.69.1 dev eth0 proto dhcp src 192.168.69.4 metric 100
	# 192.168.69.0/24 dev eth0 proto kernel scope link src 192.168.69.4

# per aggiungere rotte:
# invio diretto nella rete locale:
ip route add 192.168.1.0/24 dev eth0
	# tutto il traffico verso la rete 192.168.1.0 passerà attraverso eth0
# default gateway
ip route add default via 192.168.1.1

# per scoprire la rotta usate:
 ip route get 70.143.3.67d
	 # usare indirizzo IP del target
```

configurazione con [[netplan]]: [[Netplan#Configurazione del default gateway]].