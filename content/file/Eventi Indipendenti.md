#uni 
Supponiamo che il verificarsi dell'evento A non fornisca alcuna informazione sull'evento B, ovvero $P[B|A]=P[B]$.
Dal [[Teorema di Bayes]] abbiamo che: $P[A|B]=P[A]$.
Quindi nessun evento ci da informazioni sull'altro evento.
Eventi che soddisfano questa condizione sono detti **eventi indipendenti**.
Da $P[A|B]=\frac{P[A\cap B]}{P[B]}$ ottengo:

$$
\text{Due eventi si dicono indipendenti se:} \quad P[A \cap B]= P[A] P[B]
$$

Interpretazione frequentista:
dati:
- $P[B] = P[B|A]$
- $P[A] = P[A|B]$
- $P[A\cap B]=P[A] P[B]$
- sono indipendenti
$$
\begin{matrix}
\frac{n_{A\cap B}}{n_A} \approx\frac{n_B}{N}
\\
\frac{n_{B\cap A}}{n_B} \approx\frac{n_A}{N}
\end{matrix}
$$
> Quindi frequenza di B nella sequenza di N ripetizioni dell'esperimento, approssima la frequenza di B nella sequenza di $n_A$ ripetizioni in cui si è presentato A.

Lo stesso vale per la frequenza di A.