#uni 
Dati punti $x_0,x_1,...$ detti **nodi**, in cui sappiamo il valore di una determinata funzione, vogliamo trovare una approssimazione di questa funzione **interpolando** i dati.

Possiamo:
- trovare una funzione particolarmente facile che minimizzi la distanza dai nodi: questo approccio viene usato se abbiamo tanti nodi e si chiama **regressione lineare: approssimazione ai minimi quadrati**.
- cercare un polinomio di grado $k$ (se abbiamo $k$ nodi), che passi per tutti i nodi, questo approccio viene usato se abbiamo pochi nodi.
# Interpolazione Polinomiale
Impostiamo il sistema:
$$
\begin{cases}
a_0+a_1x_0+...+a_kx_0^k=y_0
\\
...
\\
a_0+a_1x_k+...+a_kx_k^k=y_k
\end{cases}
$$
che in forma matriciale è:
$$
\underbrace{
\begin{pmatrix}
1 & x_0 & ... & x_0^k
\\
\vdots & & & \vdots
\\
1 & x_k & ... & x_k^k
\end{pmatrix} }_ V
\underbrace{
\begin{pmatrix}
a_0 \\ a_1\\ \vdots \\ a_k
\end{pmatrix} } _ a
=
\underbrace{
\begin{pmatrix}
y_0 \\ y_1 \\ \vdots \\ y_k
\end{pmatrix}
} _ y
$$
- dove $V$ è detta **Matrice di Vandermonde**

Quando questo sistema ha soluzione?
- non può avere $x_i=x_j \forall i\neq j$ altrimenti avrebbe due righe uguali e sarebbe singolare