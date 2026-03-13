#uni 
Supponiamo di eseguire un esperimento che coinvolta una coppia di eventi A e B:
- sia $P[A|B]$ La probabilità dell'evento A dato che l'evento B si è verificato
- la probabilità $P[A|B]$ è detta **prbabilità condizionata di A dato B**.

Assumendo che B abbia una probabilità non nulla:
$$
P[A|B] = \frac{P[A\cap B]}{P[B]}
$$
Questa probabilità condizionata cattura l'informazione parziale che il verificarsi dell'evento B fornisce sull'evento A.

La probabilità condizionata definisce un nuovo sistema di probabilità caratterizzato da:
- stesso spazio campione
- stessa classe di eventi
- **diversa legge di probabilità**

Fissato un evento B, $P[A|B]$ è una legge di probabilità in quanto soddisfa gli assiomi:
- normalizzazione: $\Omega = A: \quad P[\Omega|B]=\frac{P(\Omega \cap B)}{P(B)}=\frac{P(B)}{P(B)}=1$ 
- non negatività: soddisfatto per definizione
- additività: dati A1 e A2 disgiunti: $P[A1 \cup A2 | B]=\frac{P[A1 \cup B]}{P[B]}+\frac{P[A2 \cup B]}{P[B]}$ 

Facciamo una interpretazione in termini di frequenza relativa (supponendo di ripetere l'esperimento $N$ volte):
$$
P[A|B]= \frac{P[A\cap B]}{P[B]}\approx\frac{\frac{n_{A\cap B}}{N}}{\frac{n_B}{N}}=\frac{n_{A\cap B}}{n_B}
$$
Se consideriamo solo la sequenza degli $n_B$ risultati in cui si è verificato l'evento $B$, $P[A|B]$ approssima la frequenza di presentazione dell'evento $A$ in tale sequenza.
# Proprietà della probabilità condizionata
$$
\begin{matrix}
\text{I.} & \text{Se } A \cap B=\emptyset \implies P[A|B]=0
\\
\text{II.} & \text{Se } A \subset B =A \implies P[A|B]=\frac{P[A]}{P[B]} \geq P[A]
\\
\text{III.} & \text{Se } B \subset A=B \implies P[A|B]=\frac{P[B]}{P[B]}=1
\end{matrix}
$$
