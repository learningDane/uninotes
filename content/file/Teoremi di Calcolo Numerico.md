#uni 
# Algebra
>[!Theorem] Algebra Lineare, no dim
>$$
>\begin{matrix}
>A \text{ e } A^T \quad \text{sono simili}
>\\
>A=A^H \quad \text{Hermitiana}
>\\
>AA^H=A^HA \quad \text{Normale}
>\\
>AA^H=A^HA=I \quad \text{Unitaria}
>\\
>A^T=A^{-1} \quad \text{Ortogonale}: \det(A)=\pm 1,\quad \text{unitaria}
>\\
>\text{Simili} \iff \text{stesso polinomio caratteristico}
>\\
>Av=\lambda v,\quad (A-\lambda I)v=0
>\\
>w^TA=w^T\lambda,\quad w^T(A-\lambda I)=(A-\lambda I)^Tw=0
>\\
>A\text{ Simmetrica} \implies v=w
>\\
>||A||_1=\max _i\sum_j|A_{ji}| \quad \text{max somma valori colonne}
>\\
>||A||_\infty=\max _i\sum_j|A_{ij}| \quad \text{max somma valori righe}
>\\
>||v||_2=\sqrt{\sum|v_i|^2}
>\\
>||A||_2=\sqrt{\rho(AA^H)}
>\\
>||A||_F=\sqrt{\sum_{i,j}|A_{ij}|^2}
>\end{matrix}
>$$

>[!Theorem] Teorema di diagonalizzabilità, no dim
>A è diagonalizzabile se e solo se la molteplicità algebrica è uguale alla molteplicità geometrica per ogni autovalore.

> [!Theorem] Teorema Binett Cauchy, no dim
> con $A\in C^{n \times m}\cdot B\in C ^{m \times n}$:
> $$
> \det(AB)=\begin{cases}
> 0,& m\gt n
> \\
> \det(A)\cdot \det(B), & m=n
> \\
> *, & m\leq n
> \end{cases}
> $$
> $*$: dato dalla somma tra il prodotto tra tutti i minori di ordine massimo ($m$) di $A$ e tra il prodotto tra tutti i minori di ordine massimo ($m$) di $B$.

> [!Theorem] Teorema Rouché-Capelli, no dim
> Un sistema $A^{m\times n}x=b$ ammette almeno una soluzione se $\text{rank}(A)=\text{rank}(A|B)$, in particolare ammette una unica soluzione se $\text{rank}(A)=n$ (rango pari al numero di incognite), infinite soluzioni altrimenti.

> [!Theorem] Teorema Spettrale, no dim
> data una matrice hermitiana $A=A^H\in \mathbb C^{n\times n}$, essa rispetta:
> 1. $A$ è diagonalizzabile
> 2. $A$ ha autovalori reali
> 3. è possibile scegliere una base di autovettori che sia unitaria (o ortonormale nel caso reale). Ovvero esiste una matrice $V$ unitaria ($VV^H=V^HV=I$) tale che $V^HAV=\text{diag}\{\lambda_1,...,\lambda_n\}$ 

> [!Theorem] Teorema equivalenza norme, no dim
> Date due norme vettoriali generiche $||x||_p$ e $||x||_q$​, esistono sempre due costanti reali e positive $\alpha$ e $\beta$ tali che per ogni vettore $x$ valga la seguente doppia disuguaglianza:
> $$
> \alpha ||x||_p​ \leq ||x||_q​ \leq \beta ||x||_p​,\quad \forall x∈\mathbb C^n
> $$
> quindi per esempio se una successione converge ad un limite in una determinata norma, essa convergerà allo stesso limite in qualsiasi altra norma equivalente.

> [!Theorem] Teorema di Hirsch, no dim
> $$
> \rho(A)\leq ||A||
> $$
> rispetto ad una qualsiasi norma $|| \cdot||$.

> [!Theorem] ==1º Teorema di Gershgorin==
> Ogni autovalore di una matrice appartiene all'unione dei suoi dischi di Gershgorin.

> [!Theorem] 2º Teorema di Gershgorin, no dim
> Se ci sono $N$ dischi con intersezione non vuota, l'unione tra questi $N$ dischi contiene $N$ autovalori.

> [!Theorem] 3º Teorema di Gershgorin, no dim
> In una matrice irriducibile se un autovalore si trova sul bordo dell'unione di tutti i dischi, si trova sul bordo di ogni singolo disco.

