#uni 
$$
\large
\begin{matrix}
\text{dati} \quad \beta \in N, m\in N ,\quad L,U \in Z \quad \text{tale che} \quad L<U \\
\text{Definiamo}  \\
\quad F(\beta,m,L,U)= \left\{  x \in R : segno(x) \cdot \beta^e \sum_{{j=1}}^m \alpha_{j} \beta^{-j},L \leq e \leq U, \alpha_{j} \in \{ 0,..,\beta-1 \} , \alpha_{1} \neq 0 \right\} \cup \{\emptyset\}
\end{matrix}
$$
esempio per $\beta=2, L=-1, m=3, U=3 \to [\beta^i,\beta^{i+1}]$
![[esempiorapprvirgola1.svg|700]]
se guardiamo i numeri in scala logaritmica sarebbero **equispaziati**.
In ogni intervallo $[2^i;2^{i+1}]$ ho numeri di macchina che hanno esponente $e=i+1$ e variano solo di mantissa.

==Minimo Numero Rappresentabile==: $\beta^{L-1}$
==Massimo Numero Rappresentabile==: $\beta^U(1-\beta^{-m})$ 
==Quanti sono i numeri di Macchina in Binario==: $2 \cdot (U-L+1)$ 

# Rappresentazioni più comuni (Standard IEEE)

|                    | $\beta$ | $m$ | $L$   | $U$  | Memoria |
| ------------------ | ------- | --- | ----- | ---- | ------- |
| Precisione Singola | 2       | 24  | -125  | 128  | 32      |
| Precisione doppia  | 2       | 53  | -1021 | 1024 | 64      |
Ci potremmo chiedere come mai $L$ assume valori non ovvi (-125 invece di -128? ecc), questo perché alcuni valori per l'esponente sono considerati speciali, uno rappresenta $+\infty$, uno $-\infty$ ed infine uno comunica che i numeri che stiamo analizzando sono [[#Numeri Sottonormalizzati]].

La IEEE sta lavorando alla standardizzazione dei numeri reali in virgola mobile su 8 bit, ma è possibile che float8 abbia diverse versioni, con K = 3,4 o 5, quest'ultima sarebbe nell'interesse della comunità del [[machine learning]].
# Approssimazione
In genere ci viene fornito $x \notin F(\beta,m,L,U)$, in particolare ricadiamo in una di queste tre possibilità:
1. $|x|>\beta^u(1-\beta^{-m})$ : ==overflow== 
2. $|x| < \beta^{L-1}$ : ==underflow== 
3. $\beta^{L-1} \leq |x| \beta^U(1-\beta^{-m})$ : ==arrotondamento== 

Definiamo allora una funzione tale che: $RD: R \to F(\beta,m,L,U)$ e $RD(x)=\text{uno dei due numeri di macchina vicini}$ 
![[rounding1.svg|400]]
### Troncamento Round-Down
$$
\begin{matrix}
Tr(x)=\lfloor x \rfloor \\ \\

\lfloor x \rfloor =sgn(x)\cdot \beta^e \sum_{j=1}^m\alpha_{j}\beta^{-j}
\end{matrix} 
$$
vale la seguente disuguaglianza:
$$
\text{errore}: \quad |Tr(x)-x|\leq \beta^{e-m}
$$
### Troncamento Round-Up
$$
\begin{matrix}
Up(x)=\lceil x \rceil  \\ \\
\lceil x \rceil =sgn(x)\cdot \beta^e \cdot\left( \sum_{j=1}^m \alpha_{j}\beta^{-j}+\beta^{-m} \right)
\end{matrix}
$$
### Round-to-Nearest
$$
\begin{cases}
\lceil x \rceil  & \text{se}  & \alpha_{m+1}\geq \frac{\beta}{2} \\
\lfloor x \rfloor  & se & \alpha_{m+1}<\frac{\beta}{2}
\end{cases}
$$
vale quanto segue:
$$
\begin{matrix}
1. & \text{errore} : & |Rn(x)-x|\leq \frac{\beta^{e-m}}{2} \\ \\

2.  & |x-Rn(x)|=\min |z-x| & z\in F(\beta,m,L,U)
\end{matrix}
$$
# Precisazioni sui numeri in virgola mobile
- ==Errore Assoluto==: $\delta_{x}=x-Rn(x)$
- ==Errore Relativo==: $\epsilon_{x}=\frac{x-Rn(x)}{x}$ 
- ==Precisione di Macchina==: $U=\beta^{1-m}$ 
	- single precision: $U\approx 10^{-8}$
	- double precision: $U\approx 10^{-16}$ 
I numeri in virgola mobile garantiscono un errore relativo limitato in modo uniforme (salvo over/under-flow).
### Implementazione
|                      | $\beta$ | $m$ | $L$    | $U$   | segno | mantissa | esponente | U          | Memoria |
| -------------------- | ------- | --- | ------ | ----- | ----- | -------- | --------- | ---------- | ------- |
| Precisione Singola   | 2       | 24  | -125   | 128   | 1     | 23       | 8         | $10^{-8}$  | 32      |
| Precisione doppia    | 2       | 53  | -1021  | 1024  | 1     | 52       | 11        | $10^{-16}$ | 64      |
| Precisione Quadrupla | 2       | 113 | -16381 | 16384 | 1     | 112      | 15        | $10^{-32}$ | 128     |

# Numeri Sottonormalizzati
Per numeri compresi in $[0;\beta^{L-1}]$, possiamo utilizzare la sottonormalizzazione, ovvero tramite un valore speciale di $e$ indichiamo alla macchina che il numero è sottonormalizzato, e questa lo intenderà diversamente:
significa che implicitamente $e=L$ e $\alpha_1=0$ e si usano le restanti cifre della Mantissa.

Così facendo ottengo valori equispaziati fra $0$ e $\beta^{L-1}$ con distanza $\beta^{L-m}$.
Notiamo però che così facendo, più ci avviciniamo allo $zero$ e più aumenta l'errore relativo $\epsilon_{x}$.
![[sottonormalizzati1.svg|500]]
