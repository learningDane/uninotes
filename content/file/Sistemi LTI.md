#uni 
I sistemi LTI (lineari e tempo invarianti, ovvero stazionari) sono una classe interessante di sistemi per via delle proprietà di cui godono, che rendono utile anche l'approssimazione di sistemi non lineari ad essi, proprio per via della loro facilità di studio.
# Movimento
Il movimento dello stato e dell'uscita sono descritti dalle seguenti equazioni:
$$
\begin{cases}
\dot x(t)= Ax(t)+Bu(t)  \\
y(t)=Cx(t) + Du(t)
\end{cases}
$$
### Formula di Lagrange
Per determinare lo stato relativo ad un certo ingresso possiamo utilizzare la seguente formula:
$$
\begin{matrix}
x(t)=e^{A(t-t_0)}x_{t_0}+\int_{t_0}^te^{A(t-\tau)}B\cdot u(\tau)d\tau, \quad t>0 \\
y(t)=C\cdot x(t)+D \cdot u(t)
\end{matrix}
$$
In queste equazioni possiamo individuare per ognuna un blocco dipendente dal solo stato iniziale ed uno dipendente solo dall'ingresso, questi prendono rispettivamente il nome di:
- ___movimento libero___: $x_l(t)=e^{A(t-t_0}x_{T_0}$ 
- ___movimento forzato___: $x_f(t)=\int_{t_0}^te^{A(t-\tau)}B\cdot u(\tau)d\tau$ 
# Principio di Sovrapposizione degli Effetti
Considerato il sistema LTI con istante iniziale $t_0$, siano $x′$ e $y′$ i movimenti dello stato e dell’uscita generati dall’ingresso u′ e dallo stato iniziale , e $x″$ e $y″$ i movimenti dello stato e dell’uscita generati dall’ingresso $u″$ e dallo stato iniziale . Allora, per ogni coppia di scalari $\alpha$ e $\beta$, i movimenti dello stato e dell’uscita generati dall’ingresso 
$$
u (t) = \alpha u′ (t) + \beta u″ (t)
$$
e dallo stato iniziale
$$
x_{t_0}'''=\alpha x_{t_0}'+\beta x_{t_0}''
$$
sono:
$$
\begin{matrix}
(t) = \alpha x′ (t) + \beta x″ (t) \\
(t) = \alpha y′ (t) + \beta y″ (t)
\end{matrix}
$$

In realtà, si può dimostrare che questo risultato vale indipendentemente dall’ipotesi di stazionarietà del sistema cui lo si applica, mentre è legato in maniera indissolubile all’ipotesi di linearità.
# Trasformazioni Equivalenti
Data una matrice di trasformazione $T$, non singolare[^1] e quindi invertibile, possiamo definire un cambio di variabili, con corrispondenza biunivoca:
$$
\hat{x}=Tx, \quad x=T^{-1} \hat{x} \quad(TE.1)
$$
e sostituendo nel nostro sistema standard otteniamo:
$$
\begin{matrix}
\begin{cases}
\dot{\hat{x}}(t)=\hat{A}\hat{x(t)}+\hat{B}u(t) \\
y(t)=\hat{C}\hat{x}(t)+\hat{D}u(t)
\end{cases} \\
\text{con:} \quad\hat{A}=TAT^{-1},\quad\hat{B}=TB,\quad \hat{C}=CT^{-1},\quad \hat{D}=D
\end{matrix}
$$
Questo sistema dinamico è ___equivalente___ al nostro sistema originario, nel senso che in ogni istante a parità di stato iniziale e ingresso, i movimento dello stato sono legati dalla relazione $(TE.1)$, e i movimenti dell'uscita sono identici: sono due descrizioni equivalenti del medesimo oggetto fisico.
N.B.: le matrici $A,\hat A$ sono ___simili___, quindi hanno gli stesso autovalori.
[^1]: con determinante diverso da zero
# Autovalori e Modi
Gli autovalori di $A$ sono così importanti che prendono il nome di ___Autovalori del Sistema___.

Se gli autovalori $S_i$ di $A$ sono tutti distinti, posso scegliere la matrice di tradformazione di diagonalizzazione $T_D$ e ottengo: $\hat{A}=\hat{A_D}=diag\{ S_1,S_2,...,S_n \}$ e $x_l(t)=T_D^{-1}diag\{ e^{S_1t},e^{S_2t},...,e^{S_nt} \}T_D \cdot x_0$, $y_l(t)=Cx_l(t)$.
  Ottengo quindi che $x_l(t),y_l(t)$ sono combinazioni lineari degli esponenziali $e^{S_it}$, che sono detti ==modi==.
  >N.B.: anche i termini generati dalle coppie di complessi coniugati di $A$ $S_i$ e $\overline S_i$ sono detti ___modi___.

Se invece la matrice $A$ non è diagonalizzabile, posso comunque utilizzare la forma di Jordan (solo autovalori sulla diagonale e valori unitari sulla sopradiagonale) e i ___modi___ sono della forma $t^{\eta-1}e^{S_it}$ se $S_i \in R$;
se però $S_i\in C$ allora i ___modi___ sono nella forma $t^{\eta -1}e^{\sigma_it}\sin (\omega_iT+\phi_i)$ con $1 \leq \eta \leq \text{max dim. dei miniblocchi di Jordan}$.
