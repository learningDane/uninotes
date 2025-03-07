#uni 
Calcolo Numerico $\equiv$ Analisi Numerica (numerical analisys): Lo studio degli algoritmi per problemi di matematica che riguardano il continuo e/o grandi moli di dati.
"**Matematica del Continuo**"= i dati con cui abbiamo a che fare sono basati su numeri reali.

Sono necessarie approssimazioni per due motivi:
1. rappresentare oggetti matematici che richiedono infiniti parametri
2. Quasi sempre non si può trovare la soluzione con un numero finito di operazioni elementari.
Quindi abbiamo:
1. Errori a monte (nei dati)
2. Errori di approssimazione

Come interagiscono gli errori con l'algoritmo?
ciò dipende dal fatto che gli algoritmi possono essere:
- Stabili: se commetto un errore ragionevole in partenza ottengo un errore ragionevole alla fine
- Instabili
e anche dal ___Condizionamento del problema___.
Altre domande:
- quanto in fretta convergono gli algoritmi?
- Quale costo computazionale hanno?
- Che accuratezza hanno?
# Richiami di Algebra Lineare
La maggior parte dei dati che tratteremo saranno vettori del tipo $x\in\mathbb{C}^n\quad con\quad n>1$. In questo contesto sono fondamentali le [[Matrici]] perché rappresentano applicazioni (funzioni) lineari in __modo univoco__.
Poi ci servirà:
- Def __Applicazione Lineare__: 
	una app. lin. è una $f :\mathbb{C}^n \to \mathbb{C}$ t.c. $f(v_1+v_2) = f(v_1) + f(v_2)$ e $f(λv)=λf(v)$.
- Def __Lineare Indipendenza__:
	un sottoinsieme del vettore in esame $v_1,\cdots,v_s\in \mathbb{C}^n\quad con\quad(s\leq n)$ si dice linearmente indipendente se $\sum^s_{j=1}c_j\cdot v_j=0,\quad c_1,\cdots,c_s\in \mathbb{C}\Longleftrightarrow c_1=c_2=\cdots=c_s$ . Nel caso $s=n$ si dice che il sottoinsieme $v_1,\cdots,v_s$ è base di $\mathbb{C}^n$.
- Def di __Prodotto Scalare__
	riferimento a [[Vettori#Operazioni tra vettori]]. Curiosità il Prodotto Scalare costa $n-1$ somme e $n$ prodotti perciò $o(n)$.