#uni 
Siamo arrivati ad utilizzare strumenti algebrici anche relativamente complessi ([[Teoria dei Sistemi]]), studiamo ora un metodo di studio di sistemi che semplifichi i conti.
È sempre possibile passare da una forma in variabili di stato ad una ___funzione di trasferimento___.

> Quando usare quale? Per sistemi SISO: funzione di trasferimento, per sistemi MIMO: forma in variabili di stato

___Definizione___: la ___funzione di trasferimento___ di un sistema dinamico nella variabile $s$ è il rapporto fra l'uscita e il suo ingresso: $F(s)=\frac{Y(s)}{U(s)}$. 

![[funzioneditrasferimento1.svg]]

# Risposta all'impulso
I sistemi LTI possono essere caratterizzati attraverso la loro risposta all'impulso (ovvero supponiamo $u(t)=\delta(t)$:
$$
y(t)=g(t)*r(t)=\int_0^tg(t-\tau)\cdot r(\tau)d\tau=\int_0^tg(\tau) \cdot r(t-\tau)d\tau \quad ; \quad \geq 0
$$
con $r(t)$ il segnale di riferimento (input), $y(t)$ l'uscita e $g(t)$ la ___risposta all'impulso___.
In [Laplace](Trasformata%20di%20Laplace.md) per via della [proprietà di convoluzione](Trasformata%20di%20Laplace.md#Proprietà%20di%20Convoluzione) invece abbiamo semplicemente:
$$
Y(s)=G(s) \cdot U(s)
$$
Essenzialmente a partire dalla conoscenza di come un sistema risponde all'impulso, possiamo calcolare come questo stesso sistema risponde a qualsiasi altra entrata, grazie alla [[convoluzione]].

>L'antitrasformata di una funzione di trasferimento rappresenta la risposta all'impulso unitario.

>L'integrale della risposta all'impulso unitario rappresenta la risposta al gradino unitario.
# Dalla forma in Variabili di Stato alla Funzione di Trasferimento
Risolviamo il sistema con l'uso delle [[Equazioni Differenziali]] e otteniamo la Forma in Variabili di Stato:
$$
\begin{cases}
\dot{x}=Ax+Bu \\
y=Cx+Du
\end{cases}
$$
troviamo la funzione di Trasferimento:
$$
\begin{matrix}
G(s)=\frac{Y(s)}{U(s)} \\
\underbrace{s\cdot X(s)}_{L^{-1}\{\dot x(t)\}}=A \cdot X(s)+ B \cdot U(s) \implies \\

G(s)=C(s \cdot I - A)^{-1}\cdot B + D
\end{matrix}
$$

- ___Problema di Realizzazione___: la trasformazione in funzione di trasferimento non è unica.
## Matrice di Trasferimento del sistema (sistemi MIMO)
Ovviamente per sistemi MIMO la formula di cui sopra non risulta in una semplice frazione tra polinomi, ma in una matrice di funzioni di trasferimento, a loro volta frazioni tra polinomi:
$$
\begin{matrix}
G(s)=C(s \cdot I -A)^{-1}B=\begin{bmatrix}
g_{1,1} & ... & g_{1,m} \\... & ... & ... \\ g_{p,1}  & ... & g_{p,m}
\end{bmatrix} \\
m\text{ ingressi}, \ p \text{ uscite} \\
g_{ij}(s): \text{ da una entrata } u_j \text{ porta ad una uscita } y_i
\end{matrix}
$$
# Dalla Funzione di Trasferimento alla forma in Variabili di Stato: La Forma Canonica di Controllo (per sistemi SISO)
Attraverso una particolare scelta delle variabili di stato posso portarmi nella ___forma canonica di controllo___:
1. risolvo un sistema fisico e ottengo una equazione differenziale ___monica___:
$$
x^{(n)}+a_{n-1}\cdot x^{(n-1)}+...+a_1\cdot x^{(1)}+a_0\cdot x + a=b_m \cdot u ^{(m)}+...+b_0 \cdot u + b
$$
oppure una [[Funzione di Trasferimento]]:
$$
G(s) = \frac{b_m s^m + b_{m-1} s^{m-1} + \dots + b_0}{s^n + a_{n-1}s^{n-1} + \dots + a_0}
$$
2. Ridefinisco le variabili di stato come segue:
$$
\begin{cases}
x_1=x \\ x_2=x^{(1)} \\ ... \\ x_n=x^{(n-1)}
\end{cases}
$$
e risulta quindi:
$$
x_n^{(1)}=x^{(n)}=-a_{n-1} \cdot x_n-...-a_0 \cdot x_1 - b \cdot u
$$
3. Calcolo il vettore $\dot{ x}$ e lo porto in forma $\dot x = Ax + B u$:
$$
\begin{matrix}
\dot{x}=\begin{bmatrix}
x_1^{(1)} \\ x_2^{(1)}\\...\\x_n^{(1)}
\end{bmatrix} =\begin{bmatrix}
x_2\\x_3\\...\\ \small {-a_{n-1} \cdot x_n-...-a_0 \cdot x_1-b \cdot u}
\end{bmatrix}\\ \\
\text{Forma Canonica di Controllo:} \\

\dot{x}=\begin{bmatrix}
0 & 1 & ... & 0 \\0 & 0 & ... & 0 \\0 & 0 & ... & 1\\-a_0 & -a_1 & ... & -a_{n-1}
\end{bmatrix} \cdot \begin{bmatrix}
x_1\\x_2\\...\\x_n
\end{bmatrix} + \begin{bmatrix}
0\\...\\0\\1
\end{bmatrix} \cdot u \\
y=\begin{bmatrix}
b_0- a_0b & b_1-a_1b & ... & b_{n-1}-a_{n-1}b
\end{bmatrix}\cdot \begin{bmatrix}
x_1 \\x_2\\...\\x_n
\end{bmatrix}+b \cdot u
\end{matrix}
$$      
Quella che ho ottenuto è la forma canonica di controllo.

>Notiamo che i parametri $a_i$ sono i coefficienti del denominatore di $G(s)$