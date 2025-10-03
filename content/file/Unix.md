#uni 
[[Comandi Unix Network]] 
Unix nasce nel 1969.
Ne escono 3 derivati:
- BSD (1977)
	- Darwin (MacOS)
- GNU (1984)
	- GNU/Linux
- Solaris (1992)
# Caratteristiche di Unix
Unix è Case sensitive!
- multitasking
- multiutente
- portabile
- modulare
# Redirezione IO
I processi hanno tre canali di input/output standard:
- stdin: input da tastiera
- stdout: output da schermo
- stderr: messaggi di errore su schermo
Possiamo reindirizzare l'output dei comandi dentro file o altro:
- `>` invia stdout ad un file, se il file non esiste viene creato, se esiste viene sovrascritto
- `2>` invia stderr in un file
- `&>` invia sia stdout sia stderr in un file
- `>>, 2>>, &>>` stessa cosa ma non sovrascrive, concatena
- `comando > fileSTDOUT 2> fileSTDERR` scrive stdout in un file e stderr in un altro

- `<` recupera l'input da un file
# Pipeline
Il simbolo `|` collega l'output di un comando all'input del successivo
# Comandi Unix di base
- `shutdown` di default solo root può lanciarlo
	- `-h now` halt
	- `-r now` reboot
- `cd` change directory
- `echo "contenuto" > file.txt` sostituisce il contenuto con quello nuovo.
  Per aggiungere invece bisogna usare `echo "contenuto" >> file.txt`
- `pwd` print working directory, mostra il percorso assoluto attuale
- `ls` elenca elementi cartella attuale
	- `-l` long (più informazioni per ogni file)
	- `-a` all (anche file nascosti)
- `man` mostra il manuale contenente la descrizione esaustiva del comando specificato, la sintassi, le opzioni, i messaggi di errore
	- `man man` è il manuale di man, che è diviso in sezioni
	- `man comando` è il manuale del comando
	- `man 3 comando` va alla al manuale della funzione c di comando
	- non solo per comandi: anche funzioni del kernel, funzioni delle librerie [[C]], file di configurazione..
- `whatis` informazioni di base su argomento
- `apropos` serve per ricercare una parola in nomi e descrizioni, che comandi ho per fare una determinata cosa
- `mkdir nome` fa cartella
- `rmdir cartella` rimuove cartella, ma solo se è vuota
- `cp src dest`
	- `cp src1 src2 dst_dir` copia tutti i file dentro un cartella
- `mv src dest` 
- `touch nome_file` aggiorna il timestamp di accesso e modifica di un file, se il file non esiste lo crea
- `cat file1 file2` concatena il contenuto dei file e li stampa a video nello *standard output*, se è un solo file ne stampa solo il contenuto
- `rm file1 file2` rimuove file
	- `rm -r nome_cartella` cancella la cartella e tutto il suo contenuto
	- `rm -d` rimuove cartelle vuote
	- `rm -f` force: non prompta, ignora file non esistenti
- `less` visualizza file interattivamente un po' alla volta
- `head/tail` permetto di visualizzare solo la prima/ultima parte di uno o più file
	- `-c` specifica numero di byte
	- `-n` specifica numero di righe (di default 10)
- `sort`
- `su` *switch user* serve per accedere al terminale di un altro utente, se non specifico argomento, si accede al terminale di root, chiede la password dell'utente con il quale si vuole accedere
- `sudo comando` serve per lanciare un comando come un altro utente, se non specifico che utente, si intende root, l'utente attuale deve far parte del gruppo **sudoers**, viene chiesta la password dell'utente corrente