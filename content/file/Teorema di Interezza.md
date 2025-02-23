#uni 
Questo Teorema dice che:
I vertici ([[vertice]]) di un poliedro $\begin{cases} Ex=b \\ x\geq 0\end{cases}$ , con $E$ [[Problema di Programmazione Matematica a Reti non Capacitate (PLRnC)#Matrice di Incidenza della Rete]], sono a componenti intere.
# Spiegazione
Una matrice di incidenza su reti è una matrice (di dimensioni |nodi| x |archi|) che presenta su ogni colonna degli 0, UN +1 ed UN -1.
Un albero di copertura sulla rete è descritto da una sottomatrice di E quadrata di dimensioni (n-1)x(n-1).
Questa sottomatrice è quindi a sua volta composta da 0,1 e -1, e con opportune permutazioni di riga e/o colonna, può essere portata in forma triangolare inferiore con sulla diagonale +1 e -1.
Una matrice triangolare inferiore con 1 e -1 sulla diagonale ha determinante +-1.
L'indeterminatezza del segno deriva dal fatto che le permutazioni di riga e di colonna cambiano il segno del determinante.
Questo tipo di matrice è unimodulare, e le soluzioni di sistemi lineari su queste matrici producono risultati a componenti intere, per il teorema di Cramer
Ne otteniamo che le soluzioni di sistemi Ex=b con E matrice di incidenza e b a componenti intere (NOTA BENE!) sono a loro volta a componenti intere. 