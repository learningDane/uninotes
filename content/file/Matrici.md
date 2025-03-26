#uni 
# Matrici e Sistemi Lineari
Ogni sistema lineare si può scrivere nella forma: 
$$
Ax=b
$$
$A_{n \times m}$ è la matrice dei coefficienti.
$x_{m \times 1}$ è il vettore colonna delle incognite.
$b_{n \times 1}$ è il vettore colonna dei termini noti.
Il sistema ha tante equazioni quante sono le righe di $A_{n \times m}$ e i termini noti $b_{n \times 1}$, ($n$).
# Notazione
Indichiamo con $M_{n\times m}$ l'insieme delle matrici con $n$ righe e $m$ colonne.
Se $A \in M_{n\times m}$ allora l'elemento che sta nella riga $i$ e colonna $j$ si indica con $A_{i \times j}$.
Se $n=1$ allora la matrice prende il nome di ___Vettore Riga___.
Se $m=1$ allora la matrice prende il nome di ___Vettore Colonna___.
Se $n=m=1$ allora la matrice è un solo numero.
# Matrici Speciali
1. __Matrice Nulla__ = matrice con tutti $0$.
2. __Matrice Identità__ $I_{n \times n}$= matrice quadrata con tutti $1$ sulla diagonale principale e $0$ altrove: $\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$ 
	   tutte le volte che moltiplico una matrice per una matrice identità, ottengo la matrice stessa.
3. Distinguiamo 2 situazioni:
	1. $A\in \mathbb{C}^{n\times n}\quad \begin{cases} Hermitiana\ A=A^H\\ AntiHermitiana\ A=-A^H \\ Unitaria\ A^H\cdot A=A\cdot A^H=I\ e\ A^{-1}=A^H\\ Normale\ A^H\cdot A=A\cdot A^H\end{cases}$
	2.  $A\in \mathbb{R}^{n\times n} \quad \begin{cases} Simmetrica\ A=A^T\\ AntiSimmetrica\ A=-A^T \\ Ortogonale\ A^T\cdot A=A\cdot A^T=I\ e\ A^{-1}=A^T\end{cases}$
