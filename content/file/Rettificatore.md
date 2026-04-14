#uni 
Il rettificatore è un dispositivo elettronico in grado di convertire una corrente di alimentazione alternata in una corrente unidirezionale.

Può essere realizzato in diversi modi ma l'utilizzo di diodi ([[Diodo]]) è una delle opzioni più utilizzate.

Un diodo come sappiamo (a meno di tensioni molto negative) lascia scorrere la corrente solo da anodo a catodo, può essere quindi usato per rettificare la corrente.

> Esempio di rettificatore con un diodo e una resistenza (che simula il carico): 
> ![[rettificatore_diodo_res.svg]]

Usando il modello a caduta costante per il diodo:
Data $V_S=V_M \sin (\omega t)$ in entrata, notiamo che la $V_u$ in uscita è unidirezionali, ma è diversa da zero solo durante i semi periodi positivi della tensione in entrata, inoltre, a causa della caduta di potenziale sul Diodo ($\sim0.7 \text V$) notiamo che sono presenti un **ritardo di conduzione** e un **anticipo di spegnimento**, entrambi del valore di $\Delta t$.

Se inseriamo invece un condensatore risolviamo il problema della tensione in uscita presente solo durante i semiperiodi positivi, in quanto quando il condensatore è carico fornisce lui la differenza di potenziale durante i semiperiodi negativi:

> Esempio di rettificatore con un diodo ed un condensatore (filtro RC):
> ![[rettificatore_filtro_rc.svg]]

Come abbiamo detto durante i semiperiodi negativa è il condensatore a fornire la differenza di potenziale, che però diminuisce al diminuire della carica del dispositivo.
Più capacitivo è il condensatore e meno si scarica tra i semiperiodi positivi, fornendo un potenziale più stabile.

Ora però la ricarica del condensatore avviene solamente durante i semiperiodi positivi, se riuscissimo ad invertire la tensione durante quelli negativi raddoppieremmo la frequenza di ricarica e dimezzeremmo il **ripple**.
Questa rettificazione si chiama *full wave rectification*

Introduciamo il **PIV**: PIV sta per Peak Inverse Voltage ed indica il valore massimo della tensione ai capi del diodo quando questo è interdetto.
Se la PIV supera $V_\text{BR}$ abbiamo breakdown del Diodo ([[Diodo#Breakdown]]).

La PIV per questi due rettificatori è $\text{PIV}= 2 \cdot V_M$.
# Raddrizzatore a Presa Centrale
![[rettificatore_ponte_centrale.png]]
# Raddrizzatore a Ponte di Graetz
![[rettificatore_graetz.png]]
# Confronto

| Caratteristica     | Presa Centrale | Ponte di Graetz   |
| ------------------ | -------------- | ----------------- |
| PIV                | $2 \cdot V_M$  | $V_M$             |
| `#diodi`           | 2              | 4                 |
| Ingombro           | Elevato        | Ridotto           |
| Caduta di Tensione | $V_\gamma$     | $2\cdot V_\gamma$ |
