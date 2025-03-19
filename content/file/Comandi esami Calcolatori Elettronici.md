#uni 
# Esercizi Assembler
Scrivete il file **es1.s** con il vostro editor preferito, oppure con emacs. Il comando per assemblare e collegare il primo esercizio è:
```bash
g++ -o es1 -fno-elide-constructors es1.s prova1.cpp
```
Per confrontare output:
```shell
./es1 | diff - es1.out
```
### Debug
Aggiungendo l'opzione **-g** al comando **g++** verranno aggiunte le informazioni di debug negli eseguibili.
# Esercizi Nucleo