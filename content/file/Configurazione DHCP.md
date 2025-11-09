#uni 
Il dynamic host configuration protocol consente la configurazione automatica e dinamica dei parametri TCP/IP degli host, UDP porta 67:
- indirizzo IP
- maschera di rete
- indirizzo del gateway
- indirizzo del server DNS
All'interno della rete è configurato un **server DHCP**, quando il client si connette alla rete, il server gli fornisce i parametri di configurazione:
- indirizzo IP viene scelto dall'insieme di indirizzi IP disponibili all'interno della rete
- indirizzo IP e altri parametri hanno una scadenza, quando questa viene raggiunta l'host deve ricontattare il server DHCP
# Processo di leasing IP
Protocollo **DORA**:
- discover
- offer
- request
- acknowledge
### Protocollo
1. Host (con IP 0.0.0.0) contatta il server all'indirizzo 255.255.255.255,67, con DHCPDISCOVER
2. Server risponde in broadcast (255.255.255.255,68) con DHCPOFFER, indicando un indirizzo IP disponibile
3. Host invia DHCPREQUEST
4. Server invia in broadcast DHCPACK
# Server DHCP - Kea
The username is `kea-api`, and the password will be expected to be in `/etc/kea/kea-api-password`.
Password: studenti
[[Kea]].
file di configurazione: /etc/kea/kea-dhcp4.conf
# Client DHCP
Per impostare la configurazione dell'indirizzo di una interfaccia tramite DHCP bisogna impostare dhcp4 a true:
```yaml
network:
    ethernets:
        enp0s1:
            dhcp4: true
```