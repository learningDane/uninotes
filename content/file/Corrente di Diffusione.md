#uni 
Il fenomeno della diffusione è la tendenza a raggiungere l'equilibrio di concentrazione dei portatori di carica.

Questo processo è descritto dalla Legge di Fick, che vale per vari tipi di particelle, non sono portatori di carica.

>[!theorem] Legge di Fick
>Il processo di diffusione passiva delle particelle (soluti o gas) da una zona a concentrazione maggiore verso una a concentrazione minore, proporzionalmente al gradiente di concentrazione crea un flusso.
>Il flusso (J) è influenzato dall'area di scambio (A), dal coefficiente di diffusione (D) e dallo spessore della membrana (d).

Nell'ambito dei conduttori la Legge di Fick descrive una tendenza dei portatori di carica a muoversi da zone ad alta concentrazione a zone di bassa concentrazione delle stesse causa una corrente, detta **Corrente di Diffusione**.

Dato il seguente conduttore:
![[diffusione.svg]]
Calcoliamo la corrente di diffusione:
$$
\vec J_\text{diff} = q\cdot D_n(-\frac{\partial n}{\partial x})\hat i_x
$$
- $q$ è la carica dei portatori di carica che stiamo trattando
- $D_n$ e $\partial n$, $n$ indica che trattiamo un gradiente di elettroni, quindi $q=-|q_\text{elettrone}|$ 

$D_n$ è la **costante di diffusione**, sempre positiva, è legata alla mobilità attraverso la seguente relazione, proposta da [[Einstein]]:
$$
\frac{D_n}{\mu_n}=\frac{D_p}{\mu_p}=\frac{K_B \cdot T}{q}=V_T
$$
Qua $V_T$ è detta **thermal voltage**, a 300 Kelvin vale circa $26 mV$.

Valori di costante di diffusione:
- $D_n=34 \text{ cm}^2/s$ 
- $D_p=12 \text{ cm}^2/s$ 

Quindi in un conduttore la corrente totale è somma della corrente di drift e della corrente di diffusione:
$$
\begin{matrix}
\vec J_n=\vec J_\text{n,drift} + \vec J_\text{n, diffusione}=nq\mu_n\cdot \vec E+\vec J_\text{n,diffusione}
\\
\vec J_p=\vec J_\text{p,drift} + \vec J_\text{p, diffusione}=pq\mu_p \cdot \vec E=pq\mu_p\cdot \vec E+\vec J_\text{p,diffusione}
\\
\vec J_\text{tot}=\vec J_n + \vec J_p
\end{matrix}
$$
