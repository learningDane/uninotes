#uni 
Poiché come abbiamo detto un Calcolatore non ha a disposizione l'astrazione delle infinite cifre sappiamo di avere bisogno di arrotondamento, a monte e a valle ([[Numeri di Macchina]],[[Rappresentazione in Virgola Mobile]]).

Quello che si fa su un calcolatore infatti è approssimare i dati ed approssimare il risultato dell'operazione se questo non rientra in $F(\beta,mL,U)$.
Eg. $x+y \to x \oplus y=Rn(x+y)$.

Così facendo ovviamente introduciamo ___errori___.

Studiamo quindi ora come calcolare l'errore durante il calcolo di una [[Funzione Razionale]] $f:\mathbb{R}^n \rightarrow \mathbb{R}$ nel punto$P_{0}=(x^{(0)}_{1},x^{(0)}_{2},\ldots,x^{(0)}_{n})\in\mathbb{R}^n$ dove le $x$ sono componenti del punto in $n$ dimensioni.
# Fonti dell'Errore
1. $P_{0}$ potrebbe non appartenere a $F(\beta,m,L,U)$ quindi viene approssimato, componente per componente, con $RN(P_{0})=P_{1}$.
2. $\tilde{f}$ viene "tradotta" in una funzione $f_{a}$ in __aritmetica floating point__, quindi in un polinomio che coinvolge operazioni floating point ($\oplus,\ominus,\odot,\oslash$).

In sostanza noi vorremmo calcolare $f(P_{0})$ ma in realtà calcoliamo $f_{a}(P_{1})$
##### Esempio
calcoliamo $e^\pi$:
1. approssimiamo con [[Formula di Taylor]]: $e^x\approx 1+x+\frac{x^2}{2}=\tilde{f}(x)$  (vedi [[Errori nelle Funzioni Non Razionali]])
2. $RN(\pi)=3,1415=P_{1}$
3. "traduco" $\tilde{f}_{a}(P_{1})=1\oplus (P_{1}((P_{1}\odot P_{1})\oslash 2))$ 
# Errore Totale
data $f:\mathbb{R}^n \rightarrow \mathbb{R},\quad P_{0}\in\mathbb{R}^n$ e un algoritmo: l'Errore Totale è dato da $$
\begin{matrix} \\
\large
\delta_{f}=\tilde{f}_{a}(P_{1})-f(P_{0}) \\ \text{con}\quad P_{1}=Rn(P_{0})
\end{matrix}$$
# Errori Algoritmico e Inerente

L'__Errore Assoluto Totale__ ($\delta_{f}$) è definito come:$$\large \delta_{f}=\tilde{f}_{a}(P_{1})-f(P_{0})=\underbrace{\tilde{f}_{a}(P_{1})-f(P_{1})}_{\delta_{a}}+\underbrace{f(P_{1})-f(P_{0})}_{\delta_{d}}=\delta _{a}+\delta_{d}$$
$\delta_{a}$ = __Errore Assoluto Algoritmico__ 
$\delta_{d}$ = __Errore Assoluto Inerente__ (ai dati)

Allo stesso modo definiamo l'__Errore Relativo Totale__ ($\epsilon_{f}$), ricordandoci che $\epsilon=\frac{\delta}{f(P_{0})}$ :$$\large \begin{matrix}\epsilon_{f}=\frac{\delta_{f}}{f(P_{0})}=\frac{f_{a}(P_{1})-f(P_{0})}{f(P_{0})}=\frac{f_{a}(P_{1})-f(P_{1})}{f(P_{0})}+\underbrace{\frac{f(P_{1})-f(P_{0})}{f(P_{0})}}_{\epsilon_{d}}=\\= \frac{f_{a}(P_{1})-f(P_{1})}{f(P_{1})}\cdot \frac{f(P_{1})}{f(P_{0})}+\epsilon_{d} =\epsilon_{a}\cdot(1+\frac{f(P_{1})-f(P_{0})}{f(P_{0})})+\epsilon_{d}=\\= \epsilon_{a}\cdot(1+\epsilon_{d})+\epsilon_{d}=\epsilon_{a}+\epsilon_{d}+\underbrace{\epsilon_{a}\epsilon_{d}}_{\ll\min\{\epsilon_{a},\epsilon_{d}\}}=\epsilon_{a}+\epsilon_{d} \end{matrix}$$
$\epsilon_{a}$ = __Errore Relativo Algoritmico__
$\epsilon_{d}$ = __Errore Relativo Inerente__

__Tips__: i termini di grado superiore al primo durante un calcolo di errori li elimino perché significherebbe avere un errore irrilevante rispetto agli altri termini.

