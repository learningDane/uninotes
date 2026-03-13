#uni 
Consideriamo due diversi esperimenti aleatori caratterizzati da spazi campione diversi.
Indichiamo con $A_1$ il generico evento del primo esperimento e con $A_2$ il generico evento del secondo.
Indichiamo le funzioni di probabilità: $P_1()$ e $P_2()$.

È possibile definire un esperimento composto con:
- risultati: coppia ordinata dei risultati degli esperimenti componenti
- spazio campione: prodotto cartesiano degli spazi campioni dei componenti: $\Omega = \Omega_1 \times \Omega_2$
- eventi: tutti i sottoinsiemi di $\Omega$ del tipo $A=A_1 \times A_2$

Calcoliamo la probabilità dell'evento $A=A_1 \times A_2$, sapendo $P_1(A_1)$ e $P_2(A_2)$.
Questo problema non ha in generale una soluzione: dalla conoscenza delle leggi di probabilità dei singoli esperimenti non è possibile ricavare la legge di probabilità dell'esperimento congiunto.
Eccezione fatta per il caso di esperimenti indipendenti: se il risultato del primo esperimento non influenza il risultato dell'altro.

# Composizione di esperimenti indipendenti
- Spazio campione composto: $\Omega = \Omega_1 \times \Omega2$
- eventi: tutti i sottoinsiemi di $\Omega$ del tipo $A=A_1 \times A_2$, formati dalle coppie $(\xi,\lambda)$, tali che $\xi \in A_1$ e $\lambda \in A_2$
- Funzione di probabilità $P(\cdot)$ 

Osserviamo che $P(A \times \Omega_2)=P_1(A_1)$ e $P(A \times \Omega_1)=P_2(A_2)$.

$$
\begin{matrix}
A=A_1 \times A_2=(A_1 \times \Omega_2)\cap (\Omega_1 \times A_2)
\\
P(A)=P(A_1 \times A_2)=P((A_1\times \Omega_2)\cap (\Omega_1\times A_2))= P(A_1\times \Omega_2)\cdot P(\Omega_1 \times A_2) =P_1(A_1)\cdot P_2(A_2)
\end{matrix}
$$

Ovvero la condizione di indipendenza tra due esperimenti equivale ad assumere indipendenti tutti gli eventi del tipo $(A_1 \times \Omega_2)$ e $(\Omega_1 \times A_2)$ definiti nello spazio campione $\Omega$ dell'esperimento composto.
## Prove ripetute binarie e indipendenti
Consideriamo un esperimento con uno spazio campione $\Omega=\{ A,\overline A\}$ costituito da due risultati soltanto: $P(A) = p; \quad P(\overline A)=1-p=q$.

Consideriamo poi l'esperimento composto ottenuto ripetendo N volte lo stesso esperimento e facendo in modo che ciascuna prova sia *indipendente* dalle altre:
Calcolare la probabilità $P(E)=P(\text{A si verifica k volte in un ordine qualsiasi})$.
- $E=E_1 \cup E_2 \cup ... \cup E_R$ ($E_i$ eventi disgiunti)
- $R$ = numero di sequenze distinte che contengono $k$ eventi $A$ 
$$
E_1=\underbrace{A\times A\times ...\times A}_k\times\underbrace{\overline A \times \overline A \times ... \times \overline A}_{N-k}
$$