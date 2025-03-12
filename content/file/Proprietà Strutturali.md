#uni 
Le 3 proprietà strutturali di un sistema sono: la stabilità, la raggiungibilità e l'osservabilità, e sono determinate dalle matrici di struttura del sistema.
# Stabilità
Questa proprietà dipende unicamente dal movimento libero del sistema[^1], che possiamo comunque evitare di calcolare ([[Stabilità secondo Lyapunov]]).

Il movimento $\tilde{x}$ è stabile se $\forall \epsilon>0, \exists \delta >0 : \forall \delta_{x_0} \text{ per cui } ||\delta_{x_0}|| \leq 0 \text{ risulti } ||\delta_x(t)|| \leq \epsilon, t \geq 0$ 

$\tilde{x}$ è asintoticamente stabile se inoltre $\lim_{t\to \infty} || \delta_x(t)||=0$ 

___Teorema___: un movimento (o uno stato di equilibrio) di un sistema lineare stazionario è stabile, asintoticamente stabile o instabile se e solo se tutti i movimenti (o gli stati di equilibrio) del sistema sono rispettivamente stabili, asintoticamente stabili o instabili.

___Teorema___:

[^1]: [[Sistemi LTI#Formula di Lagrange]]
