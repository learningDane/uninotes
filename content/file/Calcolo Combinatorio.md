#uni 
- Ho una procedura composta da $N$ passi.
- Ogni passo è svolgibile in $k_1,k_2,..$ modi diversi

Numero di modi in cui una procedura può essere fatta:
$$
M=\prod_{i=1}^N k_i
$$
- se però $k_i=k_j \forall i,j \implies M=k^N$.
# Disposizioni
Una disposizione di $N$ oggetti presi $k$ a $k$ è una sequenza ordinata di $k$ oggetti scelti tra gli $N$ associati. 

Numero di disposizioni semplici (no ripetizioni) di $N$ oggetti:
$$
D_{N,k}=\frac{N!}{(N-k)!}
$$
# Permutazioni
Se parlando di disposizioni abbiamo $k=N$, si parla di permutazioni semplici:
$$
P_{N}=N!
$$
# Combinazioni
Una combinazione semplice di $N$ oggetti presi $k$ a $k$ è una sequenza non ordinata di $k$ oggetti fra gli $N$ dati:
$$
C_{N,k}=\frac{D_{N,}}{k!}=\frac{N!}{k!(N-k)!}=\begin{pmatrix}N\\k\end{pmatrix}:\text{Coefficiente binomiale di N su k}
$$
# Formula di Bernoulli
Probabilità che l'evento $A$ (con $P(A)=p$) si verifichi $k$ volte in $N$ prove in un ordine qualsiasi:
$$
P(E)=\binom{N}{k}p^k(1-p)^k=\frac{N!}{k!(N-k)!}p^k(1-p)^k
$$