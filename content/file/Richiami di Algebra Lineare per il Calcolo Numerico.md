#uni 
La maggior parte dei dati che tratteremo saranno vettori del tipo $x\in\mathbb{C}^n\quad con\quad n>1$. In questo contesto sono fondamentali le [[Matrici]] perché rappresentano applicazioni (funzioni) lineari in __modo univoco__.
Poi ci servirà:
- Def __Applicazione Lineare__: 
	una app. lin. è una $f :\mathbb{C}^n \to \mathbb{C}$ t.c. $f(v_1+v_2) = f(v_1) + f(v_2)$ e $f(λv)=λf(v)$.
- Def __Lineare Indipendenza__:
	un sottoinsieme del vettore in esame $v_1,\cdots,v_s\in \mathbb{C}^n\quad con\quad(s\leq n)$ si dice linearmente indipendente se $\sum^s_{j=1}c_j\cdot v_j=0,\quad c_1,\cdots,c_s\in \mathbb{C}\Longleftrightarrow c_1=c_2=\cdots=c_s$ . Nel caso $s=n$ si dice che il sottoinsieme $v_1,\cdots,v_s$ è base di $\mathbb{C}^n$.
- Def di __Prodotto Scalare__
	riferimento a [[Vettori#Operazioni tra vettori]]. Curiosità il Prodotto Scalare costa $n-1$ somme e $n$ prodotti perciò $o(n)$.
- [[Matrici]]:
	__Osservazioni:__
	Le op tra matrici sono differiscono anche per ordine delle operazioni. 2 op equivalenti potrebbero avere costo computazionale diverso!!
	Inoltre è vera questa serie di implicazioni $$\begin{array}ddet(A)\neq 0,\ A\in\mathbb{C}^{n\times n}\Longleftrightarrow rango(A)=n\Longleftrightarrow le \ colonne \ di \ A \ sono \ lin.\ indipendenti\Longleftrightarrow \\ \Longleftrightarrow le \ colonne \ di \ A \ formano \ una\ base\ di \ \mathbb{C}^n \Longleftrightarrow \exists A^{-1} \end{array}$$

- [[Teorema di Binet-Cauchy]]
- [[Sistema Lineare]]:
	__Osservazioni:__
	Nel caso $m=n$ ($m$ eq. in $n$ incognite) se $det(A)\neq 0$ quindi $(rango(A)=n)$ la soluzione di $Ax=b$ è __unica__ $\forall b\in \mathbb{R}^n \longrightarrow x=A^{-1}\cdot b$
- [[Teorema di Rouché-Capelli]] 
- [[Regola di Cramer]]