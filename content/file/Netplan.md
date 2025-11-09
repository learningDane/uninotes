#uni 
Per configurare Netplan andare nella cartella `/etc/netplan/`

Il nome del file per convenzione ha un prefisso numerato (01-) per controllare l'ordine di
esecuzione dei file di configurazione all’accensione. Questo file applica una configurazione
ampia (“all”), delegando tutte le interfacce a NetworkManager.

Priorità: se sono presenti altri file di configurazione, hanno prefissi diversi (02-) per
determinare la loro priorità

>Le configurazioni verranno concatenate in ordine crescente di nome di file, con eventuali sovrascrizioni per configurazioni diverse delle stesse impostazioni

Per vedere la configurazione di Netplan:
- `sudo netplan get`
- `sudo netplan status`: fa vedere solo le interfacce attive
- `sudo netplan status -all`: fa vedere tutte le intefacce
questo comando unisce tutti i file [[YAML]] in ordine alfabetico crescente per ottenere la configurazione globale.
# 01
Troviamo il file `01-network-manager-all.yaml`, che contiene la semplice configurazione di rete, dove tutto viene delegato al **network manager**.
# 50
È presente anche un file `50-cloud-init.yaml`, inserito da **cloud-init**, che è un tool usato per automatizzare la configurazione di rete al bootstrap.
==Non è possibile modificarlo==.
Qui viene specificato al network manager che l'interfaccia di rete enp0s1 (o comunque la interfaccia attiva) verrà configurata automaticamente dal **DHCP**.
# Configurazione
```bash
# Se non viene premuto ENTER entro 120 secondi dall'invio di questo comando, la configurazione NON viene applicata
sudo netplan try

# per applicare direttamente la nuova configurazione
sudo netplan apply
```
### Esempio
Aggiungiamo un indirizzo IP ad una interfaccia.
```yaml
# file 51-enp0s3-interface.yaml
network:
	ethernets:
		enp0s3:
			addresses: [192.168.0.1/24]
```
nel terminale:
```bash
# rimuoviamo la read permission agli utenti non root
# 600 = 6.0.0 = 110.000.000 = rw-.---.---
sudo chmod 600 51-enp0s3-interface.yaml
```
# Configurazione del default gateway
[[Configurazione del Default Gateway]]
aggiungere queste righe alla configurazione delle interfacce:
```yaml
routes:
    - to: default
    - via: 192.168.1.1
```

configurare DNS specifici sull'intefaccia di rete con Netplan:
```yaml
network:
    version: 2
    renderer: NetworkManager
    ethernets:
        enp0s1:
            addresses: [10.10.10.2/24]
            nameservers:
                search:
                -"mycompany.local" # quando cerco un hostname senza dominio completo, il sistema prova ad aggiungere mycompany.local alla fine del nome per completare la richiesta nella rete locale
                addresses:
                    -    10.10.10.253
                    -    8.8.8.8
```