#uni 
La **trasformata di Laplace** è uno strumento matematico fondamentale nell’analisi dei sistemi dinamici, nelle equazioni differenziali e nel controllo automatico. Essa permette di trasformare equazioni differenziali nel **dominio del tempo** in equazioni algebriche nel **dominio della frequenza complessa**, facilitando la loro risoluzione.

Questa trasformata trova applicazioni in ingegneria, fisica e teoria dei segnali, rivelandosi uno strumento potente per lo studio dei sistemi lineari e la progettazione di circuiti elettrici e meccanici.
# Definizione

Formalmente, la trasformata di Laplace di una funzione $f(t)$, definita per $t \geq 0$, è data da:
$$  
F(s) = \mathcal{L} \{ f(t) \} = \int_0^{\infty} e^{-st} f(t) \, dt
$$
  
dove $s$ è un numero appartenente ai [[Numeri Immaginari (o Complessi)]] con parte reale sufficientemente grande affinché l’integrale converga.
# Applicabilità
La trasformata di Laplace è applicabile a tutte le funzioni che posseggono i seguenti requisiti:
- $f(t)$ definita sul semiasse reale positivo del piano complesso
- $f$ generalmente continua: può essere divisa in tratti in cui è continua e ammette limite destro e sinistro diversi (ovvero ammette ___salti___)
- $t \in R$ 
- $f$ di ordine esponenziale $\alpha$, ovvero: $\exists \alpha,M>0$ tale che per qualche $t_0>0$: $|f(t)| \leq M e^{\alpha t},t>0$
### Condizione Formale di Convergenza
Condizione Necessaria e Sufficiente di Convergenza dell'integrale della trasformata di Laplace:
$$
\int_0^{+\infty} |f(t)e^{-st}|dt<\infty, \quad \forall s\in I
$$
Notiamo che se l'integrale converge per un $S_0 \in C$, allora converge $\forall s \in C$ tali che:
$$
Re(s) > Re(S_0)
$$
con $S_0$ ___ascissa di convergenza___: il valore minimo della parte reale tale che l'integrale converga.
L'ascissa di convergenza separa il piano complesso in due parti, una nella quale converge, ed una nella quale non converge.
# Singolarità della trasformata di Laplace
Data $F(s)=\frac{N(s)}{D(s)}$:
- ___zeri del sistema dinamico___: le radici di $N(s)=0$
- ___poli del sistema dinamico___: le radici di $D(s)=0$ 
# Antitrasformata di Laplace
$$
f(t)= L^{-1}\{ F(s)\} = \frac{1}{2 \pi j} \int_{\gamma- \infty}^{\gamma+\infty} F(s)e^{st}ds
$$
Assumendo $f(t)=0, \forall t<0$.
### Procedimento attraverso la decomposizione in Fratti Semplici
1. Decompongo la funzione in fratti semplici:
$$
G(s)=\frac{n(s)}{d(s)}=\frac{n(s)}{\prod_i(s-p_i)^{h_i}}
$$
	dove $s_i$ è un ___polo___, con molteplicità $h_i$.
2. Scrivo $G(s)$ come somma di Residui Polari:
$$
G(s)=\sum_{i=1}\sum_{j=1}^{h_i}\frac{K_{ij}}{(s-p_i)^j}
$$
	dove $i$ è l'indice dei poli distinti e $j$ si riferisce alla molteplicità.
3. Calcolo i Residui:
$$
K_{ij}=\frac{1}{(h-j
)!}\lim_{s \to p_i}\frac{d^{h-j}}{ds^{h-j}}\Big[(s-p_i)^h \cdot G(s)\Big]
$$
4. Finalmente antitrasformiamo utilizzando la tabelle delle antitrasformate: 
$$
g(t)=\sum_{i=1}\sum_{j=1}^{h_i}K_{ij}\cdot t^{j-1}\cdot e^{p_i\cdot t}
$$
# Proprietà della Trasformata di Laplace
### Proprietà di Linearità
$$
L\{ c_1 \cdot f_1(t)+c_2 \cdot f_2(t) \}=c_1 \cdot F_1(s) + c_2 \cdot F_2(s)
$$
Ed inoltre l'ascissa di convergenza è il massimo tra le ascisse di convergenza dei termini originari.
### Proprietà della Traslazione di t
$$
L\{f(t-t_0)\}=e^{-st_o}F(s)
$$
### Proprietà di Scala
$$
L\{f(a \cdot t)\}=\frac{1}{a}\cdot F\Big(\frac{s}{a}\Big)
$$
### Proprietà di Derivazione in s
$$
L\{t \cdot f(t)\}=-\frac{dF(s)}{ds}
$$
### Proprietà di Traslazione in s
$$
F(s-a)=L\{ e^{at}ft)\}
$$
### Proprietà di Derivazione in t
$$
L\Big\{\frac{df}{dt}\Big\}=s\cdot F(s)-f(0)
$$
### Proprietà di Integrazione in t
$$
L \Big\{
\int_0^t f(t)dt
\Big\}=\frac{1}{s}F(s)
$$
### Proprietà di Convoluzione
$$
L\{f_1(t)*f_2(t)\}=F_1(s) \cdot F_2(s)
$$
Vedi [[Convoluzione]].
### Teorema Valore Iniziale
$$
\lim_{t \to 0}f(t)=\lim _{s \to \infty}s \cdot F(s)
$$
### Teorema Valore Finale
$$
\lim _{t \to \infty}f(t) = \lim_{s \to 0}s \cdot F(s)
$$
Condizione: $\lim_{t \to \infty} f(t)$ deve esistere ed essere finito (ovvero il sistema deve essere stabile, ma non marginalmente).
# Tabella delle Trasformate di Laplace
$$
\begin{array} {|c|c|} \hline   \text{nome}  & f(t) & F(s)  \\
\hline \text{Delta di Dirac} & \delta(t_0) & e^{-st_0}  \\
\hline \text{Funzione gradino} & 1(t) & \frac{1}{s}  \\
\hline \text{Rampa} & t & \frac{1}{s^2}\\ 
\hline \text{Gradino Traslato} & 1(t-t_0) & \frac{e^{-st_0}}{s}  \\
\hline \text{Funzione Esponenziale}  & k \cdot e^{at} & \frac{k}{s-a}  \\
\hline & k \cdot te^{at} & \frac{k}{(s-a)^2}\\
\hline \text{Esponenziale Irriducibile} & \frac{a \sqrt{d}\cos(\frac{\sqrt{d}}{\sqrt{c}}\cdot t)+b\sqrt{c}\sin(\frac{\sqrt{d}}{\sqrt{c}} \cdot t)} {c \sqrt{d}}  & \frac{s\cdot a+b}{c\cdot s^2+d} \\
\hline \text{seno} & \sin(wt+\phi) & \frac{w\cdot \cos \phi+s\cdot\sin \phi}{s^2+w^2} \\
\hline \text{coseno} & \cos(wt+\phi) & \frac{s \cdot\cos \phi+w\cdot \sin \phi}{s^2+w^2} \\
\hline
\end{array} 
$$