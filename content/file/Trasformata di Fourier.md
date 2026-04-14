#uni 
Definizione:
Dato un segnale $x(t)$ ad *energia finita*, si definisce TCF (Trasformata Continua di Fourier):
$$
\large
X(f)=\int x(t)e^{-j2\pi f t}dt
$$
questa si chiama *Equazione di Analisi* poiché riesco a fare l'analisi delle componenti frequenziali del segnale.

Si definisce **anti-trasformata** continua di Fourier:
$$
x(t)=\int X(f)e^{j2\pi f t}df
$$
questa si chiama *Equazioni di sintesi* poiché attraverso la trasformata sintetizzo il segnale effettivo.

Ad ogni segnale $x(t)$ corrisponde una ed una sola $X(f)$ e viceversa:
$$
x(t) \iff X(f)
$$

Vale per segnali reali e complessi (ovviamente i segnali fisici sono reali).
# Trasformata di Fourier

>[!theorem] Trasformata di Fourier
>$$
>\large
>\begin{matrix}
>\text{Equazione di Analisi:} & X(f)=\int x(t)e^{-j2\pi f t}dt
>\\
>\text{Equazione di Sintesi:} & x(t)=\int X(f)e^{j2\pi f t}df
>\\
>\text{Univocità:} & x(t) \iff X(f)
>\end{matrix}
>$$

# Spettro di Ampiezza e di fase
La funzione complessa $X(f)$ può essere scomposta:
$$
\large
X(f)=|X(f)|e^{j\angle X(f)}
$$
dove:
- $|X(f)|$ è lo **Spettro di ampiezza**
- $\angle X(f)$ è lo **Spettro di fase**
Queste sono ampiezza e fase delle componenti frequenziali in cui il segnale è scomposto.
## Simmetria degli spettri per segnali reali (fisici)
Dato un segnale $x(t)\in R$:
$$
\begin{matrix}
|X(-f)|=|X(f)|\quad \text{Spettro di ampiezza: simmetria pari}
\\
\angle X(-f)=-\angle X(f) \quad \text{Spettro di fase: simmetria dispari}
\\
\text{ovvero:}\quad X(-f)=X^*(f) \quad \text{Simmetria Hermitiana}
\end{matrix}
$$
Questa simmetria non è soddisfatta da segnali complessi $x(t) \in C$
# Teorema di Parseval
L'energia di un segnale nel tempo è uguale all'energia in frequenza:

>[!theorem] Teorema di Parseval
>$$
>\large
>E_x=\int |x(t)|^2dt=\int |X(f)|^2df
>$$
>densità spettrale di energia: $\large \cal E_x(f)=|X(f)|^2$
>

Questo teorema vale sia per segnali Reali che complessi.
# Densità spettrale di potenza
Per i segnali a potenza media finita si ha che:
$$
\begin{matrix}
P_x= \lim_{T\to \infty}\frac{E_{x_T}}{T}=\lim_{T\to \infty}\int \frac{|X(f)|^2}{T}df=\int \lim \frac{|X(f)|^2}{T}df=
\\
\large P_x=\int \cal P_x(f)df
\end{matrix}
$$
dove $\cal P_x(f)$ è la densità spettrale di energia.
# Spectrum Analyzer
I dispositivi che prendono in ingresso un segnale e restituiscono l'ampiezza e la fase del segnale si chiamano **spectrum analyzer**.

Questi dispositivi utilizzano l'algoritmo *fast fourier transform* (**FFT**).
# Relazione tempo-banda
- Un segnale di breve durata nel tempo ha uno spettro largo in frequenza.
- Un segnale con spettro stretto in frequenza ha una lunga durata nel tempo.

Legame durata nel tempo - durate in frequenza:
$$
\Delta_t\Delta_f\approx \text{costante}
$$
# extra
- segnali che cambiano velocemente hanno componenti frequenziali più significative
- Le componenti frequenziali elevate sono responsabili dei cambiamenti più rapidi.
# Teoremi della trasformata di Fourier
## Linearità
$$
x(t)=ax_1(t)+bx_2(t)\iff  X(f)=aX_1(f)+bX_2(f)
$$
## Dualità
$$
x(t)\iff X(f) \leftrightarrow X(t) \iff x(-f)
$$
Se inverto le forme d'onda
## Teorema del Ritardo
$$
\begin{matrix}
y(t)=x(t-t_0) \iff Y(f)=X(f)e^{-j2 \pi f t_0}
\\
\to |Y(f)|=|X(f)|
\\
\to \angle Y(f)=\angle X(f)-2\pi f t_0
\end{matrix}
$$
Un ritardo temporale:
- modifica lo spettro di fase: introduce una fase che cresce linearmente con la frequenza
- non cambia lo spettro di ampiezza
## Teorema della Modulazione
$$
x(t)\cos (2\pi f_o t) \iff \frac{X(f-f_0)+ X(f+f_0)}{2}
$$
# Trasformate Notevoli

| Nome                       | tempo                                      | frequenza                               |
| -------------------------- | ------------------------------------------ | --------------------------------------- |
| f. esponenziale monolatera | $x(t)=e^{-t/T}u(t)$                        | $X(t)=\frac{T}{1+2j\pi f T}$            |
| funzione rettangolare      | $x(t)=\text{rect}\left(\frac{1}{T}\right)$ | $X(t)=T\text{sinc}(fT)$                 |
| f. Seno Cardinale          | $x(t)=\text{sinc}(2Bt)$                    | $\frac{1}{2B}\text{rect}(\frac{f}{2B})$ |
|                            | $x(t)=\text{sinc}^2(2 Bt)$                 | $\frac{1}{2B}\text{tri}(\frac{f}{4B})$  |
note:
- seno cardinale: $\text{sinc}(\alpha)=\frac{\sin(\pi\alpha)}{\pi \alpha} \quad \forall \alpha \neq 0,\quad \text{sinc}(0)=1$ 