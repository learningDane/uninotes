#uni 
Avremo due macchine virtuali: (entrambe con Emulated VLA)
- VM - server
	- scheda 1: interfaccia in NAT connessa ad internet
	- scheda 2: interfaccia a cui è raggiungibile il server DHCP [[Kea]] 
- VM - client
	- scheda 1: interfaccia configurata come client DHCP, che chiede l'IP al server DHCP

UTM:
1. creare su UTM un network
2. macchina Server: aggiungere una interfaccia, una interfaccia deve essere "solo host", l'altra deve essere shared network
3. macchina client: basta una sola interfaccia, impostata solo host

La VM server riceve traffico da una rete interna e lo inoltra verso internet usando l'interfaccia in NAT.