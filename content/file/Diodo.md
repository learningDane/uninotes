#uni 

>Diodo:
>![[Diodo.svg]]

Un diodo è l'applicazione più semplice della [[Giunzione PN]]. È un dispositivo che funziona da valvola per la corrente: se vi applichiamo tensione in polarizzazione diretta la corrente che vi scorre aumenta esponenzialmente secondo la [[Legge di Shockley]], in polarizzazione inversa la corrente che vi scorre invece è solamente la corrente inversa di saturazione, che è trascurabile:

![[Legge di Shockley]]


# Breakdown
Se analizziamo il valore della corrente $I_D$ a tensioni $V_D$ che si aggirano attorno per esempio ai $-70\text V$ (quindi in polarizzazione inversa) notiamo il verificarsi di una rapida discesa della corrente (esponenziale):
![[breakdown.svg]]

# Risoluzione di Circuiti con Diodi
Poiché il diodo non è un dispositivo lineare, gli strumenti che possiamo utilizzare per risolvere i circuiti secondo il ==metodo numerico== si limita alle leggi di Kirchoff ([[Prima Legge di Kirchkoff]],[[Seconda Legge di Kirchkoff]]).

Possiamo utilizzare il ==metodo grafico==, ma ha alcuni sconvenienti:
- è praticamente utilizzabile solo nel caso di un Diodo solo nel cicuito
- necessita la conoscenza dei parametri del Diodo
- anche se due Diodi sono nominalmente identici i valori effettivi possono variare anche notevolmente
- realisticamente parlando è una approssimazione poiché dipende dal livello di precisione utilizzato.

Entrambi questi metodi sono quindi spesso non viabili, vediamo allora metodi che includono una approssimazione lineare del Diodo:

L'idea generale è approssimare il Diodo linearmente, i metodo variano per il metodo di approssimazione. Dividono il dominio della risposta alla tensione applicata del Diodo (la tensione $V_D$) in due: 
- $V_D < V_k$
- $V_D \geq V_k$ 
Ad ognuna di queste due parti associamo un comportamento diverso del Diodo e quindi un diverso dispositivo con cui deve essere sostituito nel nostro circuito.

Poi dobbiamo effettuare una ipotesi: il Diodo è ON o OFF? Ovvero nel nostro circuito, nel diodo scorre corrente?
- se ipotizziamo Diodo OFF rimpiazziamo il Diodo con il componente associato a $V_D < V_k$ 
- se ipotizziamo Diodo ON rimpiazziamo il Diodo con il componente associato a $V_D \geq V_k$ 

Una volta effettuata la sostituzione risolviamo il circuito risultante, che è lineare.

Una volta risolto dobbiamo controllare che l'ipotesi fatta in partenza si sia rivelata corretta, se non lo è dobbiamo sostituire il Diodo con il componente associato all'ipotesi contraria e ricominciare con la risoluzione del circuito, con la certezza però di avere stavolta fatto l'ipotesi corretta (Se non è zuppa è pan bagnato).

Vediamo i diversi modelli di linearizzazione utilizzabili:
## Modello
$$
\begin{matrix}
V_D \lt V_k & a & \text{circuito aperto}
\\
V_D \geq V_k &a&\text{gen. di tensione}
\end{matrix}
$$
## Modello 2
## Modello Linearizzato