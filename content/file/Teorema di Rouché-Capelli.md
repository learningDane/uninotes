Il teorema ci dice se il [[Sistema Lineare]] ammette almeno una soluzione.
Quindi $Ax=b$ ammette __almeno una soluzione__ se $rango(A)=rango(A|B)$:$$\begin{bmatrix}
a_{11} & \cdots & a_{1n} & b_1 \\
\vdots & & & \vdots \\
a_{m1} & \cdots & a_{mn} & b_m
\end{bmatrix}\in \mathbb{C}^{m\times(n+1)}$$ Per quanto riguarda l'__unicità__ della soluzione:
sappiamo che se $m\geq n$ (__sistema sovradeterminato__)
- se $rango(A)=n$ allora __sol. unica__
- se $rango(A)<n$ allora $\infty$ soluzioni e il loro insieme forma un sottospazio vettoriale di $dim = n-rango(A)$ 