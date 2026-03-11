#uni 
Un **segnale** è una qualunque grandezza fisica variabile cui è associata una certa informazione.

Si dividono in:
- Segnali **Deterministici**: 
	- segnali noti
	- per ogni istante temporale si conosce il suo valore
	- rappresentabile con funzioni analitiche
- Segnali **Aleatori**:
	- segnali non noti a priori
	- rappresentabili statisticamente

In generale un segnale può essere espresso in funzione di più variabili indipendenti.

Un'altra suddivisione è la seguente:
- segnali **Continui**: il segnale varia con continuità nell'insieme
- segnali **Discreti** 
# Segnali Complessi
Dato un segnale complesso $z(t)$:
$$
\begin{matrix}
z(t) = a(t) + i\cdot b(t)= c\cdot e^{i\theta(t)}
\\
\large {\frac{dz(t)}{dt}=\frac{da(t)}{dt}+i\cdot \frac{db(t)}{dt}}
\\
\int z(t)dt = \int a(t)dt + i\cdot \int b(t)dt
\end{matrix}
$$
# Potenza ed energia
La potenza istantanea Normalizzata di un segnale $x(t)$ è:
$$
P(t)={|x|}^2(t)
$$

L'energia totale dissipata dal segnale $x(t)$ è:
$$
E=\int_{-\infty}^{+\infty} P(t)dt=\int_{-\infty}^{+\infty} {|x|}^2(t)dt 
$$

La **potenza media** di un segnale $x(t)$ troncato nel tempo $x_T(t)$ è:
$$
\begin{matrix}
P_{x_T}= \frac{E_{x_T}}{T}
\\
\text{e l'energia:} \quad E_{x_T}=\int{x_T}^2(t)dt
\end{matrix}
$$

Definiamo allora **la potenza media di un segnale qualunque**:
$$
\large
P_x=a \lim_{T\to \infty}P_{x_T}=\lim\frac{E_{x^T}}{T}=\lim _{T \to \infty}\frac{1}{T}\int_{-T/2}^{+T/2}|x(t)|^2dt
$$
Ne otteniamo che:
- un segnale ad energia finita ha potenza media nulla
- un segnale a potenza media finita ha energia infinita
# Segnali Periodici
Definiamo un segnale periodico come segue:
$$
x(t)=x(t+T_0)
$$

La potenza media di un segnale periodico è:
$$
\large
P_x=\frac{1}{T_0}\int_{-T_0/2}^{T_0/2}|x(t)|^2dt
$$
dove $T_0$ è il periodo.
# Lunghezza d'onda
La lunghezza d'onda è lo spazio percorso dall'onda durante un periodo di oscillazione e vale:
$$
\lambda = \frac{c}{f_0}\text{m}
$$
dove:
- $c=3\times 10^8m/s$
- $f_0$ è detta **frequenza portante**

Valori notevoli:

| frequenza f_0 | lunghezza d'onda |
| ------------- | ---------------- |
| 2.4GHz        | 0.125m           |
| 3GHz          | 0.1m             |
| 5.1GHz        | 0.06m            |
| 30GHz         | 0.01m            |
# Rapporto Segnale - Rumore (SNR)
Il rapporto segnale rumore (**SNR**) vale:
$$
\text{snr} = \frac{P_\text{ricevuta}}{P_\text{rumore termico}}=\frac{P_r}{P_n}
$$

dove possiamo approssimare $P_n$ a $B\cdot K_B \cdot T$.