## Sottomatrice
Una sottomatrice è una porzione della matrice di partenza, quindi una matrice che ha __rango__ minore rispetto alla matrice genitrice.
Il suo determinante è detto __minore__.
## Matrice di Permutazione 
Data $P\in \mathbb{R}^{n\times n}$ si dice __matrice di permutazione__ se $P$ si ottiene da $I$ permutandone (cambiandone l'ordine) le righe o le colonne.
### Proprietà
1. le matrici di permutazioni sono __ortogonali__
2. il prodotto di $A$ con $P$ mi restituisce $A$ permutata:
   - sulle __righe__ se $P$ a __sinistra__
   - sulle __colonne__ se $P$ a __destra__
# Operazioni
### Somma / Differenza

$$
A+B=\begin{pmatrix} a & b \\ c & d \end{pmatrix}+\begin{pmatrix} e & f \\ g &h \end{pmatrix} = \begin{pmatrix} a+e & b+f \\ c+g & d+h\end{pmatrix}
$$

### Moltiplicazione per uno Scalare

$$
k \cdot A = k \cdot\begin{pmatrix} a & b \\ c & d \end{pmatrix}= \begin{pmatrix} ka & kb \\ kc & kd \end{pmatrix}
$$

### Prodotto di Matrici
Moltiplico le righe della prima per le colonne della seconda

$$
A_{n \times m} \cdot B_{m \times k}= M_{n \times k} =\begin{pmatrix} a & b & c \\ d & e & f \end{pmatrix} \cdot \begin{pmatrix} g & h\\ i &j \\ k & l \end{pmatrix} = \begin{pmatrix} ag+bi+ck & ah+bj+cl \\ dg+ei+fk & dh+ej+fl \end{pmatrix}
$$
 
$$
(AB)_{i,j}= \sum_{r=1}^{m}A_{i,r}\cdot B_{r,j}
$$

###### Proprietà
1. Se le dimensioni sono compatibili il prodotto è distributivo: $(A+B)C=AC+BC$ 
2. Il prodotto si distribuisce rispetto al prodotto per una costante: $(λA)B=λ(AB)$ 
3. Il prodotto è associativo: $A(BC) = (AB)C$ 
4. Il prodotto ___NON___ è commutativo: $AB \neq BA$ e probabilmente $BA$ non si può nemmeno fare.
### Matrice Trasposta
La Matrice Trasposta $A^t$ di $A$ è la matrice che si ottiene scambiando le righe con le colonne. 
$$
(A^t)_{n\times m} = A_{m \times n} = \begin{pmatrix} a & c \\ b & d \end{pmatrix}
$$

# Determinante
Il Determinante ($\det A$ o $|A|$) è:
1. una funzione che prende in input $n$ vettori di $R^n$ e restituisce in output un numero. Se il risultato è $0$ i vettori sono ___linearmente dipendenti___.
2. funzione che prende in input una matrice $A_{n \times n}$, quindi quadrata, e restituisce un numero. 
###### Minore Complementare

$$
M_{i,j}=\det(A-i-j)
$$

###### Complemento Algebrico (o Sviluppo di Laplace)

$$
A_{i,j}=(-1)^{i+j}M_{i,j}
$$

##### Definizione Assiomatica (le proprietà)
Le Proprietà:
1. $\det I_{n \times n} = 1$
2. se tra gli $n$ vettori ce ne sono due uguali allora il $\det = 0$
3. $\det (v_1 , v_2 , λv_3 , ... , v_n) = λ\det(v_1 , ... , v_n)$ 
4. le somme escono fuori: $\det(v_1,..., v_i + v_j,...,v_n)= \det(v_1,v_i,...,v_n)+\det(v_1,v_j,...,v_n)$ 
Le proprietà 3 e 4 le posso riassumere dicendo che il determinante è una funzione lineare di ognuno degli $n$ vettori.
5. se scambio due vettori tra di loro il determinante cambia segno.
##### Determinante di una matrice 2x2

$$
\det\begin{pmatrix} a&b\\c&d\end{pmatrix}=ad-cb
$$

##### Formula Generale per il Determinante
Il Determinante di una generica matrice quadrata è la somma degli elementi di una riga (o di una colonna) moltiplicati per il loro complemento algebrico. Posta la riga $k$ con $1\leq k \leq n$ :
$$
\det(A_{n \times n})=\sum_{i=1}^na_{k,i}A_{k,i}
$$
# Rango 
Il __rango__ di una matrice è definito come il massimo numero di colonne linearmente indipendenti (che coincide con il max numero di righe linearmente indipendenti) ed è uguale all'__ordine massimo dei minori__ $\neq$ 0 nella matrice
## Proprietà
se $rango(A)=dim(Im(A)),\quad A\in \mathbb{C}^{m\times n}\quad \Rightarrow \quad Im(A)=\{y\in \mathbb{C}^{m}:y=Ax,\quad x\in\mathbb{C}^{n}\}$  
se $A\in \mathbb{C}^{n\times n}\quad rango(A)<n\quad \Longleftrightarrow \quad det(A)=0$ 
# Kernel (nucleo)
Kernel risponde alla definizione di insieme delle soluzioni di $Ax=0$, più formalmente:$$Ker(A)=\{x\in \mathbb{R}^{m\times n} :Ax=0\} $$
ecco che tramite [[Teorema di Rouché-Capelli]] vediamo che $dim(Ker(A))=n-rango(A)$ 
# Autovalori e Autovettori
Data $A\in \mathbb{C}^{n\times n}, \quad \lambda \in \mathbb{C}$ si dice __autovalore__ se $\exists \ vettore \ v\in \mathbb{C}^n,\quad v\neq 0 \ t.c. \quad Av=\lambda v$ .
In questo caso v si dice __autovettore destro__ di $A$ rispetto a $\lambda$ .
Similmente si dice __autovettore sinistro__ se vale $w^HA=\lambda w^H$.
__Osservazione__:
$w$ è autovettore sx rispetta a $\lambda \ se \ e \ solo \ se \ w$ autovalore dx per $A^H$ rispetto a $\overline{\lambda}$ :$$(w^HA)^H=A^Hw\longrightarrow (\lambda w^H)^H=\overline{\lambda}w$$ Domanda: ma $\exists$ autovalori e autovettori di una matrice?$$Av=\lambda v \longrightarrow Av-\lambda v=0 \Longleftrightarrow (A-\lambda I)v=0$$
Per [[Teorema di Rouché-Capelli]] il sistema ha soluzioni diverse dal vettore nullo $se\ e\ solo\ se\ det(A-\lambda I)=0 \Rightarrow$ __Equazione Caratteristica__ .
Ne segue che gli __autovalori sono le radici di questa equazione!!__ $$det(A-\lambda I)=\overbrace{c_0+c_1\lambda + \cdots+c_n\lambda^n}^{\Large{Polinomio}  \ Caratteristico}$$
se prendiamo in considerazione il Polinomio Caratteristico troviamo che:$$p_x(A)=det(A-\lambda I) = (-1)^n\lambda^n+ (-1)^{n-1}\sigma_1\lambda^{n-1}+\cdots-\sigma_{n-1}\lambda+\sigma_n$$
dove:
- $\sigma_j$ è la somma dei minori delle sottomatrici principali di ordine j
- considerando l'affermazione di sopra $\sigma_1=\sum^n_{j=1}a_{jj}=$ traccia di $A$
- di conseguenza $\sigma_n=det(A)=\prod^n_{j=1}\lambda_j$ , se $det(A)=0 \Longleftrightarrow \exists\lambda=0$ 
## Molteplicità
Un autovalore ha molteplicità algebrica $\alpha(\lambda)=k$  se $k$ è la sua
---------finire