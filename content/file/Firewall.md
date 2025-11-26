#uni 
# Concetto di firewall e packet filtering
Il firewall è un sistema di sicurezza che controlla le connessioni in ingresso e in uscita e applica delle regole di blocco e filtraggio.

Il firewall può essere implementato via hardware o via software., inoltre può operare a livello di rete (network firewall) o di singola macchina (host-based firewall).
## Tipi di Firewall
- network layer (packet filter)
	- opera a livello di TCP/IP, analizzando gli header IP, TCP e UDP
- application layer
	- fa deep packet inspection
	- più efficace ma più esoso computazionalmente
	- efficace anche contro malware, ecc
## Packet filtering
Questi firewall si dividono in:
- **stateless**: ogni pacchetto viene analizzato singolarmente
- **stateful**: tiene traccia delle connessioni TCP e degli scambi UDP in corso, più efficace ma complesso e pesante rispetto allo stateless
### Funzionamento
Il firewall contiene una tabella di regole, ogni regola contiene:
- caratteristiche del pacchetto (i criteri)
- azione da intraprendere (target)
	- DROP
	- ACCEPT
	- ecc

<table>
	<tr>
		<th>Indice</th><th>IP sorgente</th><th>Porta sorgente</th><th>IP destinatario</th><th>Porta destinatario</th><th>Azione</th>
	</tr>
	<tr>
		<td>1</td><td>131.114.0.0/16</td><td></td><td>131.114.54.4</td><td>80</td><td>DROP</td>
	</tr>
</table>
Per ogni pacchetto il firewall:
1. analizza l'header
2. scorre la tabella delle regole
3. trova una regola che corrisponde alle caratteristiche del pacchetto analizzato
4. intraprende l'azione specificata

> Le regole sono processate nell'ordine in cui vengono inserite, e solo la prima corrispondenza trovata viene applicata!

### Default
La regola di firewall di default è quella in fondo alla lista, ha come criterio qualsiasi pacchetto.
#### white list
la regola di default: firewall inclusivo:
<table>
	<tr>
		<td>ultima posizione</td><td>0.0.0.0</td><td></td><td>0.0.0.0</td><td></td><td>BLOCCA</td>
	</tr>
</table>
Blocca tutti i pacchetti, a meno che non vengano specificatamente accettati da regole precedenti. Questa regola deve essere messa per ultima.
# Netfilter
Netfilter è il componente del kernel [[Linux]] che offre le funzionalità di:
- stateless/stateful packet filtering
- `NAP[P]T`: estensione di [[Network Address Translation]] che consente di mappare molti indirizzi IP in un unico indirizzo IP
# iptables
Iptables è il programma CLI che serve per configurare le tabelle delle regole.
Iptables lavora su diverse tabelle (tables), ognuna specifica per una funzionalità (noi vediamo solo le tabelle `filter` e `nat`).
Ogni tabella contiene diverse catene (chains), ogni catena contiene una lista di regola da applicare a una categoria di pacchetti.
## filter
La tabella filter ha 3 catene:
- input
- output
- forward
## Comandi
Per visualizzare le regole:
`# iptables [-t table] -L [chain]`
Se non si specifica una tabella, viene usata filter.
Se non si specifica una catena, vengono elencate tutte le catene.

```shell
# aggiungere una regola in fondo alla catena
iptables [-t table] -A chain rule-specification


# aggiungere una regola in una posizione specifica
iptables [-t table] -I chain [num] rule-specification
# se non si specifica num, vale 1 (in testa alla catena)

# rimuovere una regola dalla catena
iptables [-t table] -D chain rule-specification
iptables [-t table] -D chain num


# rimuovere tutte le regole
iptables [-t table] -F [chain]


# per cambiare la regola di default
iptables [-t table] -P target
```
## regole
```
-p <protocollo> protocollo (TCP, UDP, ICMP, …)
-s <address> indirizzo sorgente
-d <address> indirizzo destinazione
--sport <port> porta sorgente
--dport <port> porta destinazione
-i <interface> interfaccia di ingresso
-o <interface> interfaccia di uscita
-j <target> azione (DROP/ACCEPT)
```
## Salvare e applicare le regole
Le regole non vengono salvate permanentemente, è necessario reimpostarle all'avvio.

```shell
# salvare le regole
iptables-save > file

# caricare le regole
iptables-restore < file
```
# NAT/PAT
Iptables gestisce il `NA[P]T` tramite la tabella *nat*.
La tabella nat ha 3 catene:
- **prerouting**: D-nat: alterare indirizzo/porta di destinazione dei pacchetti in arrivo
- **output**: D-nat: alterare indirizzo/porta di destinazione dei pacchetti in uscita dai processi locali prima del routing
- **postrouting**: S-nat: alterare indirizzo/porta sorgente dei pacchetti in partenza