>[!Theorem] Corollari dei teoremi di Gershgorin, no dim
>- $A$ e $A^T$ hanno gli stessi autovalori, si può quindi prendere come regione dove stanno gli autovalori l'intersezione dell'unione dei loro dischi di gershgorin
>- se una matrice è a predominanza diagonale forte allora è non singolare
>- se la matrice è a predonominanza diagonale debole ed è irriducibile, allora è non singolare
>- in una matrice reale, se un disco contiene un autovalore complesso, deve anche contenere il suo coniugato -> un disco isolato di una matrice reale non può contenere autovalori complessi
>- se una matrice ha tutti i dischi disgiunti, allora ha tutti autovalori distinti, quindi è *diagonalizzabile*.

> [!Theorem] ==Teorema di Riducibilità==
> Una matrice è riducibile (per permutazione) se e solo se il suo grafo associato non è fortemente connesso.
> Un grafo è fortemente connesso se e solo se da ogni suo nodo è possibile raggiungere qualsiasi altro nodo seguendo un cammino orientato.

# Calcolo Numerico

## Misc

> [!Theorem] Teorema della rappresentazione, no dim
> La rappresentazione in virgola mobile è unica se:
> $$
> \begin{matrix}
> \text{dati} \quad \beta\in N, \beta >1, x \in R \quad \text{e} \quad x \neq 0 \\
> \text{Allora} \quad \exists \quad \text{ed è unica la rappresentazione:}  \\
> x=\text{segno}(x)\cdot \beta ^ e \cdot \sum_{j=1}^\infty \alpha_j \cdot \beta^{-j} \quad \text{tale che}  \\
> 1. \quad \alpha_{i} \neq 0 \\
> 2. \quad \nexists k \in N:\alpha_{j}=\beta -1 \quad\forall j>k
> \end{matrix}
> $$

> [!Theorem] Teorema di Condizionamento, no dim
> Teorema per la maggiorazione dell'errore inerente relativo sulla soluzione $x$ di un sistema lineare $Ax=b$.
> 
> Sia $x$ la soluzione esatta del sistema $Ax=b$, sia la matrice perturbata $A+\delta A$ non singolare, allora vale:
> $$
> \epsilon_\delta=\frac{||\delta x||}{||x||}\leq \frac{\mu(A)}{1-\mu(A)\frac{||\delta A||}{||A||}}\left( \frac{||\delta A||}{||A||} +\frac{||\delta b||}{||b||}\right)
> $$
> caso semplificato, perturbazione solo su $b$:
> $$
> \epsilon_\delta=\frac{||\delta x||}{||x||}\leq\mu(A)\frac{||\delta b||}{||b||}
> $$

## Sistemi lineari

> [!Theorem] Teorema di convergenza dei metodi iterativi di punto fisso, no dim
> Un metodo iterativo di punto fisso converge per ogni vettore $x^{(0)}$ se e solo se la sua matrice di iterazione $B$ è convergente, ovvero ha raggio spettrale minore di $1$.

> [!Theorem] ==Teorema di convergenza di Jacobi e Gauss Seidel== 
> Il metodo di Jacobi e il metodo di Gauss Seidel risultano convergenti se la matrice $A$ del sistema è a predominanza diagonale forte, oppure se è a predominanza diagonale debole ed irriducibile.

> [!Theorem] Teorema di convergenza di Jacobi e Gauss-Seidel con matrice tridiagonale, no dim
> Se A è una matrice tridiagonale e se è diagonalmente dominante forte oppure se è diagonalmente dominante debole ed irriducibile (ogni elemento sulle codiagonali è diverso da 0), allora i metodi di Jacobi e Gauss-Seidel convergono e vale:
> $$
> \rho(H_{GS})=\rho^2(H_J)
> $$
> quindi Gauss Seidel converge più velocemente di Jacobi.

## Sistemi rettangolari

> [!Theorem] ==Teorema di esistenza e unicità delle soluzione delle equazioni normali==
> Il sistema delle equazioni normali $A^HAx=A^Hb$ ha sempre soluzione, la soluzione è unica se e solo se $A$ ha rango massimo.

>[!Theorem] Teorema di esistenza della fattorizzazione QR, no dim
>Per ogni matrice esiste sempre una fattorizzazione QR, ma non è mai unica.

## Interpolazione

> [!Theorem] Teorema determinante della matrice di Vandermonde, no dim
> Il determinante della matrice di Vandermonde è:
> $$
> \det(V)=\prod_{0\leq i \lt j \leq k}(x_j-x_i)
> $$
> con $k$ grado del polinomio. Quindi se $x_i\neq x_j \forall i\neq j$ allora il determinante è diverso da zero.

>[!Theorem] ==Teorema di esistenza ed unicità del polinomio interpolante==
>Dati $k+1$ punti reali distinti $(x_i,y_i)$, esiste è ed unico il polinomio $P_k(x)$ di grado al più $k$ che vale $P_k(x_i)=y_i \quad \forall i=0,1,\dots,k$.

