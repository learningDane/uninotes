#uni 
# IP routing table
il routing può essere effettuato in diversi modi:
- routing by destination address
- label swapping
- source routing

Quando un router riceve un pacchetto (e non è la Destinazione) la decisione su quale porta da usare per la ritrasmissione viene fatta in base alla routing table (o di forwarding).

**Lookup**: Dentro la routing table devo trovare la stringa con la sottostringa più lunga in comune con l'ip Destinatario.

Per esempio OSPF mantiene un database chiave-contenuto, routing table è improprio poiché non sempre è una semplice tabella.
## Routing Table in Cisco IOS
La routing table in CiscoIOS è in RAM ed è visualizzabile tramite il comando `show ip route`
```CiscoIOS
router#show ip route
```
Nella tabella ho per ogni sottorete di destinazione:
- l'indirizzo IP del next-stop
- l'interfaccia (porta di uscita) da usare per raggiungere la next-stop
- un tempo che indica da quanto tempo ho questa informazione. Dipende dal protocollo di routing usato.

Ci possono essere più righe per una destinazione: uno stesso algoritmo ha determinato che ci sono più percorsi con lo stesso costo con next-hop diverso: **equal cost, multiple path** (**ECMP**)-> Load Balancing.
# Routing Metrics
Nella routing table in Cisco IOS in ogni riga ho `[y/x]`, `x` è il costo.

Ci sono tante metriche ma usiamo solo `Costo`, che dipende dall'algoritmo usato: in OSPF dipende dalla banda, in RIP è l'hop-count.

Il costo 

`y` è la **distanza amministrativa**: non ha nulla a che fare con una misura reale (distanza, destinazione), è una cosa decisa a tavolino e dipende dal router. Minore è il numero e meglio è, indica quale algoritmo viene preferito.
Ovviamente `Connected` ha costo 0.
# Rotta statica
Una rotta statica è una rotta per una destinazione che inserisco manualmente.
`Static` ha distanza amministrativa 1.
## Configurazione di rotta statica
```
router#ip route ADDRESS MASK
{ip-address | exit-interface } [Distance]

router#debug ip routing
```