#uni 
Questo è un metodo di rappresentazione per numeri reali che risolve il problema di rappresentare $x \in R$ usando solo parametri $\in N,Z$.

Fissato $\beta > 1, \in N$, possiamo sempre trovare un certo esponente $e \in Z$ ed una successione di cifre $\{ \alpha_{j} \}_{j=1,2,..}$ tale che:
$$
x= segno(x)\cdot \beta ^e \cdot \sum_{j=1}^\infty \alpha_{j} \cdot \beta ^{-j} \quad \text{con} \quad segno(x)=\begin{cases}
1 & x >0 \\
-1  &  x<0
\end{cases}
$$
ad esempio: $3,14 = +1 \cdot 0,314 \cdot 10^1$ 

Abbiamo però un problema: questa rappresentazione presentata così ==non è unica==.

---
___Teorema di Rappresentazione___:

La rappresentazione in virgola mobile è unica se:
$$
\begin{matrix}
\text{dati} \quad \beta\in N, \beta >1, x \in R \quad \text{e} \quad x \neq 0 \\
\text{Allora} \quad \exists \quad \text{ed è unica la rappresentazione:}  \\
x=segno(x)\cdot \beta ^ e \cdot \sum_{j=1}^\infty \alpha_j \cdot \beta^{-j} \quad \text{tale che}  \\
1. \quad \alpha_{i} \neq 0 \\
2. \quad \nexists k \in N:\alpha_{j}=\beta -1 \quad\forall j>k
\end{matrix}
$$
Derivati:
1. l'unica rappresentazione che soddisfa quanto sopra si chiama ___rappresentazione in virgola mobile normalizzata___.
2. la serie $\sum_{j=1}^\infty \alpha_{j} \beta ^{-j}$ si dice ==Mantissa== e vale $\frac{1}{\beta} \leq \sum_{j=1}^\infty \alpha _j \cdot \beta ^{-1} < 1$  
3. l'intervallo di rappresentabilità è fissato dal numero di cifre dell'esponente e l'accuratezza è fissata dal numero di cifre della mantissa. 

---

__Problema__: Su un computer non possiamo utilizzare infinite cifre, dobbiamo quindi troncare la mantissa ed usare un insieme limitato per l'esponente, qui entrano in gioco i [[Numeri di Macchina]].