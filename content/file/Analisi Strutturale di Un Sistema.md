#uni 
# Stabilità
| stabilità  | Modi          | Autovalori                                                                                                                          |
| ---------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Asintotica | tendono a $0$ | $Re(\lambda) <0$                                                                                                                    |
| Marginale  | limitati      | $Re(\lambda) \leq 0$ e per i $\lambda$ per cui $Re(\lambda)=0$, $q$ (dimensione del blocco di jordan relativo) $=1$, ovvero $mg=ma$ |
### Esempio
$$
A=\begin{bmatrix}
-7   & |& 0 & 0 &| &  0 \\ \hline
0 & | & 0 & -2 &| &  0 \\
0 &| &  2 & 0 &| & 0 \\ \hline
0 &| &  0 & 0 &| &  -8
\end{bmatrix}
$$
questa è una matrice diagonale a blocchi, quindi sappiamo che gli autovalori di questa matrice sono gli autovalori dei blocchi:
- $\lambda_1=-7$
il prossimo blocco presenta due autovalori complessi coniugati:
- $\lambda_2=0+2j$
- $\lambda_3=0-2j$
ed infine l'ultimo:
- $\lambda_4=-8$ 
Quindi abbiamo 4 autovalori distinti, di cui due con parte reale nulla, il sistema può quindi essere o instabile o marginalmente stabile, se e solo se le relative molteplicità geometrica e algebrica coincidono. Essendo tutti autovalori distinti le molteplicità algebriche sono pari a $1$, inoltre sappiamo che $mg \leq ma$, quindi $mg=1=ma$, quindi il sistema è marginalmente stabile.
# Modi
- Se gli autovalori sono tutti diversi e reali, i modi sono tanti quanti gli autovalori e si calcolano come $e^{\lambda_i t}$.
- I modi relativi ad autovalori complessi coniugati si calcolano invece come $e^{\sigma t}\cos(\omega t)$ e $e^{\sigma t} \sin (\omega t)$.
- I modi relativi ad autovalori con molteplicità algebrica non unitaria sono $t^je^{\lambda_{i}t}$ con $j=0,...,ma-1$ 