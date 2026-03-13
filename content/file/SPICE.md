#uni 
Spice sta per Simulation Program with Integrated Circuit Emphasis, sviluppato dall'università Berkeley in California, nel 1972.

Imput testuale (NETLIST) -> Risolutore -> Output testuale

Ci sono poi versioni commerciali del kernel SPICE:
- PSSPICE
- LTSPICE
- HSPICE
Questi programmi offrono una interfaccia grafica:
Input grafico -> input testuale (NETLIST) -> Risolutore -> Output grafico (Probe)

In LTSPICE c'è solo un limite, la libreria standard non comprende componenti di altri produttori.
# Elaborazione
## Analisi statica
Soluzione di un sistema di equazioni non lineari: caratteristiche e punto di riposo.
## Analisi dinamica
Soluzione di un sistema di equazioni integro-differenziali lineare che diventa lineare nel dominio $s$: risposta in frequenza, FdT.
## Analisi in transitorio
Soluzione di un sistema di equazioni integro-differenziali non lineare. Computazionalmente gravoso.
## Presentazione dei risultati
- Tensione dei nodi
- Corrente nei rami
# Netlist
## Struttura della Netlist
- statement di apertura contenente il nome del circuito
- statement di descrizione della topologia del circuito
- direttive per specificare l'analisi da compiere
- direttive per specificare il formato dei dati in uscita
- direttiva di chiusura: `.END` 

- commenti preceduti da `*` 
### Statement di descrizione
Numerazione univoca dei nodi.
Il nodo di GND deve avere numero zero.
#### Resistenza
I nomi di resistenza devono partire con $R$:
```Netlist
Rs 1 2 1k
* resistenza chiamata Rs tra nodo 1 e nodo 2 con resistenza 1kOhm
* non avendo polarità l'ordine dei nodi non importa
```
#### Condensatore
```Netlist
Cout 2 0 1u
```
#### Generatore di tensione
```Netlist
Vs N+ N- DC valore
* generatore di tensione costante di valoreV
```
il primo nodo è il polo positivo, il secondo è quello negativo.
#### Generatore di corrente
```Netlist
Inome N+ N- DC valore
* corrente va da N+ a N-
```
#### Prefissi
- P: pico -12
- N: nano -9
- U: micro -6
- M: milli -3
- K: chilo 3
- MEG: mega 6
### Direttive (dot commands)
Le direttive cominciano con `.`
Direttive di analisi:
- `.OP ` determina punto di riposo
- `.AC [DEC] [OCT] [LIN] NP fstart fstop` 
- `.TRAN tstep tstop [start] [tmax] [UIC]` durata del transitorio: .TRAN 5ms
- `.IC` initial condition: `.IC V(OUT)=0.5` per condensatore per esempio

Direttive di uscita:
- `.PRINT type var1 var2`
