#uni 
Tutti i dischi vengono resi accessibili (montati) tramite un unico filesystem virtuale:
- `/` è la directory principale
- `/root` home directory dell'utente root
- `/home` contiene le varie *home directory* degli utenti
- `/sbin` per programmi di sistema
- `/dev` per file del dispositivo
- `/etc` per file di configurazione utente
- `/usr` per applicazioni utente
- `/var` per dati variabili tipo log
- `/boot` per file per il boot
- `/opt` per applicazioni terze
- `/tmp` per file temporanei
- `/lib` per librerie condivise
# Come descrivere un percorso
Percorso assoluto: `/home/utente/Documents/......`
Percorso relativo: `Documents/....` se sono in `/home/utente` 
Caratteri speciali:
- `~` indica la **nostra** home directory
- `.` indica la directory corrente
- `..` indica la directory padre