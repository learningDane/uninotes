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

La potenza media di un segnale $x(t)$ troncato nel tempo $x_T(t)$ è:
$$
\begin{matrix}
P_{x_T}= \frac{E_{x_T}}{T}
\\
\text{e l'energia:} \quad E_{x_T}=\int{x_T}^2(t)dt
\end{matrix}
$$

Definiamo allora la potenza media di un segnale qualunque:
$$
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

@todo