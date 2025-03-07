Come il calcolo di punti in Funzioni Razionali genera errori anche nel calcolo di punti in Funzioni Non Razionali genera degli errori causati sempre dell'approssimazione di ciò che vorremmo calcolare.
# Fonti dell'Errore
1. errore dettato dall'approssimazione di $f(P_0)$ in $\tilde{f}(P_0)$, passaggio fondamentale per approssimare una FNR a una FR in particolare a un polinomio di Taylor tramite la [[Formula di Taylor]]   $\Longrightarrow$ Errore Analitico
2. [[Errori nelle Funzioni Razionali#Errore Algoritmico]]
3. [[Errori nelle Funzioni Razionali#Errore Inerente]]
# Errore Totale
Gli [[Errori nelle Funzioni Razionali#Errori Algoritmico e Inerente]] rimangono invariati, a questi va aggiunto l'[[#Errore Analitico]]:$$\large \delta_{f}=\tilde{f}_{a}(P_{1})-f(P_{0})=\delta_a+\underbrace{\tilde{f}(P_1)-f(P_1)}_{\delta_{an}}+\delta_d=\delta_a+\delta_{an}+\delta_d$$
## Errore Analitico
- Assoluto: $\delta_{an}=\tilde{f}(P_1)-f(P_1)$ , Maggiorazione: $max|\tilde{f}(P_1)-f(P_1)|$
- Relativo: $\Large \epsilon_{an}=\frac{|\delta_{an}|}{|f(P_0)|}$ , Maggiorazione: $\Large \frac{max|\tilde{f}(P_1)-f(P_1)|}{min|f(P_0)|}$
L'Errore Analitico è quell'errore derivante dall'approssimazione tramite [[Formula di Taylor]] della FNR in FN. 
__Esempio__
<<<<<<<<<<<