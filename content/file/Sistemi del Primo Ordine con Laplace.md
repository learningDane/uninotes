#uni 
Supponiamo di aver risolto un sistema fisico, otteniamo quindi una [equazione differenziale](Equazioni%20Differenziali.md) del primo ordine, con condizioni iniziali nulle:
$$
a_1\frac{dy}{dt}+a_0y=b_0u \quad , \quad y(0)=0
$$
Utilizziamo la [[Trasformata di Laplace]] per risolverla e quindi trasformiamo:
$$
a_1 \cdot s \cdot Y(s) + a_0 \cdot Y(s)=b \cdot U(s)
$$
e calcoliamo la [[Funzione di Trasferimento]]:
$$
G(s)=\frac{Y(s)}{U(s)}=\frac{b}{a_o+a_1 \cdot s}
$$

Calcoliamo la ___risposta al gradino___ ($U(s)=\frac{1}{s}$) di questa funzione:
$$
y(t)=L^{-1}\Big\{  \frac{1}{s}G(s) \Big\}=L^{-1} \Big\{ \frac{b_0/a_1 } {s^2+s \cdot a_0 /a_1}\Big\}
$$
Questa è la ___Forma di Evans___, ovvero portiamo il denominatore ad essere ___monadico___.

Date le condizioni iniziali sappiamo che $y(0)=0$, per quanto riguarda il ___valore a regime___ possiamo applicare il teorema del valore finale ed otteniamo $\lim_{t \to \infty}y(t)=\frac{b_0}{a_0}$.

Per calcolare il ___transitorio___ dobbiamo invece risolvere $y(t)$:
$$
\begin{matrix}
Y(s)= \frac{b_0/a_1 } {s^2+s \cdot a_0 /a_1}=\frac{A}{s}+\frac{B}{s+a_0/a_1} \\
A=...=\frac{b_0}{a_0}=G(0) \\
B=...=\frac{-b_0}{a_0}=-G(0) \\
y(t)=\frac{b_0}{a_0}(1-e^{-\frac{a_0}{a_1}t})\cdot1(t)=G(0)\cdot(1-e^{-\frac{t}{T}})\cdot1(t)
\end{matrix}
$$

>Curva della funzione per $T=1$, notiamo il valore per $y(T)=0,63 \cdot G(0)$:
>![[rispostasistemaprimoordine.svg]]

Definiamo il ___tempo di assestamento___ al valore $i\%$: il tempo che un sistema dinamico impiega per raggiungere (e poi mantenere) un valore in una fascia di $\pm i \%$ intorno al valore di regime (il guadagno statico $G_0$).
# Caso in cui compare anche la derivata dell'ingresso
$$
a_1\frac{dy}{dt}+a_0y=b_1\frac{du}{dt}+b_0u \quad , \quad y(0)=0
$$
con [[Funzione di Trasferimento]]:
$$
\begin{matrix}
G(s)=\frac{Y(s)}{U(s)}=\frac{b_0+b_1\cdot s}{a_o+a_1 \cdot s} \\
\text{Forma di Bode} \small\text{ (mette in evidenza le costanti di tempo)}: \\
 \quad G(S)=\frac{b_0}{a_0} \cdot \frac{1+s \cdot\frac{b_1}{b_0}}{1+s \cdot \frac{a_1}{a_0}}=G(0) \cdot \frac{1+s \cdot \tau_z}{1+s \cdot \tau} \\
\text{ Forma di Evans} \small \text{ (evidenzia le singolarità dinamica del sistema, ovvero poli e zeri)} : \\
 G(S)=\frac{b_1}{a_1} \frac{s+\frac{b_0}{b_1}}{s+ \frac{a_0}{a_1}}
\end{matrix}
$$
