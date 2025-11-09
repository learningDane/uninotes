#uni 
# LIBCE
```bash
brew install make x86_64-elf-gcc x86_64-elf-gdb wget
	#GNU "make" has been installed as "gmake".
	#If you need to use it as "make", you can add a "gnubin" directory
	#to your PATH from your bashrc like:
	#PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"
wget https://calcolatori.iet.unipi.it/resources/libce-4.3.tar.gz
tar xvzf libce-4.3.tar.gz
cd libce-4.3
make
make install
	#==> Creo '/Users/davidesqueri/CE/share/hd.img' (dimensione: 20M)
	#==> Installo libce.conf in '/Users/davidesqueri/CE/etc'
	#==> Installo libce64.a e libce-debug.py in '/Users/davidesqueri/CE/lib64/ce'
	#==> Installo i file .h in '/Users/davidesqueri/CE/include/ce'
	#==> Installo boot.bin e boot.ld in '/Users/davidesqueri/CE/lib/ce'
	#==> Installo gli script in '/Users/davidesqueri/CE/bin'
echo $HOME/CE/bin | sudo tee -a /etc/paths
	#aggiunge boot compile e debug al path
```
# QEMU
```bash
python3 -m pip install tomli
brew install coreutils
echo 'export PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"' >> ~/.zshrc
# poi ricaricare la shell:
source ~/.zshrc
brew install ninja pkg-config sphinx-doc glib
wget https://calcolatori.iet.unipi.it/resources/qemu-ce-9.2.2-3.tar.gz
tar xvf qemu-ce-9.2.2-3.tar.gz
cd qemu-ce-9.2.2-3
./install
```
# Nucleo
```bash
# scaricare cartella dove volete
# scompattare:
tar xvf nucleo-8.3.tar.gz
```

> informazioni sull'uso di [[LIBCE]], esempiIO e nucleo: [[Comandi Utili Calcolatori Elettronici]]

# ESERCIZI DI TRADUZIONE C++ - ASM
Gli esercizi di traduzione possono essere tranquillamente compilati ed eseguiti tramite `compile` e `boot`, con l'unico neo che in questi esercizi il professor Lettieri utilizza spesso e volentieri la libreria `iostream`, o altre librerie che non sono presenti nella macchina virtuale qemu e che quindi non possono essere utilizzate.

> La soluzione semplice ma non definitiva è rimuovere ogni libreria non utilizzabile dentro qemu, per esempio rimpiazzando `#include <iostream>` con `#include "libce.h"` e invece di utilizzare `std::cout` eccetera, utilizzare `flog`, della libreria [[LIBCE]].

La soluzione che ho deciso di adottare è creare un container docker (ho una installazione [[docker]]+colima per rimanere minimal, quindi niente docker desktop) che emuli un sistema ubuntu x86_64, con il necessario per compilare gli esercizi di traduzione e il necessario per far funzionare lo script `scarica-esame`, tutto dichiarato via Dockerfile. 
Invece di creare un nuovo container ad ogni avvio, il primo `docker run` condivide la cartella corrente con il container, in modo da poter scrivere il codice su macchina (Zed/VSCODE/vim/ecc) ed compilarlo ed eseguirlo nel container, inoltre il `docker run` da il nome desiderato al container in modo da poterlo facilmente utilizzare con `docker start -ai nomeContainer`.
Questa soluzione è leggera (docker+colima è molto più leggero di docker desktop) e facile da usare.
## Setup
### Dockerfile
```Dockerfile
# Usa immagine Linux x86_64 (emulata su ARM via QEMU)
FROM --platform=linux/amd64 ubuntu:22.04

# Installa compilatori e strumenti di base
RUN apt update
RUN apt upgrade -y
RUN apt install -y build-essential gdb
# strumenti per lo script scarica-esame:
RUN apt install -y curl wget

# Imposta la directory di lavoro
WORKDIR /workspace
```
### comandi
```shell
# costruisci l'immagine
docker build -t linux-x86-env .

# avvia, con montaggio della cartella
docker run --platform linux/amd64 \
	--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
	-it \
    -v $(pwd):/workspace \
    --name containerCE \
    linux-x86-env
    
	# per uscire dal container
	exit
    
    # dopo averlo avviato una prima volta, per farlo ripartire:
    docker start -ai containerCE
    
    # dentro docker
    g++ -fno-elide-constructors prova1.cpp es1.s -o exec
    ./exec
    ./exec | diff - es1.out
```
### scarica esame
Chiamare il file scarica-esame e metterlo in /usr/local/bin/ (o comunque aggiungerlo al PATH).
```sh
#!/bin/sh

set -e

PAGINA_APPELLI="https://calcolatori.iet.unipi.it/appelli2.php?tag=c2as_qemu-v8"
VERSIONE=08
WORKSPACE="${ROOT_ESAMI_CE:-/workspace}"

NC='\033[0m'

RED='\033[0;31m'
BLUE='\033[0;34m'
GREEN='\033[0;32m'

if [ -z "$1" ]; then
  printf "scarica-esame list         mostra tutte le date disponibili per il download\n"
  printf "scarica-esame yyyy-mm-dd   scarica l'esame della data yyyy-mm-dd\n"
  exit 1
fi

DATE_APPELLI=$(curl -s "$PAGINA_APPELLI" | grep -o "value='[0-9_-]*'" | sed "s/value='\([0-9_-]*\)'/\1/")

if [ "$1" = "list" ]; then
    printf "Date disponibili:\n"
    for date in $DATE_APPELLI; do
        if [ -d "$WORKSPACE/$date" ]; then
            printf "$GREEN${date%_*}: Esame già scaricato $NC\n"
        else
            printf "$BLUE${date%_*}: Esame disponibile per il download $NC\n"
        fi
    done

else
    DATE_LIST=$(printf "$DATE_APPELLI" | sed "s/_$VERSIONE//g")
    if printf "$DATE_LIST" | grep -q "^$1$"; then
        if [ -d "$WORKSPACE/${1}_${VERSIONE}" ]; then
            printf "$RED Esame già scaricato $NC\n"
            exit 1
        fi
        uri="https://calcolatori.iet.unipi.it/appelli_download.php?data0=${1}_${VERSIONE}"
        tmp=$(mktemp -d)

        wget $uri -O $tmp/esame.tar.gz
        tar -xzvf $tmp/esame.tar.gz -C $WORKSPACE
        printf "$GREEN Esame scaricato correttamente $NC\n"
    else
        printf "$RED Esame non disponibile $NC\n"
        exit 1
    fi
fi

```