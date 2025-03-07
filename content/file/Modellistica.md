#uni 
Partendo dagli _input_ e dagli _output_, come possiamo ricostruire la relazione che li lega?
Possiamo avere 4 approcci:
# Black Box
Questo è un approccio sperimentale (o induttivo).
![[blackbox1.svg]]
Il fitting consiste nel cercare una funzione matematica (modello) che dati gli input dia gli output che rende la "black box".
In [[MatLab]] la funzione `interp`, dati $u$ e $y$ rende la funzione
# White Box
Questo è un approccio Analitico (o deduttivo).
![[whitebox1.svg]]
# Gray Box
Questo è un mix tra i primi due, conosciamo il comportamento generale ma dobbiamo trovare gli specifici parametri.
# Approccio Pragmatico

![[approcciopgramatico1.svg]]
# Modello Macchina a Stati Finiti

![[macchinaastatifiniti1.svg]]
Questo è un modello molto potente per studiare il comportamento di sistemi, finché rimaniamo in numero di stati relativamente basso (<100).

Un sistema viene detto ==discreto== se il tempo è una variabile $k \in Z$, si parla quindi di stati.

Noi ci concentreremo su sistemi ==continui==, ovvero le variabili di stato si evolvono continuamente nel tempo, che è quindi una variabile $t \in R$.
I sistemi continui non sono macchine a stati finiti.

### Esempio: controllo del livello del serbatoio
Immaginiamo un sistema composto da un serbatoio, con uno scarico in fondo e con un'entrata in cima.
Chiamiamo $h$ il livello dell'acqua, $u(t)$ l'acqua in entrata e $A$ l'area della base del serbatoio.
Scegliamo infine l'uscita $y(t)$ del sistema pari al livello dell'acqua $h(t)$.
- Problema del controllo: mantenere costante il livello dell'acqua al valore desiderato $\overline{h}$.
- Segnale di riferimento (o ==set point==): $\dot{h(t)}= \overline{h}$, ovvero il valore desiderato in uscita.
- Azione di controllo: apertura/chiusura del rubinetto in entrata, ovvero regolazione di $u(t)$.
Calcoli:
$$
\begin{matrix}
\Delta V=A \cdot (h_{1}-h_{0})=\int_{t_{0}}^{t_{1}} u(\tau) d \tau \\
A \cdot \frac{dh}{dt}=u(t) \\
\text{chiamiamo} \quad x=h \to \frac{dx}{dt}=\dot{x}=\frac{1}{A} u(t)
\end{matrix}
$$
ed otteniamo così l'[[Equazioni Differenziali]] che risolve il nostro problema di controllo.
# Sistemi Lineari e Tempo Invarianti (LTI)

Tutti i sistemi lineari hanno le seguenti proprietà:
- ==omogeneità==: se si scala l'ingresso $u(t)$ allora l'uscita verrà scalata dello stesso fattore: $a\cdot u(t)= a \cdot y(t)$
- ==Sovrapposizione degli Effetti==: se un modello ha ha due risposte $y_{1}(t),y_{2}(t)$ a due ingressi $x_{1}(t),x_{2}(t)$, allora la risposta alla combinazione lineare di questi ingressi è data dalla combinazione lineare delle rispettive uscite: $\alpha_{1}x_{1}(t)+\alpha_{2}x_{2}(t)\implies \alpha_{1}y_{1}(t)+\alpha_{2}y_{2}(t)$

L'invarianza nel tempo vuol dire che:
- Il sistema si comporta in modo indipendente dal tempo: $x_{1}(t-\tau)\implies y_{1}(t-\tau)$
- Formalmente, nelle equazioni non c'è dipendenza esplicita dal tempo.

>"_Linear Systems are important because we can solve them_."
>__Richard Feynman

# Modello in Variabili di Stato
Questa è una rappresentazione __standard__ per rappresentare la dinamica di un sistema lineare.
- $x$: stato 
- $y$: uscita
- $u$: ingresso
$$
\begin{matrix}
\begin{cases}
\dot{x}=Ax+Bu \\
y=Cx+Du
\end{cases} \\
 \\
u \in R^r, \quad x \in R^n, \quad y \in R^m \\
A \in R^{n \times n}, \quad B \in R^{n \times r}, \quad C \in R ^{ m \times n}, \quad D \in R^{m \times r}
\end{matrix}
$$

Queste [[Matrici]] si chiamano "==Realizzazione di un sistema dinamico==" e ci permettono di misurare alcune proprietà strutturali del sistema:
- $A$ mette in evidenzia la proprietà di ==stabilità==. 
- La coppia $[A,B]$ mette in evidenzia la proprietà di ==controllabilità==.
- La coppia $[A,C]$ mette in evidenzia la proprietà di ==osservabilità==, ovvero la capacità di dedurre lo stato di $S$ a partire da $y \text{ e } u$.
La tempo invarianza è garantita dal fatto che le matrici non sono funzioni del tempo.

Le variabili di Stato ___sono il minimo insieme di variabili che descrive il sistema nella sua interezza___.
Questo modello permette di capire le relazioni tra le variabili di stato.

### Schema a blocchi del modello in Variabili di Stato

![[schemaablocchimodelloinvariabilidistato1.svg]]

- $\int = \frac{1}{S}$ 

### Esempio massa-molla-smorzatore

![[massamollasmorzatore.svg]]

$B$: attrito
- Variabili di Stato: __posizione__ e __velocità__: $x,v$ $\to$ $\large \begin{bmatrix} x \\ v\end{bmatrix}$ 
- Uscita: __posizione__: $x$

calcoli:
$$
\large
\begin{matrix}
F(t)=M\cdot \frac{dv}{dt} + Bv+Kx \\
\frac{dx}{dt}=v \\
\frac{dv}{dt}=- \frac{k}{M}x-\frac{B}{M}v+\frac{1}{M}F \\
 \\
\begin{cases}
\begin{bmatrix}
\dot{x} \\
\dot{v}
\end{bmatrix} = \begin{bmatrix}
\frac{dx}{dt} \\ \frac{dv}{dt} \end{bmatrix}= \begin{bmatrix}
0 & 1 \\ -\frac{k}{M} & -\frac{B}{M} \end{bmatrix} \begin{bmatrix}
x \\ v 
\end{bmatrix} +\begin{bmatrix}
0 \\ \frac{1}{M}
\end{bmatrix} F \\ \\

x=\begin{bmatrix}
1 & 0
\end{bmatrix} \begin{bmatrix}
x \\v
\end{bmatrix}+ \begin{bmatrix}
0
\end{bmatrix}F
\end{cases}
\end{matrix}
$$
# Sistemi non Lineari
Prendiamo per esempio la seguente forma non lineare:
$$
\large
\begin{cases}
\dot{x}=f(x,u) \\
y=g(x)
\end{cases}
$$
questa prende il nome di ==forma standard bilineare==.
Per ora non sappiamo come trattarla, a meno di fare ipotesi semplificative.
Cominciamo quindi a parlare di [[Equilibri e Stabilità]].