#uni 

>Diodo:
>![[Diodo.svg]]

Un diodo è l'applicazione più semplice della [[Giunzione PN]]. È un dispositivo che funziona da valvola per la corrente: se vi applichiamo tensione in polarizzazione diretta la corrente che vi scorre aumenta esponenzialmente secondo la [[Legge di Shockley]], in polarizzazione inversa la corrente che vi scorre invece è solamente la corrente inversa di saturazione, che è trascurabile:

![[Legge di Shockley]]

Va notato però che per correnti $I_D$ molto grandi si raggiunge una sorta di saturazione, noi però questo fenomeno non lo studiamo.

Ad un diodo è anche possibile associare una Capacità, ma di solito è un valore trascurabile, sopratutto se utilizzato in bassa frequenza.

Esempio di datasheet di un diodo: `1N4148 PHILIPS | Alldatasheet`.
# Breakdown
Se analizziamo il valore della corrente $I_D$ a tensioni $V_D$ che si aggirano attorno per esempio ai $-70\text V$ (quindi in polarizzazione inversa) notiamo il verificarsi di una rapida discesa della corrente (esponenziale):
![[breakdown.svg]]
Due fenomeni fisici diversi contribuiscono al Breakdown, questi però entrano in azione generalmente a tensioni diverse, si può dire che quello che entra in effetto per $|V_D|$ minore "vince" e causa il breakdown prima dell'altro.

Il fenomeno di breakdown di per se non causa danni permanenti, tuttavia se la corrente $I_D$ supera certi valori (che dipendono dallo specifico diodo utilizzato) il diodo non riesce a dissipare abbastanza energia e si brucia.

Per questo motivo di solito mettiamo una resistenza in serie per limitare la quantità di corrente.
## Effetto Valanga
Questo effetto, che si verifica di solito $|V_D |= |V_{BR}| > 7\text V$, si verifica quando le cariche libere (sia elettroni sia lacune, anche se è più difficile da spiegare), tra un urto e l'altro riescono ad accumulare abbastanza energia da rompere il legame della carica colpita al prossimo urto (questo fenomeno prende il nome di **Ionizzazione per Urto**), causando una reazione *a valanga*.


## Effetto Zener
Questo effetto, che si verifica di solito a $|V_D |= |V_{BR}| < 5\text V$, si verifica quando il campo elettrico interno al diodo diventa abbastanza forte da rompere i legami covalenti, causando un aumento del potenziale built-in e del campo elettrico stesso, causando un aumento esponenziale di corrente (diretta da catodo a anodo).
### Diodi Zener

> Diodo Zener: 
> ![[diodo_zener.svg]]

Un diodo zener è un diodo con livelli di [[Drogaggio]] molto più grandi di un diodo normale, sia nella zona P sia nella zona N. 