> [!Theorem] Teorema di errore di interpolazione polinomiale, no dim
> Presi i $k+1$ punti $x_0,\dots,x_k$ diversi tra loro, sia $f:\mathbb R \to \mathbb R, \quad f\in C^{k+1}(I)$ con $I$ intorno contenente i punti $x_i$. Se $p_k(x)$ è un polinomio di grado al più $k$ che interpola i punti $(x_i,f(x_i))$, allor vale:
> $$
> \text{errore}=f(x)-p_k(x)=\frac{f^{(k+1)}(\xi)}{(k+1)!} \prod_{j=0}^k(x-x_j)
> $$
> per un certo $\xi$ compreso tra il minimo ed il massimo punto dato $x_i$.

> [!Theorem] Teorema di Faber, no dim
> Non esiste alcuna scelta dei nodi di interpolazione che garantisca la convergenza dell’interpolazione polinomiale per tutte le funzioni continue.
> 
> Qualunque sia il metodo con cui scegli i nodi, si può sempre trovare una funzione continua per cui l’interpolazione polinomiale fallisce.

## Integrazione

> [!Theorem] Teorema di unicità della formula Gaussiana, no dim
> Il sistema non lineare:
> $$
> \begin{cases}
> a_0+a_1+\dots +a_n = m_0
> \\
> a_0x_0+\dots a_nx_n=m_1
> \\ \vdots \\
> a_0x_0^{2n+1}+\dots +a_nx_n^{2n+1}=m_{2n+1}
> \end{cases}
> $$
> ammette sempre un'unica soluzione per ogni scelta di $[a,b],n,\rho(x)$, e l'unica formula di quadratura che verifica questo sistema si dice **formula Gaussiana**, e ha grado di precisione $2n+1$ su $n+1$ nodi.

> [!Theorem] Teorema di Peano, no dim
> Data una funzione derivabile $n+1$ volte ($f(x)\in C^{n+1}$), con $m$ grado di precisione della formula di quadratura $J_n$, allora l'errore $E_n$ si può scrivere come:
> $$
> E_n(f)=I(\rho,f)-J_n(f)=\frac{1}{m!}\int_a^bf^{(m+1)}(t)\cdot G(t)dt
> $$
> dove $G(t)$ è detto **Nucleo di Peano** e vale:
> $$
> G(t)=E_n(s_m(x-t))=I(\rho\cdot s_m(x-t))-J_n(s_m(x-t))
> $$
> e la $s_m(x)$ è:
> $$
> s_m(x)=\begin{cases}
> x^m, &x \gt 0
> \\
> 0, & x \leq 0
> \end{cases}
> $$

## Sistemi non lineari

> [!Theorem] Teorema di errore del metodo delle secanti, no dim
> Se $f\in C^2([a,b])$ ammette radice, allora il metodo converge localmente con ordine:
> $$
> p=\frac{1+\sqrt{5}}{2}>1
> $$
> ovvero solitamente risulta in un errore migliore del lineare ma peggiore del quaddratico.

