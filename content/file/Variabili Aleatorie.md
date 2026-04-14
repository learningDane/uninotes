#uni 
Dato un esperimento aleatorio con:
- spazio campione $\Omega$
- classe degli eventi $S$
- legge di probabilità $P(\cdot)$ 

Definiamo una corrispondenza $X(\omega)$, che associa a ciascun risultato $w$ dell'esperimento un unico numero reale.

Questa corrispondenza è detta **variabile aleatoria** se l'insieme di risultati per i quali $X(\omega) \leq a$ è un *evento*.
Posso dunque assegnare al generico evento del tipo $\{ X(\omega) \leq a \}$ una probabilità $P(\cdot)$.
# Funzione di distribuzione
Si indica con **funzione di distribuzione** di probabilità di una variabile aleatoria $X$, la funzione:
$$
\large
F_X(x)\triangleq P(\{ X \leq x \})
$$
La definizione di variabile aleatoria assicura l'esistenza della funzione di distribuzione $F_X(x)$ per ogni $x\in \Bbb R$.

> Le variabili aleatorie sono indicate con la lettera maiuscola, invece con la lettera minuscola si indica un valore reale generico ma *fissato* che identifica l'evento $\{X \leq x \}$ di cui calcola la probabilità.

## Proprietà della funzione di distribuzione

> [!theorem] Le proprietà della funzione di distribuzione:
> $$
> \large
> \begin{matrix}
> \text{I.}&:& 0 \leq F_X(x) \leq 1
> \\
> \text{II.}&:& \lim_{x\to-\infty} F_X(x)=P(\{ X \leq -\infty \})=0
> \\ && \lim_{x\to+\infty} F_X(x)=P(\{ X \leq +\infty \})=1
> \\ && \small \text{poiché}: \{X\leq -\infty\}=0 \text{ e } \{ X \leq +\infty \}= \Bbb R
> \\
> \text{III.}&:& F_X(x) \text{ è monotona non decrescente}
> \\
> \text{IV.} &:& P(x_1 \lt X \leq)=F_X(x_2)-F_X(x_1)
> \\
> \text{V.} &:&F_X(x^+)=\lim_{h \to 0^+} F_X(x+h)=F_X(x)
> \\ && \small \text{la funzione di distribuzione è continua da destra}
> \\
> \text{VI.} &:& P(\{ X=\overline x \})= F_X(\overline x ^+)-F_X(\overline x ^-)
> \\ && \small \text{Se la funzione di distribuzione presenta una discontinuità di 1 specie }
> \end{matrix}
> $$

Queste probabilità mostrano che dalla conoscenza di $F_X(\cdot)$ è possibile determinare la probabilità di un qualunque evento $\{X\in I\}$ essendo $I$ un qualunque insieme reale ottenuto come somma di intervalli dell'asse reale.

> Ovvero *la conoscenza di $F_X(\cdot)$ rappresenta una descrizione statistica completa della variabile aleatoria $X$*.

A volte ci possono essere descrizioni statistiche equivalenti ma più semplici:
- la funzione massa di probabilità, nel caso di VA discrete
- la funzione densità di probabilità, nel caso di VA continue
# Variabili aleatorie discrete
Una VA si dice *discreta* se assume un numero finito o una infinità numerabile di valori distinti $x_1, x_2,..$.
## Funzione massa di probabilità
Si indica con **funzione massa** di probabilità di una variabile aleatoria discreta $X$, la funzione:
$$
p_X(x)=P(\{X=x\})
$$
ed è diversa da zero solo in $x=x_1,x_2,...$.
### Misura della massa di probabilità di VA discrete
Definizione di massa di probabilità come limite della frequenza relativa:
$$
\large
p_X(x_i)=P(\{X=x\}) = \lim_{N\to +\infty}\frac{n(x_i)}{N}
$$
1. ripetere $N$ volte l'esperimento
2. per ogni $x_i$ definiamo il numero di volte $n(x_i)$ che tale valore si è presentato
3. per ogni $x_i$ calcolare la frequenza di presentazione: 
$$
\hat p_X(x_i)=\frac{n(x_i)}{N}
$$

## Variabile Aleatoria di Bernoulli
Una variabile aleatoria di Bernoulli è una variabile aleatoria che assume:
- il valore 1 con probabilità $p$
- il valore 0 con probabilità $1-p$
E si scrive: $X\in Bernoulli(p)$.
## Variabile Aleatoria Binomiale
Ripetiamo $N$ volte un esperimento aleatorio nel quale un certo evento $A$ (evento favorevole) si può presentare con probabilità $p$ in ciascuna prova (prove indipendenti), possiamo definire una variabile aleatoria $X$ il cui valore si identifica con il numero di volte in cui si verifica l'evento $A$ sul totale $N$ delle prove, questa variabile aleatoria è detta *numero di successi*, è di tipo *discreto* e può assumere i valori $x_k=0,1,2,...,N$ con massa di probabilità:
$$
p_X(k)=P(\{X=k\}) = \binom{N}{k}p^k(1-p)^{N-k}, \quad 0\lt p \lt 1,k=0,1,...,N
$$

