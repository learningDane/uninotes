#uni 
# Parametri Caratteristici
- $t_d$: tempo di ritardo, il tempo necessario a raggiungere il 50% del guadagno statico
- $t_r$: tempo di risposta, il tempo necessario a raggiungere il valore del guadagno statico: $\text{per un target di 90\%G(0):}\quad t_r=\frac{1.8}{w_n}$ 
- $s$ ( o $M_p$): overshoot, la massima elongazione relativa, di solito in percentuale: $s\%=100e^{\frac{-\xi \pi}{\sqrt{1-\xi^2}}}$
- $t_p$ (o $t_{max}$): tempo di massima elongazione: $t_{max}=\frac{\pi}{w_n \sqrt{1- \xi ^2}}$ 
- $t_s$ (o $t_{ass}$): tempo di assestamento, il tempo necessario per raggiungere (e mantenere) un valore compreso in una certa fascia di tolleranza $\epsilon$, di solito del $2\%$, oppure del $5\%$: $t_{ass}=\frac{-\ln(\frac{\pm \Delta \%}{100})}{\xi w_n}$  
- $T_P$: periodo di oscillazione, periodo tra due picchi: $T_P=\frac{2 \pi}{w_n \sqrt{1- \xi^2}}$ 
# Calcolo degli errori

| Ingresso $r(t)$                             | Tipo 0          | Tipo 1        | Tipo 2        |
| ------------------------------------------- | --------------- | ------------- | ------------- |
| Gradino $1(t)$                              | $\frac{1}{1+k}$ | $0$           | $0$           |
| Rampa $t \cdot 1(t)$                        | $\infty$        | $\frac{1}{k}$ | $0$           |
| Parabola $\frac{1}{2} \cdot t^2 \cdot 1(t)$ | $\infty$        | $\infty$      | $\frac{1}{k}$ |
Per calcolare l'errore ad un determinato ingresso, applico il teorema del valore finale della [[Trasformata di Laplace]] alla funzione errore $E(s)=\frac{1}{1+L(s)}$.
# Margini
Idealmente vorremo un margine di fase ([[Diagramma di Bode#Margini di Fase e di Guadagno]]) di $90 \deg$, ma non sempre è possibile, utilizziamo quindi la seguente regola empirica:
$$
m_\phi\geq m_\phi^* \approx 100 \xi^*
$$
con $\xi^*$ lo smorzamento relativo all'overshoot desiderato.
# Cancellazione di Modi indesiderati
È possibile progettare un controllore tale che annulli le parti della $G(s)$ che non ci piacciono, non posso però svolgere ___cancellazioni improprie___, ovvero cancellare zeri e poli con parte reale maggiore di $0$.
Questo perché nella realtà queste cancellazioni non sono perfette e non possiamo quindi operare con dinamiche instabili.
# Sensitività e Reiezione dei Disturbi di Carico
![[controlloinfeedback.svg|500]]
La sensitività è la [[Funzione di Trasferimento]] che lega i disturbi di carico all'uscita.
$$
S(s)=\frac{1}{1+L(s)}
$$
con $L(s)=C(s) \cdot G(s)$, ovvero la funzione in anello aperto.
$$
Y(s)=\frac{1}{1+L} \cdot D(s)=S(s) \cdot D(s)
$$

Una specifica possibile è la seguente:
$$
\begin{matrix}
S(s)\leq \epsilon_n \quad \text{per} \quad w\leq w_n \\
\to \quad |1+L(s)| \geq \frac{1}{\epsilon_n} \quad \to \quad |L(s)| \geq \frac{1}{\epsilon_n} \quad \text{per}\quad w \leq w_n
\end{matrix}
$$
# Reiezione dei disturbi di Misura
![[controlloinfeedback.svg|500]]
La [[Funzione di Trasferimento]] che studia l'amplificazione dell'azione di controllo in funzione del riferimento e/o del disturbo è la seguente:
$$
\begin{matrix}
Q(s)= \frac{C(s)}{1+C(s)\cdot G(s)}=\frac{C(s)}{1+L(s)} \\
\text{e quindi} \quad U(s)= Q(s) \cdot R(s) \quad \text{o} \quad N(s)
\end{matrix}
$$
# Frequenza di Taglio (o crossover)
La frequenza di Taglio è la frequenza alla quale il modulo della [[Funzione di Trasferimento]] ad anello aperto ($L(s)=C(s) \cdot G(s)$) è $1$, ovvero $0dB$.
Normalmente prendiamo la prima frequenza alla quale $|L(s)|=1$.
Se $|L(s)|\neq 1 \forall w$ la frequenza di taglio non esiste, non posso quindi calcolare il [margine di fase](Diagramma%20di%20Bode.md#Margini%20di%20Fase%20e%20di%20Guadagno).
# Banda Passante
La banda passante è la frequenza alla quale il modulo della funzione di trasferimento ad anello chiuso ($H(s)=\frac{L(s)}{1+L(s)}$) è di $3dB$ inferiore rispetto a $H(0)$.