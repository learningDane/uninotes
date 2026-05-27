#uni 
# Sistemi trinagolari
Si usa la sostituzione all'indietro se è triangolare inferiore, altrimenti se è triangolare superiore la sostituzione in avanti.

La sostituzione avanti/indietro costa $O(n^2)$.
# Eliminazione di Gauss
1. Ci si porta in forma triangolare $U\cdot x=c$ 
2. sostituzione indietro/avanti

La riduzione costa $O(2/3 n^3)$ e poi c'è la sostituzione.

Non possiamo però avere un elemento sulla diagonale nullo, poiché la divisione fallirebbe ($l_{ji}=\frac{a_{ji}}{a_{ii}}$). Utilizziamo allora il pivoting: utilizzare una matrice di permutazione che porti un elemento diverso da zero sulla diagonale.
## Fattorizzazione LU
$A=LU$ con
- $U=H_{n-1} \cdot ... \cdot H_1 \cdot A$
- $L=H_1^{-1} \cdot ... \cdot H_{n-1}^{-1}$ 
- $H_i$ è un matrice in cui ogni riga $j$ rappresenta una operazione lineare effettuata sulla riga $j$, esempio: $H_1=\begin{pmatrix}1 & ... & ... & 0 \\ -l_{21} & 1 & ... & 0 \\ & ... \\ -l_{n1} & ... & ... & 1\end{pmatrix}$ 
- per invertire una $H$ basta cambiare i segni dei moltiplicatori $l$
- $Ax=b \implies LUx=b \implies \begin{cases} Lc=b \\ Ux=c \end{cases} \implies x = U^{-1} L ^{-1} b$ che costa $O(n^2)$ 
# Condizionamento di un sistema lineare
$$
\frac{||\tilde x-x||}{||x||} \leq \mu(A) \frac{||r||}{||b||}
$$
- se un problema è mal condizionato ($\mu(A) >> 1$), un residuo piccolo non garantisce un errore piccolo
- se invece un problema è ben condizionato, un residuo piccolo garantisce un errore piccolo
- se $A$ è hermitiana ($A=A^*$) il numero di condizionamento in norma 2 diventa: $\mu(A)=\frac{\max|\lambda_i|}{\min |\lambda_i|}$ 
- $\tilde x$ è la soluzione ottenuta
- $r$ è il **vettore residuo**: $r=b-A\tilde x$ 
# NON INVERTIRE MATRICI
$$
A^{-1} \cdot b = A \ \text{\\} \ b
$$
ovvero meglio risovere sistemi lineari invece che invertire matrici.