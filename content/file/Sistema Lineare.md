#uni 
Un'equazione lineare è un'equazione in cui compaiono solo somme di multipli di incognite. 
$$
ax + by +\ ...\ + cz = k
$$
 Un sistema lineare è un sistema di equazioni lineari. 
$$
\begin{cases} \ ax + by = c \\ \ dx + ey = f \\ \ ... \end{cases}
$$
In generale lo possiamo descrivere in questo modo:$$Ax=b\quad con\quad A=\begin{bmatrix} a_{11}  \ \ \cdots   \ \ a_{1n}\\
\vdots \ \ \ \ \ \ \ \ \ \ \ \ \ \ \vdots \\
 a_{m1} \  \ \cdots \ a_{mm}
\end{bmatrix}\in \mathbb{C}^{m\times n} ,\quad x=\begin{bmatrix}
x_1\\
\vdots
\\ x_m
\end{bmatrix} \in \mathbb{C}^n,\quad b= \begin{bmatrix}
b_1  \\
\vdots \\
b_m
\end{bmatrix}\in \mathbb{C}^m  $$

# Sistemi Lineari Omogenei
Un sistema si dice omogeneo se il termine noto è uguale a $0$ in tutte le equazioni. Un sistema lineare può:
- avere una soluzione unica
- non avere soluzione
- avere infinite soluzioni
# Mosse di Gauss
- Aggiungere un multiplo di un'equzione a un'altra
- Moltiplicare un'equazione per uno scalare nullo
- Riordinare le equazioni
# Eliminazione Gaussiana, Algoritmo di Gauss
Applicare le 3 mosse di Gauss per semplificare un sistema di equazioni lineari.
# Matrici a Scala
Tutte le righe sono del tipo: 
$$
\begin{pmatrix} 0 \ ... \ 0 \ \ * \ \ * \ ... \ *\end{pmatrix}
$$
Dove il primo $*$ è un numero diverso da zero, e quelli dopo sono altra roba, che può anche essere $0$
Nella prima riga possono non esserci zeri iniziali.
In ogni riga c'è almeno uno zero iniziale in più della precedente.
Il primo numero non nullo prima degli zeri iniziali, si chiama ___pivot della riga___.
Il fatto fondamentale è che lavorando alla Gauss posso portare qualunque matrice in una forma a scala.
### Soluzioni
La soluzione è unica quando le righe differiscono tutte per numero $1$ zeri.
Le soluzioni sono infinite quando le righe differiscono per un numero di zeri diverso da $1$.
Le soluzioni sono impossibili quando ottengo una riga con tutti zeri nella parte dei coefficienti ed un numero diverso da zero della parte dei termini noti.
In un sistema a scala, solo le variabili che hanno un pivot hanno una soluzione unica.
### Variante di Jordan
Lavorando dal basso, dopo aver ridotto a scala possiamo mettere degli zeri sopra tutti i pivot

$$
\begin{pmatrix} 1 & 0 & 2 & 3 \\ 2 &-1 & 1 & 1 \\ 1 &-1& 3 & 0\end{pmatrix} \to \begin{pmatrix} 1 & 0 & 2 & 3 \\ 0 & -1 & -3 & -5 \\ 0 & -1 & 1 & -3 \end{pmatrix} \to \begin{pmatrix} 1 & 0 & 2 & 3 \\ 0 & -1 & -3 &-5\\0 &0&4&2 \end{pmatrix} \to \begin{pmatrix} 1&0&2&3\\0&1&3&5\\0&0&2&1\end{pmatrix}
$$
 Adesso Jordan 
$$
\begin{pmatrix} 1&0&0&2\\ 0&2&0&7\\ 0&0&2&1 \end{pmatrix}
$$
E ho risolto.