Questo aumento, causa un aumento delle cariche libere e quindi un rimpicciolimento della zona di svuotamento ([[Giunzione PN#Valore di W la dimensione della zona di svuotamento]]), il campo elettrico $E=\frac{V}{W}$ quindi aumenta velocemente, aumentando l'effetto zener e abbassando il valore di tensione inversa applicata a cui si verifica il breakdown.

Durante la produzione di questi diodi è possibile tarare $V_{\text{BR}}$ ad un livello desiderato, questo permette di utilizzare i diodi zener per generare tensioni di riferimento poiché, una volta raggiunto il breakdown, grandi cambiamento della corrente in entrata causano insignificanti cambiamenti nella tensione $V_D$, a causa dell'alta inclinazione del grafico $I_D(V_D)$.

L'effetto zener è una applicazione pratica del fenomeno del [[Tunneling Quantistico]]: a causa del forte campo elettrico, gli elettroni riescono a passare dalla banda di valenza alla banda di conduzione attraverso la stretta barriera di potenziale della giunzione.

> I diodi zener sono anche più stretti dei diodi normali, a quanto pare questo aumenta la probabilità del verificarsi del tunneling quantistico.

## Effetto della Temperatura sul Breakdown
**Se $T$ aumenta**:
- **L'effetto zener aumenta**: $E=\frac{V}{W}=\frac{V_0-V}{W}=\frac{-V+\frac{K_B \cdot T}{q}\ln(\frac{N_A \cdot N_D}{n_i^2})}{W}$ quindi all'aumentare della temperatura il campo elettrico aumenta: $|V_\text{BR}|$ diminuisce.
- **L'effetto Valanga diminuisce**: Temperature più alte portano a maggiore mobilità, ovvero più urti, le cariche libere non riescono quindi tra un urto e l'altro a raggiungere la quantità necessaria di energia per rompere legami covalenti: $|V_\text{BR}|$ aumenta.
### Diodi Zener a coefficiente di Temperatura compensato
Dentro la famiglia dei diodi zener esistono diodi costruiti in maniera da diminuire gli effetti del cambiamento della temperatura, precisamente attorno al punto di rottura (breakdown).

Per esempio se vogliamo fare un diodo che abbiamo una tensione di rottura $V_\text{BR}$ di $-6\text V$ e che sia indifferente (quanto possibile) attorno a questo range creiamo un diodo che abbia $V_\text{BR,zener} \approx - 5\text V$ e $V_\text{BR,cascata} \approx - 7\text V$, in questo modo attorno a $V=-6 \text V$ abbiamo una buona resistenza ai cambiamenti di temperatura, poiché i due trend di effetto zener e cascata si combattono a vicenda.
# Risoluzione di Circuiti con Diodi
Poiché il diodo non è un dispositivo lineare, gli strumenti che possiamo utilizzare per risolvere i circuiti secondo il ==metodo numerico== si limita alle leggi di Kirchoff ([[Prima Legge di Kirchkoff]],[[Seconda Legge di Kirchkoff]]).

Possiamo utilizzare il ==metodo grafico==, ma ha alcuni sconvenienti:
- è praticamente utilizzabile solo nel caso di un Diodo solo nel cicuito
- necessita la conoscenza dei parametri del Diodo
- anche se due Diodi sono nominalmente identici i valori effettivi possono variare anche notevolmente
- realisticamente parlando è una approssimazione poiché dipende dal livello di precisione utilizzato.

Entrambi questi metodi sono quindi spesso non viabili, vediamo allora metodi che includono una approssimazione lineare del Diodo:

L'idea generale è approssimare il Diodo linearmente, i metodo variano per il metodo di approssimazione. Dividono il dominio della risposta alla tensione applicata del Diodo (la tensione $V_D$) in due: 
- $V_D < V_\gamma$
- $V_D \geq V_\gamma$ 
Ad ognuna di queste due parti associamo un comportamento diverso del Diodo e quindi un diverso dispositivo con cui deve essere sostituito nel nostro circuito.

Poi dobbiamo effettuare una ipotesi: il Diodo **conduce** (**ON**) o **non conduce** (**OFF**)? Ovvero nel nostro circuito, nel diodo scorre corrente?
- se ipotizziamo Diodo OFF rimpiazziamo il Diodo con il componente associato a $V_D < V_\gamma$ 
- se ipotizziamo Diodo ON rimpiazziamo il Diodo con il componente associato a $V_D \geq V_\gamma$ 

Una volta effettuata la sostituzione risolviamo il circuito risultante, che è lineare.

Una volta risolto dobbiamo controllare che l'ipotesi fatta in partenza si sia rivelata corretta (*ipotesi consistente*), se non lo è dobbiamo sostituire il Diodo con il componente associato all'ipotesi contraria e ricominciare con la risoluzione del circuito, con la certezza però di avere stavolta fatto l'ipotesi corretta (Se non è zuppa è pan bagnato).

Vediamo i diversi modelli di linearizzazione utilizzabili:
## Modello a caduta Costante
$$
\begin{matrix}
V_D \lt V_\gamma & I_D=0\text A & \text{circuito aperto}
\\
V_D \geq V_\gamma & V_D=V_\gamma\text V &\text{gen. di tensione}
\end{matrix}
$$
![[modello_caduta_costante.svg]]
## Modello del Diodo Ideale
$$
\begin{matrix}
V_D \lt 0 & I_D=0\text A & \text{circuito aperto}
\\
V_D \geq 0 &V_D=0 \text V&\text{corcocircuito}
\end{matrix}
$$
![[modello_diodo_ideale.svg]]
Se so che le tensioni in gioco nel circuito sono molto maggiori di $0.7 \text V$ questo metodo è all'incirca preciso quanto il modello a caduta costante, ma è molto più veloce da computare.
## Modello Lineare a tratti
$$
\begin{matrix}
V_D \lt V_\gamma & I_D=0\text A & \text{circuito aperto}
\\
V_D \geq V_\gamma & I_D=\frac{V_D}{R_D} &\text{Resistenza} R_D + \text{gen. Tensione} V_\gamma
\end{matrix}
$$
![[modello_lineare_a_tratti.svg]]
