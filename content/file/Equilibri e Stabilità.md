#uni 
Cerchiamo ora come arrivare ad una forma lineare senza l'utilizzo di ipotesi semplificative.
$$
\large
\begin{matrix}
\text{Dato} \quad \dot{x} =f(x,u) \\
\text{dato un segnale di ingresso} \quad u(t)  \\
\text{uno stato } \overline{x} \text{ si dice di equilibrio se}  \\
f(\overline{x},u) =\dot{x}=0
\end{matrix}
$$
# Linearizzazione attorno ad uno stato di equilibrio
- partendo da una forma standard
- sistema stazionario (ovvero non funzione del tempo), per semplicità
- ingresso $\overline{u}$ e stato di equilibrio corrispondete $\overline{x}$
$$
\text{Risolviamo} \quad \dot x=0=f(\overline x, \overline{u})
$$
Definiamo inoltre due nuove variabili che rappresentano la variazione dall'equilibrio:
$$
\Delta x=\overline{x}-\dot{\overline{x} } \quad \text{e} \quad \Delta u=\overline{u}-\dot{\overline{u}}
$$

Scriviamo adesso le equazioni di stato attraverso la [[Formula di Taylor]] centrata nello stato di equilibrio e tronchiamo al primo ordine.
$$
\large
\begin{matrix}
\dot{x}=\dot{x}-\dot{\overline x} = \Delta\dot{x}=f(x,u)= \\
=f(\overline{x},\overline{u})+\frac{∂f}{∂x}|_{\begin{matrix}
x=\overline{x}\\ u=\overline{u}\end{matrix}}\Delta x+\frac{∂f}{∂u}|_{\begin{matrix}
x=\overline{x}\\ u=\overline{u}\end{matrix}}\Delta u+O(||\Delta x||^2)+O(||\Delta u||^2)
\end{matrix} 
$$
possiamo semplificare $f(\overline{x},\overline{u})$ e $O(||\Delta x||^2)+O(||\Delta u||^2)$ poiché diventano ininfluenti e possiamo ora concentrarci sulle Matrici Jacobiane (matrici di costanti che moltiplicano i termini del primo ordine):
$$
\begin{matrix}
A=\frac{∂f}{∂x}|_{\overline{x},\overline{u}}=\begin{bmatrix}
\frac{∂f_{1}}{∂x_{1}} & \frac{∂f_{1}}{∂x_{2}}  & \dots  \\
\frac{∂f_{2}}{∂x_{1}} & \frac{∂f_{2}}{∂x_{2}} & \dots \\
\dots & \dots & \dots
\end{bmatrix}
\\ \\
B=\frac{∂f}{∂u}|_{\overline{x},\overline{u}}=\begin{bmatrix}
\frac{∂f_{1}}{∂u_{1}} & \frac{∂f_{1}}{∂u_{2}}  & \dots  \\
\frac{∂f_{2}}{∂u_{1}} & \frac{∂f_{2}}{∂u_{2}} & \dots \\
\dots & \dots & \dots
\end{bmatrix}
\end{matrix}
$$
e quindi
$$
\Delta\dot{x}=\dot{x}=A\cdot \Delta x+B \cdot\Delta u
$$
E siamo tornato alla forma standard lineare $\dot{x=Ax+Bu}$.

A questo stato di equilibrio è associata una uscita di equilibrio
$$
\overline{y}=g(\overline{x},\overline{u})
$$
definendo $\Delta y$ e le relative Jacobiane trovo
$$
y=Cx+Du
$$

Quindi, ricapitolando:
- esistono diversi tipi di non linearità
- non sempre posso trovare una forma standard lineare
- mi posso ricondurre a una condizione di stabilità linearizzando
Studieremo adesso la [[Stabilità secondo Lyapunov]].