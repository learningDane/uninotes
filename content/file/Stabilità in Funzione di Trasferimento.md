#uni 
- Un sistema è stabile se i suoi Poli sono tutti nel Semipiano Reale negativo.
- Più un polo è vicino all'asse immaginario e più e lenta la risposta del sistema.
- Se vi è una coppia di poli complessi la risposta è oscillatoria.
- Gli zeri non hanno effetto sulla stabilità.
- Uno zero nel semipiano reale positivo porta ad una risposta al gradino inversa.
>Risposta al gradino di due sistemi lineari, di cui uno con zero nel semipiano reale:![[zeroInSemipianoReale.svg]]

I Poli del sistema sono un sottoinsieme delle radici dell'equazione $\det(sI-A)=0$, che coincidono con le radici dell'equazione caratteristica $\det(A-\lambda I)=0$.

>I poli della F.d.T. del sistema sono un sottoinsieme degli autovalori della matrice $A$, in particolare per ogni funzione di trasferimento $g_{i,j}(s)$, i suoi poli sono tutti e soli i poli raggiungibili da $u_i$ e osservabili da $y_j$.

Altri criteri di stabilità:
- [[Criterio di Stabilità di Routh]] 
- [[Luogo delle Radici]]
- [[Criterio di Stabilità di Bode]]
- [[Criterio di Stabilità di Nyquist]] 
# Stabilità BIBO
>Un sistema si dice BIBO stabile (bounded input, bounded output) se ad ogni ingresso limitato corrisponde una uscita limitata.

Questa definizione si applica a sistemi lineari o sistemi comunque vicini ad un punto di linearizzazione.

>Per sistemi lineari, si ha stabilitá a BIBO se e solo se i poli della FdT hanno tutti parte reale strettamente minore di $zero$.

Concludiamo quindi che la stabilitá BIBO dipende solo dalla risposta forzata.
Se un polo ha parte reale nulla il sistema presenta oscillazioni permanenti.
Un sistema che oscilla può essere stabile, anche se sicuramente non andrà a zero.
Se una FdT non ha poli ripetuti nell'origine si ha ___stabilità marginale___, ovvero la risposta ne cresce, ne scende, ne oscilla.

>Poli Multipli sull'asse immaginario rendono il sistema instabile.
# Poli Dominanti
Al di la del transitorio iniziale, l'effetto prevalente è quello dei modi più ==lenti==.

>Il ___polo dominante___ è il polo (o coppia complessa coniugata di poli) di parte reale maggiore (NON in valore assoluto).

>Sistemi a confronto in base alla posizione del loro polo dominante ![[polodominante.svg]]

