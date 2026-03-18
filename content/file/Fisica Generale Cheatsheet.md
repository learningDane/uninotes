#uni 
# Elettromagnetismo
- *Legge di Coulomb*:
$$
\large
\begin{matrix}
F_{q_{1,2}}=k_e\frac{q_1 \cdot q_2}{r^2}\hat r_{1,2}
\\
k_e=\frac{1}{4 \pi \mathscr E_0}=8.9876\times 10^9 \text N \text m^2/\text C^2
\\
\mathscr E_0=8.854 \times 10^{-12}\text C^2  / \text N \cdot \text m ^2
\\
e=1.6\times 10^{-19} \text C
\end{matrix}
$$
- Campo Elettrico: 
$$
\large
\begin{matrix}
\vec E = \frac{\vec F}{q}, \quad [E]=\text N / \text C
\\
\vec E= k_e\cdot \frac{q}{r^2}\hat r
\end{matrix}
$$ 
- Flusso del campo Elettrico: $\Phi_e = \int \vec E \cdot d\vec A$ 
- *Teorema di Gauss*:
$$
\large
\begin{matrix}
\text{Per una superficie Gaussiana}: 
\Phi_E=\oint\vec E \cdot d \vec A=\frac{\sum_\text{interne} q_\text{interne}}{\mathscr E_0}
\\
\Phi_E \text{ delle cariche esterne}: \Phi_E=0
\end{matrix}
$$
- Potenziale: $V=\frac{U}{q}$v
$$
\Delta V_{a,b}=-\int_a^b \vec E \cdot d \vec s
$$
- Corrente Elettrica: $I_\text{media}=\frac{\Delta Q}{\Delta t}, \quad I=\frac{dQ}{dt}, \quad [I]=\text A=\text C/\text s$ 
- Densità di corrente: $J=\frac{I}{A}=nqv_d=\sigma \frac{\Delta V}{l}, \quad [J]=\text A/\text m^2$  
- *Legge di Ohm*:
$$
\sigma = \frac{J}{E}
$$
- Resistenza: $R=\frac{\Delta V}{I}, \quad R=\rho \frac{l}{A}, \quad [R]=\ohm=\text V / \text A$ 
- Resistività: $\rho = \frac{1}{\sigma}, \quad [\rho]=\ohm \cdot m$ 
- Potenza: $P=\Delta V \cdot I= R \cdot I^2, \quad [P]=\text W=\text j/\text s$ 
- Leggi di Kirchoff:
$$
\begin{matrix}
\text{I.} &:& \sum_\text{nodo}I=0
\\
\text{II.} &:& \sum_\text{maglia}\Delta V = 0
\end{matrix}
$$
- Circuiti RC:
$$
\begin{matrix}
q(t)=C\cal E(1-e^{-t/\tau})=Q_\text{max} (1-e^{-t/\tau})
\\
i(t)=\frac{\cal E}{R}e^{-t/\tau}
\\
W_\text{fem per caricare C}=Q_\text{max} \cal E=C\cdot \cal E ^2
\\
\Delta V_\text{C. carico}=\frac{Q}{C} \quad\text{e} \quad I_\text{C. carico}=0
\\
I_\text{max}=I_i=\frac{\cal E}{R}
\\ 
Q_\text{max} = C \cdot \cal E
\end{matrix}
$$
- Campo Magnetico:
$$
\begin{matrix}
\vec F_B=q \cdot \vec v \times \vec B \implies |F_B|=|q| \cdot |v| \cdot |B| \cdot \sin \theta
\\
!!! \ \vec F_B \ \text{non compie lavoro!}
\\
[B]=\text T=\frac{\text N}{\text C \cdot \text m / \text s}=\frac{\text N}{\text A \cdot \text m} \quad \text {Tesla}
\\
[B]=\text T=10^4 \text G\quad \text{Gauss}
\end{matrix}
$$
- *Forza di Lorentz*: $\vec F_L=q\cdot \vec E + q \cdot \vec v \times \vec B$ 
- *Legge Biot-Savart*: campo elettrico generato da cariche in movimento:
$$
\large
\begin{matrix}
\text{Legge Biot-Savart}:\quad d\vec B=\frac{\mu_0}{4\pi}\frac{I d s^2 \times \hat r}{r^2}
\\
\mu_0=4\pi \times10^{-7} \text T\cdot \text m / \text A : \text {permeabilità magnetica nel vuoto}
\end{matrix}
$$
- *Legge di Ampere*: 
$$
\large
\begin{matrix}
\text{Legge di Ampere}:\quad \oint \vec B \cdot d\vec s=\mu_0 \cdot I
\\
I: \text{C.C. tot. che attraversa una sup. qualsiasi con }\oint d\vec s \text{ come frontiera}
\\
\oint d \vec s: \text{Percorso Amperiano}
\end{matrix}
$$
- *Legge di Gauss*: 
$$
\large
\begin{matrix}
\text{Legge di Gauss}:\quad \Phi_B=\int \vec B \cdot d\vec A
\\
\Phi_B: \text{Flusso del campo magnetico}
\\
[\Phi_B]=\text{Wb}=\text T \cdot \text m^2 \quad \text{Weber}
\\
\text{Se } \oint d\vec A \text{ è una superficie chiusa} : \Phi_B=0
\end{matrix}
$$
- *Legge dell'Induzione di Faraday*: 
$$
\large
\begin{matrix}
\text{Legge dell'induzione di Faraday}:\quad \cal E_\text{indotta} = -\frac{d\Phi_B}{dt}
\\
\Phi_B : \text{Flusso Magnetico concatenato col circuito}
\\
\text{caso bobina di }N\text{ spire} : \cal E=-\it N\frac{d \Phi _B}{dt}
\\
\oint \vec E \cdot d\vec s=-\frac{d\Phi_B}{dt}
\end{matrix}
$$
- *Legge di Lenz*: "La polarità della FEM indotta è tale che la corrente generata crei un campo magnetico che si oppone alla variazione del flusso del campo magnetico che l'ha generata."
- Generatore di Tensione: $\cal E = \it N B  A  \omega  \sin(\omega \cdot t)$ 