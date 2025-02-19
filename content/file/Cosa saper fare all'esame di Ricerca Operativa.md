 #uni 
scrivere comandi [[MatLab]] per il TSP
piano di taglio
[[Algoritmo di Riduzione del Gap Branch and Bound]] 
[[Algoritmo di Riduzione del Gap tramite Piano di Taglio]] 
# Trucchi
### Calcolatrice ti-nspire cx cas 2
`hessian(hfunc)` con hfunc quadratica: restituisce l'hessiana di f
`eig(hfunc)` con hfunc funzione quadratica: restituisce gli autovalori della hessiana della f
`grad(hfunc)` con hfunc quadratica restituisce il gradiente di f
`h(matrix,n)` con matrix matrice M e n numero di variabili, restituisce la matrice H ([[Metodo del Gradiente Proiettato]])
`solve( [A]•[xk+t•dk]≤[b] )` poi prendi il max ed è passo massimo del [[Metodo del Gradiente Proiettato]] 
- calcolare moltiplicatori PNL: pongo a zero i moltiplicatori di vincoli NON attivi, calcolo le prime due righe, risolvo matricialmente $A^{-1} \cdot b$.  
# Precisazioni per lo scritto
1. è necessario scrivere i cammini aumentanti nell'ffek
2. nel branch and bound NON scrivere le fogli "vuote"
3. sempre meglio provare qualcosa e a malapena abbozzarlo che lasciare vuoto