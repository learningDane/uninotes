#uni 
La prova pratica viene mantenuta per 5 appelli e per passare si necessita del 15.
Sito del corso: https://calcolatori.iet.unipi.it dove si trovano le slide.
Ricevimento Lunedì 15:30-17:30
Argomenti del corso:
1. Interruzioni
2. Protezione
3. Memoria virtuale
Questi compongo la multiprogrammazione

All'esame si può portare TUTTO, anche esami passati.
# Devcontainer
Per apple silicon prima riga di Dockerfile:
`FROM --platform=linux/amd64 mcr.microsoft.com/devcontainers/base:noble` 
```bash
apt update && apt install -y build-essential python3 python3-venv zlib1g-dev  \
		libgtk-3-dev libpulse-dev libpixman-1-dev libjson-xs-perl \
		ninja-build ncurses-dev git
apt update && apt install build-essential gcc g++
apt-get update && apt-get install -y gcc-x86-64-linux-gnu g++-x86-64-linux-gnu #gcc/g++/multilib non sono disponibili su arm
apt install make
wget https://calcolatori.iet.unipi.it/resources/libce-4.1.tar.gz
tar xvzf libce-4.1.tar.gz
```