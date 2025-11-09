#uni 
# tcpdump
Opzioni:
- -c : count
- -i : interface
- -q : quick/quiet, visualizza meno informazioni
- -n : non risolve i nomi [[DNS]] (più veloce e chiaro)
- -v, -vv, -vvv : verbose, livello di dettaglio crescente
- -w nome_file.pcap (write) : scrive l'output in un file (da aprire con [[Wireshark]])
- -r nome_file.pcap (read) : legge un file precedentemente creato con [[Wireshark]]

- Per filtrare i pacchetti: man pcap-filter: descrive come formattare il filtro
	- sudo tcpdump port 80
	- sudo tcpdump host 192.168.4.2
	- sudo tcpdump udp and port 5555
	- sudo tcpdump dst host google.it and port 80
	- sudo tcpdump src host 192.168.0.2 and not port 90
- Per filtrare i pacchetti di richiesta DHCP ([[Kea]]) 
	- sudo tcpdump -i enp0s3 port 67 or port 68 -n -vv