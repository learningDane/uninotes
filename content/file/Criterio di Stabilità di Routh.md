#uni 
Questo criterio è applicabile su sistemi [LTI](sistema%20LTI.md) e SISO.

Data una generica equazione caratteristica:
$$
a_n \cdot s^n+a_{n-1} \cdot s^{n-1}+...+a_1 \cdot s^1+a_0=0
$$
- con $a_n>0$ (basta cambiare di segno)
- senza ritardi di tempo $e^{-\pi \tau}$, in caso contrario approssimiamo a polinomio: $\frac{1-\frac{\tau}{2}s}{1+\frac{\tau}{2}s}$
>Il sistema associato è stabile se tutti gli $n+1$ elementi della prima colonna della tabella di Routh hanno lo stesso segno.

Per $n \leq 2$ questo si riduce alla ___regola di cartesio___: gli tutti gli $n+1$ coefficienti $a_i$ hanno lo stesso segno.
# Tabella di Routh
$$
\begin{array} {c|cc}
n & a_n & a_{n-2} & a_{n-4} & ... \\
n-1 & a_{n-1} & a_{n-3} & a_{n-5} & ... \\
n-2 & \gamma_{3,1} & \gamma_{3,2} & \gamma_{3,3} & ... \\
n-3 & \gamma_{4,1} & \gamma_{4,2} & ... \\
... & ... & ... \\
0 & \gamma_{n+1,1}
\end{array}
$$
con:
$$
\gamma_{i,j}=\frac{-
\begin{vmatrix} \gamma_{i-2,1}  & \gamma_{i-2,j+1} \\
\gamma_{i-1,1}  & \gamma_{i-1,j+1}
\end{vmatrix}
}{\gamma_{i-1,1}}
$$
# Teoremi Formali
>Primo Teorema di Routh:
>Condizione necessaria e sufficiente perché tutte le radici dell'equazione caratteristica abbiano parte reale negativa è che tutti gli elementi della prima colonna della tabella di Routh siano positivi e non zero.

---

>Secondo Teorema di Routh:
>Se qualche elemento della prima colonna della tabella di Routh è negativo, il numero di radici con parte reale positiva è uguale al numero di cambi di segno dei coefficienti della prima colonna.

# Casi singolari
### Termine Pivot Nullo
Quando otteniamo un termine pivot nullo abbiamo due possibilità: trasliamo la relativa riga a sinistra oppure inseriamo al posto dello zero un $epsilon$, un numero quasi zero (a fine calcoli per determinare il segno facciamo il limite di $epsilon$ che tende a $0^+$).
### Riga di soli zeri
Se ottengo una riga di soli zeri sicuramente il sistema non è asintoticamente stabile, con i metodi che seguono possiamo verificare che sia stabile marginalmente o instabile.

>Solo i casi di ___simmetria quadrantale___ portano a righe di tutti zeri. <<<<<<<<<<<<
##### Metodo dell'equazione ausiliaria
1. Considero la riga precedente
2. costruisco la sua equazione (prendo solo esponenti pari o dispari a seconda del grado della riga)
3. ne trovo le radici, queste sono le radici del sistema sulle quali la tabella non mi ha dato informazioni
Se trovo radici complesse il sistema oscilla ad una pulsazione $w$ pari alla parte immaginaria della radice.
##### Metodo della derivata
1. Scrivo l'equazione ausiliaria $q(s)$ della riga precedente
2. derivo $q(s)$ in $s$ 
3. sostituisco il polinomio ottenuto nella riga di soli zeri