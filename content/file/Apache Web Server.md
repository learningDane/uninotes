#uni 
Installare apache2 in [[Ubuntu]].
Dopo l'installazione si avvia automaticamente il server.
```bash
systemctl status apache2
```
Oppure andare a `http://localhost/` che mostra la pagina in `/var/www/html/index.html`.
>Funziona perché in `/etc/hosts` c'è l'abbinamento `127.0.0.1 localhost`.

Apache può accettare e servire più richieste contemporaneamente.
Si può configurare il modello I/O da usare.

Per interagire con il server si usa il comando `apache2ctl <comando>`
- start
- stop
- restart
- status
- configtest
oppure `service apache2 <comando>`:
- start
- stop
- restart
- reload
entrambi privilegiati.

La directory principale è `/etc/apache2`, il file di configurazione principale è `/etc/apache2/apache2.conf`.
La configurazione si specifica attraverso delle direttive, eventualmente raggruppate da direttive contenitore.
```apache2.conf
# commento
Direttiva1 valore
Direttiva2 valore

<contenitore valore>
	Direttiva3 valore
	...
</contenitore> # fine contenitore
```

Apache usa un sistema modulare: il file di configurazione globale recupera pezzi di configurazione da altri file usando la direttiva `Include`.
Ad esempio il file `etc/apache2/ports.conf` contiene le direttive per specificare le porte da usare.

I pezzi di configurazione si mettono in `/etc/apache2/conf-available/`.
I file vengono abilitati con:
```
# a2enconf <nome_file>
```
Il comando crea un *soft link* nella directory `/etc/apache2/conf-enabled`.
Il file di configurazione principale è impostato per includere tutto quello che trova in `conf-enabled`.
Bisogna riavviare il server per applicare una nuova configurazione.
Un file si disabilita con:
```
# a2disconf <nome_file>
```

I pezzi di configurazione che forniscono funzionalità complesse sono detti **moduli** e si trovano in `/etc/apche2/mods-available`.
Si abilitano e disabilitano con:
```
# a2enmod <nome_file>
# a2dismod <nome_file>
```
Un modulo abilitato ha un soft link in `mods-enabled`.