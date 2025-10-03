#uni 
La macchian virtuale che useremo durante il corso di [[Calcolatori Elettronici]] è una macchina "nuda" (senza altro software) che useremo per emulare un computer PC AT della IBM (processore [[Intel 80286]]), il personal computer d'eccellenza.

Questa macchina diventò così famosa perché venne clonata per intero in numero spropositati, poiché IBM (come tutti gli altri manufacturer all'epoca) rilasciò tutta la documentazione sulla costruzione del PC AT, che rese facile la realizzazione di perfetti cloni a costi minimi rispetto all'originale.

Proprio il successo di questo computer portò alla realizzazione dello standard ISA, che viene rispettato anche oggi.
# Periferiche
Insieme al computer la nostra macchina virtuale rende disponibile alcune periferiche, identiche a quelle che venivano fornite insieme al PC AT ai tempi.
Tra queste troviamo: tastiera, video VGA e hard disk.
### Tastiera
L'interfaccia per la tastiera fornita nella macchina è una semplice interfaccia a controllo di programma:
![[interfacciatastiera.svg]]
La tastiera non fa altro che comunicare quando un tasto (il numero identificativo del tasto fisico, non la codifica [[ascii]] del carattere) viene premuto oppure rilasciato.

L'unica cosa gestita dalla tastiera stessa è la ripetizione: dopo tot tempo che un tasto rimane premuto la tastiera comincia a mandare impulsi di premuta del tasto ripetutamente.

La tastiera migliaia di volte al secondo controlla quali tasti sono premuti e da questa informazione comunica di conseguenza con l'interfaccia.

Il registro TBR serve per comunicare alla tastiera parametri come il delay prima di ripetizione, LED di stato eccetera.