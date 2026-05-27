#uni 
$$
A^{m\times n}x^n=b^m
$$

- sistema **sottodeterminato**: $m\lt n$: infinite soluzioni?
- sistema **sovradeterminato**: $m \gt n$: non esistono soluzioni?
# Sistemi sottodeterminati
Fingiamo che il sistema sia quadrato e risolviamo.
Aggiungiamo zeri sotto a A e a b
# Sistemi sovradeterminati
Risolvo, se i $m-n$ elementi in coda a $b$ sono tutti uguali a zero la soluzione esiste e la trovi guardando le prime $n$ righe.

Se invece non sono diversi da zero allora consideriamo il problema:
$$
\min||b-Ax||_2 \quad \text{oppure} \quad \min||b-Ax||_2^2
$$
- con $r=b-Ax$ vettore residuo
## Problema Lineare ai minimi quadrati
Risolviamo
$$
\min||b-Ax||_2^2=\min \sum_i ^m |r_i(x)|^2
$$
con $r(x)=||b-A\cdot x ||_2$ **vettore residuo**.

La funzione obiettivo è:
$$
\Psi(x)=(b-Ax)^T(b-Ax)
$$
Trovare i suoi punti di minimo equivale a risolvere il **sistema delle equazioni normali**: 
$$
A^TAx=A^Tb
$$
nota: nel caso complesso $A^H$ invece di $A^T$.

> [!Theorem] Teorema
> Il sistema delle equazioni normali ha soluzione sempre, inoltre la soluzione è unica se e solo se $A$ ha rango massimo, ovvero rango $n$.

Costo: $O(nm^2)$.

Metodo non stabile: mal condizionato se $\mu(A^TA)=\mu(A^2)>>1$.
### Metodo QR per problemi ai minimi quadrati