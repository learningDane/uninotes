#uni 
Idea: 
$$
\lim_{k \to \infty}x^{(k)}=x
$$
con $k$ iterazioni.
# Metodi di punto fisso
$$
x=Hx +c \implies x=(I-GA)x+Gb
$$
con $G$ matrice non singolare qualsiasi.

Processo iterativo:
$$
x^{(k+1)}=Hx^{(k)}+c, \quad k=0,1,...
$$
- $x^{(0)}$ approssimazione iniziale della soluzione.
- $H$ matrice di iterazione

> [!Theorem] 
> Condizione necessaria e sufficiente affinché un metodo iterativo della forma $x^{(k+1)}=Hx^{(k)}+c$ sia convergente per qualunque vettore iniziale $x^{(0)}$, è che la sua matrice di iterazione $H$ sia convergente

Corollari:
- per la convergenza è necessaria e sufficiente $\rho(H)<1$ 
- condizione sufficiente per la convergenza è l'esistenza di una norma naturale per cui: $||H||<1$ 
## Criteri di stop
1. restringere il residuo $\frac{|r^{(k)}}{|b|} < \delta$ 
2. restringere la variazione di errore $|x^{(k+1)}-x^{(k)}|<\delta$ 
# Idea
$$
A=D-E-F
$$
dove:
- $D$ è la diagonale di $A$
- $E$ è l'opposta della triangolare inferiore a diagonale nulla
- $F$ è l'opposta della triangolare superiore a diagonale nulla

$$
Ax=b\implies (D-E-F)x=b
$$

$$
\begin{cases} x^{(0)} \\ 
x^{(k+1)}=H x^{(k)} + c \quad \text{equazione di punto fisso}
\end{cases}
$$
## Metodo di Jacobi
$$
H_J=D^{-1}(E+F)
$$
- Ogni iterazione costa $O(n^2)$.

$$
(H_J)_{ij}=\begin{cases}-\frac{a_{ij}}{a_{ii}} & \text{se} \ i \neq j \\ 0 & \text{se} \ i=j\end{cases}
$$
Equazione:
$$
x_i^{(k+1)}=\frac{1}{a_{ii}}(b_i-\underbrace{\sum _{\begin{matrix}j=1\\ j \neq i\end{matrix}}^n a_{ij} x_j^{(k)}}_{(E+F)\cdot x})
$$
- per calcolare $x_j^{(k+1)}$ servono tutte le entrate di $x^{(k)}$, quindi non posso sovrascriverlo finché non ho tutto $x^{(k+1)}$.
## Metodo di Gauss-Seidel
$$
H_{GS}=(D-E)^{-1}\cdot F \quad \quad c=(D-E)^{-1}\cdot b
$$
- costo di ogni iterazione: $O(n^2)$.
# Considerazioni
Sia Jacobi sia Gauss-Seidel necessitano di elementi non nulli sulla diagonale, possiamo quindi trovare permutazioni $\Pi A x = \Pi b$ in modo da trovare una permutazione $\Pi x$ di $x$.

> [!Theorem] Teorema
> se $A$ è a predominanza diagonale forte oppure è irriducibile e a predominanza diagonale debole (matrice non singolare) allora il metodo di Jacobi e quello di Gauss-Seidel convergono (hanno però due dimostrazioni diverse).