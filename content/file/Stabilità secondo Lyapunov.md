#uni 
>Consideriamo le conseguenze sul movimento del sistema di un'incertezza sul valore iniziale dello stato, con l'ipotesi di ingressi fissi e noti.

Un sistema si dice ==asintoticamente stabile== se a partire da piccole variazioni dello stato iniziale ottengo piccole variazioni del movimento dello stato, che si annullano eventualmente per tempi abbastanza lunghi.

___Definizione___:
Preso un ingresso costante $u(t)=\overline{u}$ corrispondente ad uno stato di equilibrio $\overline{x}$, consideriamo un movimento perturbato ottenuto sempre da $u(t)$ ma a partire da uno stato iniziale $x_{0}$ invece di $\overline{x}$,
Definiamo uno stato di equilibrio $\overline{x}$ ==stabile== se $\forall \epsilon >0$, esiste $\delta >0$ tale che per tutti gli $x_{0}$ che soddisfano $||x_{0}-\overline{x||} \leq \delta$ il movimento del sistema rimane vicino allo stato di equilibrio ed in particolare si ha $||x(t)-\overline{x}||\leq \epsilon \quad,\quad t\geq_{0}$.

![[equilibriostabile1.svg]]

___Definizione___:
Uno stato di equilibrio è ==asintoticamente stabile== se $\forall \epsilon >0 \exists \delta>0 \text{ tale che } \forall x_{0}:||x_{0}-\overline{x} || \leq \delta$ si ha: $||x(t)- \overline{x}|| \leq \epsilon \quad, \quad t \geq 0$ e inoltre: $\lim_{ t \to \infty } ||x(t)- \overline{x}||=0$. 