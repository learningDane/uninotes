#uni 
Partendo da
$$
\begin{cases}
\dot{x}=Ax+Bu \\
y=Cx+Du
\end{cases}
$$
Per sistemi LTI possiamo calcolare in forma chiusa la funzione di transizione di stato (ovvero la soluzione):
$$
\large
\begin{cases}
x(t)=\phi(t,t_{0},x(t_{0}),u(\dot{})) \\
y(t)=\gamma(t,t_{0},x(t_{0}),u(\dot{}))
\end{cases}
$$
# Equazioni differenziali omogenee, caso scalari
Sappiamo che se abbiamo a che fare con [[Equazioni Differenziali]] Scalari Omogenee, la sua soluzione dato $x(t_{0}=0)=x_{0}$ è una esponenziale ([[Numeri Immaginari (o Complessi)]]).
$$
\begin{matrix}
 \begin{cases}
\dot{x}(t)=a \cdot x(t) \\
x(t_{0}=0)=x_{0}
\end{cases} \\
\text{soluzione:} \quad x(t)=x_{0}e^{a\cdot t}
\end{matrix}
$$

Che sarà crescente,  decrescente o costante, a seconda del valore di $a$: se la parte reale è positiva sarà crescente, se è negativa sarà decrescente, se è $0$ sarà costante.

Sviluppiamo in serie la funzione esponenziale:
$$
e^{a\cdot t}=\sum_{i=0}^\infty a^i \frac{t^i}{i!} \quad, \quad a \in R
$$

# Equazioni differenziali omogenee, caso vettoriale
Noi però abbiamo a che fare con sistemi di equazioni differenziali, consideriamo quindi il caso vettoriale omogeneo:
dato un sistema LTI con $u(t)=0, \quad \dot{x}=Ax(t), \quad x(t_{0})=x_{0}$
$$
\large
\begin{matrix}
\mathbf{Teorema:}  \\
\text{La soluzione dell'equazione differenziale vettoriale è del tipo:} \\
x(t)=e^{A\cdot t} x_{0} \\
\text{dove} \quad e^{A \cdot t}=\sum_{{i=0}}^\infty A^i \frac{t^i}{i!} \\
\text{è chiamato esponenziale della matrice } A
\end{matrix}
$$
$e^{A \cdot t}$ è la ==matrice di transizione== e determina in assenza di ingresso il moto libero del sistema.

Siamo arrivati alla soluzione:
$$
x(t)=\phi(t,t_{0},x(t_{0}),u=0)=e^{A(t-t_{0})}x(t_{0})
$$