Una variabile aleatoria $X\in B(p,N)$ è detta **binomiale** se è discreta, definita per valori interi $0,1,2,...,N$ e con questa massa di probabilità, e indica la probabilità che un certo evento $A$ si presenti un certo ammontare di volte $k$ sul totale $N$.
## Variabile aleatoria di Poisson
Questa variabile aleatoria assume valori diversi da zero per un valore illimitato numerabile di valori.

Una variabile aleatoria $X\in P(\Lambda)$ è detta **di Poisson** di parametro $\Lambda$ (con $\Lambda \gt 0$) se è discreta definita per valori interi positivi ed ha la seguente massa di probabilità:
$$
p_X(k)=P(\{X=k\}) = \frac{\Lambda^k}{k!}e^{-\Lambda}, \quad k=0,1,2,...
$$

Condizione di normalizzazione della massa di probabilità:
$$
\sum_{k=0}^{+\infty}p_X(k)=e^{-\Lambda}\sum_{k=0}^{+\infty}\frac{\Lambda ^k}{k!}=e^{-\Lambda}e^\Lambda=1
$$

- se $\Lambda \lt 1$ allora $p_X(k)$ è massima in $k=0$
- se $\Lambda$ non è un intero ed è maggiore di 1, allora il massimo si ha per $k$ uguale alla parte intera di $\Lambda$ 
- se $\Lambda$ è un intero ed è maggiore di 1, allora si hanno due massimi per $k=\Lambda$ e $k=\Lambda-1$ 
# Variabili aleatorie continue
Una variabile aleatoria si dice **continua** se può assumere una infinità (non numerabile) di valori, ognuno dei quali con probabilità nulla:
$$
P(\{X=x\})=0, \quad \forall x
$$

La funzione di distribuzione è continua:
$$
F_X(x^+)=F(x^-)
$$

Ed è quindi indifferente includere o escludere gli estremi:
$$
P(x_1 \lt X \lt x_2)=F_X(x_2)-F_X(x_1)
$$
## Densità di probabilità 'ddp'
Se $F_X(x)$ è derivabile, si definisce **densità di probabilità** (**ddp**) della variabile aleatoria $X$ la funzione:
$$
f_X(x)=\frac{dF_X(x)}{dx}
$$
dove:
- F distribuzione di probabilità
- f densità di probabilità

Se integro $f_X(x)$ da $-\infty$ a $+\infty$ ottengo $F_X(+\infty)-F_X(-\infty)=1-0=1$.

Se integro $f_X(x)$ da $-\infty$ a $\overline x$ ottengo $F_X(\overline x)$ 
### Proprietà della ddp
- $f_X(x) \geq 0$
- $F_X(x)=\int_{-\infty}^xf_X(\alpha)d\alpha$ 
- $\int_{x_1}^{x_2}f_X(\alpha)d\alpha=F_X(x_2)-F_X(x_1) \implies P(X\in I)=\int _I f_X(\alpha)d\alpha$ 
- $\int_{-\infty}^{+\infty}f_X(\alpha)d\alpha = F_X(\infty)-F_X(-\infty)=1$ : *Proprietà di normalizzazione*.
- $\int_{x_1}^{x_2}f_X(x)dx=P(x_1 \lt X \lt x_2)$, se pongo $x_1 = x, x_2=x+dx$: $f_X(x)dx=P(x \lt X \leq x +dx)$ e quindi $f_X(x)=\frac{P(x \lt X \leq x +dx)}{dx}$. Quindi la ddpp rappresenta la probabilità (al variare di x) che la variabile aleatoria $X$ assuma valori appartenenti all'intervallo infinitesimo $(x,x+d)$ diviso l'ampiezza infinitesima $dx$ dell'intervallo.

Misuriamo sperimentalmente la ddp di una VA passando alla frequenza relativa: se ripetiamo l'esperimento $N$ volte e contiamo il numero $\Delta n(x)$ di risultati per cui $x \lt X \leq x+ \Delta x$, si ottiene:
$$
f_X(x)\Delta x \approx P(x\lt X \leq x + \Delta x)\approx \frac{\Delta n(x)}{N}
$$
e purché $\Delta x$ sia sufficientemente piccolo e $N$ sufficientemente grande, la ddp si può ottenere come segue:
$$
f_X(x) \approx \frac{\Delta n(x)}{N \Delta x}
$$
## Variabile Aleatoria uniforme
Una variabile aleatoria $X \in U(a,b)$ è detta uniforme nell'intervallo (a,b) se la sua ddp è costante in quell'intervallo:
$$
f_X(x)=\begin{cases} \frac{1}{b-a} & \text{per } a \leq x \leq b \\0 & \text{altrove}\end{cases} \quad \text{e} \quad F_X(x)= \begin{cases} 0 & \text{per } x \lt a  \\ \frac{x-a}{b-a} & \text{per } a \leq x \leq b \\ 1 & \text{per } x \gt b\end{cases}
$$