> [!Theorem] ==Teorema di convergenza locale==
> Se si ha un intervallo $I\subset R$, con $\alpha \in I$ e $\phi(\alpha)=\alpha$ e $\phi \in C^1(I)$ ed esiste $\rho \in \mathbb R^+$ tale che:
> $$
> |\phi'(x)|\lt 1,\neq 0\quad \forall x\in[\alpha-\rho,\alpha+\rho]
> $$
> Allora:
> $$
> \begin{matrix}
> 4. & \forall x_0\in[\alpha-\rho,\alpha+\rho] \implies x_n\in[\alpha-\rho,\alpha+\rho]
> \\
> 5. & \forall x_0 \in[\alpha-\rho,\alpha+\rho] \implies \lim_{n\to +\infty} x_n=\alpha
> \\
> 6. & \alpha \text{ è l'unico punto fisso di } \phi(x) \text{ in } [\alpha-\rho,\alpha+\rho]
> \end{matrix}
> $$

>[!Theorem] ==Teorema di convergenza superlineare==
> La successione $\{x_n\}$ converge con ordine $p \geq 1$ ad $\alpha$ se è solo se vale:
> $$
> \phi'(\alpha)=\phi''(\alpha)=...=\phi^{(p-1)}(\alpha)=0, \quad \phi^p(\alpha)\neq 0
> $$

>[!Theorem] Teorema di convergenza in un intervallo, no dim
>Se $\phi(x) \in C^1([a,b])$ e:
>$$
>\begin{matrix}
>7. & |\phi'(x)|<1, \quad \forall x\in [a,b]
>\\
>8. & \phi(x) \in [a,b], \quad \forall x\in [a,b]
>\end{matrix}
>$$
>allora $\phi(x)$ converge su $[a,b]$.

> [!Theorem] ==Teorema convergenza locale superlineare di Newton==
> Se $\alpha$ è radice *semplice* e $f\in C^2([a,b])$ allora il metodo di Newton converge localmente con ordine $p\geq 2$.
> In particolare se $f''(\alpha)\neq 0 \implies p=2$, altrimenti se $f''(\alpha)=0 \implies p>2$.

> [!Theorem] Teorema di convergenza globale per Newton (tramite studio della concavità), no dim
> Se $\alpha \in [a,b]$ è radice *semplice* di $f\in C^2([a,b])$ e $f,f''$ sono di segno costante su $[a,b]$, il metodo di Newton converge **globalmente** in maniera superlineare ($p\geq 2$) $\forall x_0$ che verifica $f(x_o) \cdot f''(x_0) \gt 0$.

> [!Theorem] Teorema convergenza locale multivariabile ($\mathbb R^m$), no dim
> TLDR: un metodo iterativo multivariabile converge ad $\alpha$ radice se $\rho(J_\phi(\alpha))<1$, se il raggio spettrale è 0 converge superlinearmente.
> 
> Sia $\phi(x)$ continua in un intorno $\Omega\subset \mathbb R^m$ con $\alpha \in \Omega$ tale che $\phi(\alpha)=\alpha$, se:
> $$
> \rho(J_\phi(\alpha))\lt 1
> $$
> allora $\exists \delta \gt 0$ tale che $\forall x^{(0)} : |x^{(0)}-\alpha|_2 \lt \delta$ in cui la successione $x^{(n+1)}=\phi(x^{(n)})$ converge ad $\alpha$, ed $\alpha$ è l'unico punto fisso di $\phi$ in $\{ z\in \mathbb R^m:|z-\alpha|_2 \lt \delta \}$.
> 
> Ovvero se per una qualsiasi norma si trova $|J_\phi(\alpha)|\lt 1$ allora il metodo converge localmente.
> 
> se $\rho(J_\phi(\alpha))=0$ il metodo converge superlinearmente ($p \geq 2$). 

> [!Theorem] Teorema convergenza locale del metodo di Newton-Raphson, no dim
> Se $J_f(\alpha)$ è non singolare, allora esiste un intorno di $\alpha$ tale che per ogni $x^{(0)}$ nell'intorno la successione generata dal metodo a partire da $x^{(0)}$ converge superlinearmente, poiché vale:
> $$
> |x^{(n+1)}-\alpha|_2\leq \beta|x^{(n)}-\alpha|_2^2
> $$

## Autovalori

> [!Theorem] ==Teorema della convergenza del metodo delle potenze==, dimostrazione per matrici hermitiane
> data $A=A^H \in \mathbb C ^{n \times n}$ hermitiana (quindi diagonalizzabile) con autovalori: $|\lambda_1|\gt|\lambda_2|\geq |\lambda_3| \geq ... \geq |\lambda_n|\gt 0$ e consideriamo la successione:
> $$
> \begin{cases} 
> z^{(0)}=z
> \\
> z^{(k+1)}=Az^{(k)}=A^{k+1}z^{(0)}=A^{k+1}z
> \end{cases}
> $$
> se $h\in \{1,...,n\}:v^{(1)}_h\neq 0$ e $z^{(0)} \in \mathbb C^n$ è tale che: 
> $$
> \left[ V^{(1)} \right]^H z^{(0)}\neq 0 \quad \text{(non ortogonali)}
> $$
> allora la successione è tale che:
> $$
> \lim_{k \to +\infty} \frac{z^{(k)}}{z^{(k)}_h}=\tilde v^{(1)}
> $$
> e per l'autovalore vale:
> $$
> \lim_{k\to +\infty}\frac{\left[ z^{(k)} \right]^HAz^{(k)}}{\left[ z^{(k)} \right]^Hz^{(k)}}=\lambda_1
> $$

> [!Theorem] Teorema di validità del metodo QR per gli autovalori, no dim
> Metodo QR: $A_{k+1}=Q^H_kA_kQ_k$.
> Presa $A\in R^{n \times n}$ e supposto $|\lambda_1|\lt |\lambda_2| \lt ... \lt |\lambda_n|$ allora:
> $$
> \lim_{n\to \infty}A_k=T=\begin{pmatrix} t_{11} & ... & t_{1n} \\ & \ddots & \vdots \\ 0 & & t_{nn} \end{pmatrix}
> $$
> dove i blocchi $T_{jj}$ sono $1\times 1$ per autovalori reali e $2 \times 2$ per autovalori complessi coniugati.
