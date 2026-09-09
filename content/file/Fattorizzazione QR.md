#uni 
Voglio trovare una fattorizzazione tale che $A=QR$, con $Q$ unitaria e $R$ triangolare superiore rettangolare, con $m-n$ righe di zeri in fondo.

Matrice di Householder associata al vettore $v$:
$$
\tilde v=\begin{pmatrix}
v_1\pm ||v||_2 \\ v_2 \\ \vdots \\ v_m
\end{pmatrix}
$$
quindi
$$
H_v=I-2\frac{\tilde v \tilde v^H}{||\tilde v||_2^2}
$$

# Fattorizzazione
$H_1=H_{a_1}$ matrice di Householder associata ad $a_1$ prima colonna di $A$.
$$
H_1\begin{pmatrix}a_1 & a_2 & \dots & a_n \end{pmatrix}=\begin{pmatrix}
? & \dots
\\
0 & \dots
\\ \vdots
\\
0 & \dots
\end{pmatrix}
$$

poi prendiamo $H_2$ per sistemare gli elementi della sottomatrice di coda successiva:
$$
H_2=
\left(\begin{array} {c|ccc}
1 & 0&\dots &0
\\
\hline
0
\\
\vdots & &\tilde H_2
\\
0
\end{array}\right)
$$
e così via. Otterremo poi $R$ come: 
$$
R=H_n\dots H_2 H_1 A
$$
e otterremo $Q$ come:
$$
Q=H^H_1H^H_2\dots H^H_n=H_1H_2\dots H_n
$$
poiché le matrici di householder sono hermitiane.

> Costo $O(mn^2)$.