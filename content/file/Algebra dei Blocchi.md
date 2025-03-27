#uni 
# Connessione in Serie
![[connessioneinserie.svg]]
$$
\begin{matrix}
G(s)=\prod_i G_i(s) =\frac{n_1(s) \cdot n_2(s)}{d_1(s) \cdot d_2(s)}\\
Y(s)=G(s) \cdot E(s)
\end{matrix}
$$
- se $n_1,d_2$ hanno radici in comune, $G$ non è [raggiungibile](Proprietà%20Strutturali.md#Raggiungibilità) (cancellazione zero-polo).
- se $n_2,d_1$ hanno radici in comune, $G$ non è [osservabile](Proprietà%20Strutturali.md#Osservabilità) (cancellazione polo-zero).
# Connessione in Parallelo
![[connessioneinparallelo.svg]]
$$
\begin{matrix}
G(s)=\sum_iG_i(s)=\frac{n_1 \cdot d_2 + n_2 \cdot d_1}{d_1 \cdot d_2}\\
Y(s)=G(s)\cdot R(s)
\end{matrix}
$$
- se $d_1,d_2$ hanno radici in comune, $G$ è [non osservabile e non raggiungibile](Proprietà%20Strutturali.md).
# Connessione in Retroazione
![[controlloinfeedback.svg]]
$$
\begin{matrix}
G(s)=\frac{G_1(s)}{1+G_1(s) \cdot G_2(s)}=\frac{n_1\cdot d_2}{d_1 \cdot d_2 + n_1 \cdot n_2}\\
Y(s)=G(s) \cdot R(s)
\end{matrix}
$$
- in questo caso le cancellazione possono avvenire se $n_1$ e $d_2$ hanno fatto comuni.
>La retroazione modifica i poli ma non gli zeri del sistema in catena diretta
