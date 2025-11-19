#uni 
Applicazione distribuita
Peer to Peer

lavagna: To Do - Doing - Done
card: identifica specifica task da portare a compimento

La lavagna ("server") è raggiungibile alla porta 5678

Lavagna:
- ID
- colonne
- card

Card:
- ID
- colonna
- Testo Attività
- Utente (porta) che la implementa (doing) e implementata (done)
- timestamp ultima modifica

Gli utenti (almeno 4) sono identificati dal numero di porta: porte incrementali a partire dalla 5679.
La prima operazione che un utente deve eseguire è comunicare con la lavagna, rappresenta la registrazione.

673712 pari: dopo registrazione la cosa cambia: tutti gli utenti vengono notificati delle card toDo. Gli utenti decidono chi fa una attività (ALGORITMO DEL CONSENSO). Una volta scelto, un utente comunica alla lavagna quale card si prende, e la lavagna la sposta in doing. Quando l'utente ha finito lo dice alla lavagna e questa la sposta in Done.

Comandi:
- HELLO: registrazione. Lavagna segna porta e aumenta counter
- QUIT
- MOVE_CARD: eseguito dalla lavagna
- CREATE_CARD:
- SHOW_LAVAGNA: 
- SEND_USER_LIST: lavagna manda liste delle porte degli utenti
- PING_USER: per le card in DOING da troppo tempo, lavagna manda il ping, se utente non risponde, la task viene messa in TODO
- PONG_LAVAGNA: utente risponde al ping
comandi pari:
- AVAILABLE_CARD: lavagna (se c'è più di un utente registrato) invia a tutti utenti connessi tutte le card in TODO, inoltre invia la lista delle porte degli utenti presenti (escluso il destinatario) e il numero di utenti presenti
- CHOOSE_USER
- ACK_CARD
- CARD_DONE: utente comunica terminazione
- CHOOSE_USER: messaggio che si scambiano gli utenti, associando un costo all'esecuzione dell'attività della card correntemente assegnata, gli utenti convergeranno nell'assegnare la card all'utente che ha il costo minore. Una volta che sono stati ricevuti tutti i costi (numero costi inviati = numero utenti connessi) si sceglie utente con costo minore. Se c'è parità si sceglie quello con porta minore. *Utente con costo minore si rende conto che ha il costo minore, quindi sa che è stata assegnata a lui la card*.
- ACK_CARD: utente al quale è assegnata la card lo comunica alla lavagna
- CARD_DONE: utente comunica la fine attività.
# Specifiche di consegna
Documentazione di massimo due pagine. Deve includere le operazioni per compilare. NON CI DEVONO ESSERE WARNING (compilare con -Wall). Anche Makefile volendo.

```bash
./lavagna
```
Ad ogni spostamento di una card aggiorna la visualizzazione della lavagna (SHOW_LAVAGNA).