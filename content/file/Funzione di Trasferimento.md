#uni 
Siamo arrivati ad utilizzare strumenti algebrici anche relativamente complessi ([[Teoria dei Sistemi]]), studiamo ora un metodo di studio di sistemi che semplifichi i conti.
È sempre possibile passare da una forma in variabili di stato ad una ___funzione di trasferimento___.

___Definizione___: la ___funzione di trasferimento___ di un sistema dinamico nella variabile $s$ è il rapporto fra l'uscita e il suo ingresso: $F(s)=\frac{Y(s)}{U(s)}$. 

![[funzioneditrasferimento1.svg]]

# Risposta all'impulso
I sistemi LTI possono essere caratterizzati attraverso la loro risposta all'impulso (ovvero supponiamo $u(t)=\delta(t)$:
$$
y(t)=g(t)*r(t)=\int_0^tg(t-\tau)\cdot r(\tau)d\tau=\int_0^tg(\tau) \cdot r(t-\tau)d\tau \quad ; \quad \geq 0
$$
con $r(t)$ il segnale di riferimento (input), $y(t)$ l'uscita e $g(t)$ la ___risposta all'impulso___.
In [Laplace](Trasformata%20di%20Laplace.md) per via della [proprietà di convoluzione](Trasformata%20di%20Laplace.md#Proprietà%20di%20Convoluzione) invece abbiamo semplicemente:
$$
Y(s)=G(s) \cdot U(s)
$$

>L'antitrasformata di una funzione di trasferimento rappresenta la risposta all'impulso unitario.

>L'integrale della risposta all'impulso unitario rappresenta la risposta al gradino unitario.