In generale per limitare $|\delta_{f}|$ si cercheranno disuguaglianze del tipo:$$|\delta_{a}|<\tau_{1},\quad |\delta_{d}|<\tau_{2}\Longrightarrow|\delta_{f}|<\tau_{1}+\tau_{2}$$
# Errore Inerente
- Assoluto: $f(P_{1})-f(P_{0})$ 
- Relativo: $\large \frac{f(P_{1})-f(P_{0})}{f(P_{0})}$ 
Possiamo definirlo anche così:
- Assoluto$$ \begin{matrix}
\large \delta_{d}=f(P_{1})-f(P_{0})=\sum^m_{j=1}\underbrace{\frac{\partial f}{\partial x_{j}}(P_{0})}_{A_{j}}\cdot \delta_{j}= \sum_{j=1}^mA_{j} \cdot \delta_{j}
\\ \text{con} \quad \\
\delta_{x_{j}}:=x^{(1)}_{j}-x^{(0)}_{j}=x_{j}^{(0)} \cdot U \\
A_{j}=\text{Coefficienti di Amplificazione dell'errore assoluto}=\frac{\partial f}{\partial x_{j}}(P_{0}) \\
\text{calcolato come} \quad |A_j|=\sup_{x_{j}\in D}|\frac{\partial f}{\partial x_{j}}(x)|
\end{matrix}$$
- Relativo$$\large \epsilon_{d}=\frac{\delta_{d}}{f(P_{0})}=\frac{\sum^m_{j=1}\frac{\partial f}{\partial x_{j}}(P_{0})\cdot \delta_{j}}{f(P_{0})} =\sum^n_{j=1}\underbrace{\frac{\partial f}{\partial x_{j}}(P_{0})\cdot \frac{x^{(0)}_{j}}{f(P_{0})}}_{\rho_{j}} \cdot \underbrace{\frac{x^{(1)}_{j}-x^{(0)}_{j}}{x^{(0)}_{j}}}_{\epsilon_{j}} =\sum_{{j=1}}^m \rho_{j}\cdot \epsilon_{j}$$
$\rho_{j}$= Coefficiente di Amplificazione dell'errore Relativo, definisce 2 classi di problemi:
- __Malcondizionati__ (almeno un $|\rho_{j}|$ grande)
- __Bencondizionati__ ($|\rho_{j}|\approx 1\quad\forall j$ ovvero se $\epsilon_{d}$ è di un ordine di grandezza comparabile a $max|\epsilon_{i}| \quad con \quad i=1,\ldots,m$)
# Errore Algoritmico
Consideriamo subito gli errori inerenti alle 4 operazioni in aritmetica floating point:
$$
\large
\begin{array} 
{|c|c|} \hline
\text{operazione}  & \delta_{d} & \epsilon_{d} \\
\hline x \oplus y & \delta_{x}+\delta_{y} & \frac{x}{x+y}\epsilon_{x}+\frac{y}{x+y}\epsilon_{y} \\
\hline x \ominus y & \delta_{x}-\delta_{y} & \frac{x}{x-y}\epsilon_{x}-\frac{y}{x-y}\epsilon_{y} \\
\hline x \otimes y & y\cdot\delta_{x}+x\cdot\delta_{y}  & \epsilon_x+\epsilon y \\
\hline x \oslash y & \frac{1}{y}\cdot \delta_{x}+\frac{\delta x}{y^2}\cdot \delta_y & \epsilon_x-\epsilon y  \\
\hline
\end{array}
$$
- ___cancellazione numerica___: quando sottraggo (o sommo a segni alterni) numeri molto simili in modulo (stesso esponente e prime cifre della mantissa uguali), di cui almeno uno soggetto ad errori di approssimazione, otteniamo una perdita di cifre significative.
  Questo per via del divisore nel calcolo dell'errore assoluto di somma e sottrazione.
- se $\large \epsilon_a$ è "piccolo" il __metodo numerico__ (o algoritmo) è ==stabile==.
### Calcolo dell'errore Algoritmico
Algoritmi diversi per la stessa operazione portano ad errori anche vastemente diversi, con valori così alti in alcuni casi da rendere inutilizzabile il risultato.
Come possiamo quindi calcolare l'errore (relativo/assoluto) di un algoritmo?
1. Partendo da un algoritmo $f_a(x)$ e vogliamo stimare $\delta_a=f_a(P_1)-f(P_1)$ e $\epsilon_a=\frac{f_a(P_1)-f(P_1)}{f(P_1)}$, ignorando l'errore di arrotondamento sui dati (ovvero $\delta_j=0 \forall j$).
2. Disegniamo il grafo (o albero) dell'algoritmo, sfruttando le relazioni per l'errore nelle 4 operazioni standard.
3. Sui "checkpoint" metto l'errore di arrotondamento, sui collegamento metto la propagazione dell'errore delle 4 operazioni.
4. Partiamo dall'ultimo checkpoint e sostituiamo via via i dati.
##### Esempio
<<<<<<<<<<
# Problema Diretto
Data una $f$, un algoritmo per essa e una stima di $\delta_{x_j}$:
Stimare (maggiorare) $\delta_f \quad \text{per} \quad P_0\in D \subset R$.
##### Esempio
<<<<<<<<<<
# Problema Inverso
Dato $\tau >0,f,D\in R^n$:
Determinare un algoritmo ed il relativo valore di $U$ tale che $|\delta_f|<\tau$.

Risoluzione:
1. stimare $|\delta_{x_i}| \forall i$ in funzione di $U$. ($\delta_{x_i} = \max\{|x_i|\} \cdot U$).
2. Calcolare $A_i\forall i$ in funzione di $U$. ($A_i=\sup_{x\in D}|\frac{ \partial f}{\partial x_i}|(x)$)
3. Otteniamo
###### Esempio
<<<<<<<<<<