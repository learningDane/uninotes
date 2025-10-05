#uni 
MATLAB è un ambiente per il [[Calcolo Numerico]] e l'analisi statistica scritto in [[Header file]], che comprende anche l'omonimo linguaggio di programmazione creato dalla [[MathWorks]].

Se si incontra una funzione di cui non si conosce/ricorda l'utilizzo è possibile invocare la guida: `help nomefunzione`.
# Funzioni
```Octave
function[y1] = nomefunzione(x1,x2)
```
- input x1 e x2, output y1
Questa dichiarazione deve essere la prima istruzione eseguibile del file che contiene la funzione.
puoi salvare una funzione in:
- un file nomefunzione.m
- oppure un file che contiene solamente definizioni di funzioni, il nome del file deve corrispondere con il nome della prima funzione contenuta nel file
- oppure in uno script che contiene comandi e definizioni di funzione, in questo caso le funzioni devono essere contenuta alla fine del file e lo script non può avere il nome di nessuna delle funzioni al suo interno

Un file può contenere molteplici funzioni locali o innestate. Al fine della leggibilità è consigliato terminare ogni funzione con `end`.

In particolare la parola chiave `end` è richiesta sempre in questi casi:
- una qualunque funzione in un file contiene una funzione innestata
- la funzione è una funzione locale all'interno di un file che contiene solo funzioni e, a sua volta, ogni funzione locale usa la parola chiave `end`.
- la funzione è locale all'interno di uno script

Per terminare una esecuzione prima dell'`end` della funzione si può usare `return`.
##### Esempio
```Octave
function [area] = areacerchio(raggio)
%AREACERCHIO Funzione che calcola l’area del cerchio di raggio r
%se viene fornito un raggio negativo ritorna il valore flag -1
if raggio < 0
	area = -1;
	return
	end
area = pi*raggio^2;
end
```
# Sintassi
- `help comando` per ottenere info sul comando
### Matrici e Vettori
- `a:t:b` crea una matrice con componenti che partono da $a$ ed arrivano a $b$ ad incrementi di $t$. Se $t=1$ si può anche solo usare `a:b`.
- `v = linspace(a,b,n)` restituisce un vettore composto dagli `n` numeri tra `a` e `b` equidistanziati
- `A(x,y,z)=k` per assegnare il singolo elemento della matrice di coordinate `x,y,k`, se cerco di scrivere un elemento che non esiste, la matrice viene ingrandita
- `lenght(A)` : length of vector
- `size(A)` : size of matrix
- `A'` : trasposta
- `A=diag(v,k)` crea una matrice con elementi del vettore v sulla k-esima diagonale e 0 altrove.
- `A( x1:y1 ; x2:y2 )` seleziona la sottomatrice di $A$ con estremi i punti delle coordinate specificate.
- `:` da solo è un'abbreviazione per `1:end` 
- `[L,U,P]=LU(A)` rende fattorizzazione LU di A con pivoting
### Grafici
- plot(x,y)` con x, y vettori della stessa lunghezza
- loglog(x,y) rappresenta la stessa cosa ma su scala logaritmica su entrambi gli assi
### Misurazione del Tempo
- tic; istruzione toc; misura il tempo di istruzione
- misurazione più precisa: `timeit`, fa la media di molte esecuzioni
# Control System Toolbox
### Bode
```Matlab
bode(tf(num,den));
bode(spk([],[],[]))
```
### Nyquist

# Optimization ToolBox
### Linprog
Per risolvere un [[Problema di Programmazione Lineare (PL)]], [[MatLab]] offre ___linprog___.
Risolve i problemi nel seguente forma: 
$$
\begin{cases} min \ c^T x \\ Ax \leq b \\ A_{eq} = b_{eq} \\ LB \leq x \leq UB \end{cases}
$$

dove $LB$ e $UB$ sono i vettori dei lower e upper bound.
Questa forma è una forma standard, quindi ogni problema PL può essere portato in questa forma
### Esempio

$$
\begin{cases} max \ x_1+x_2 \\ 3x_1+5x_2\geq 7 \\ 2x_1+6x_2-9x_3 = 9 \\ x_1, x_2, x_3 \geq 0 \\ x_2 \leq 8\end{cases}
$$

Digitare: (ordine e nomi alle matrici non contano, conta solo ordine nel comando linprog(...))
```matlab
>> c=[-1 0 -1]
>> UB=[ ; 8 ; ]
>> LB=[0;0;0]
>> beq=[9]
>> b=[-7 ; 3]
>> A=[-3 -5 0 ; 1 0 1]
>> Aeq=[2 6 -8]
>> [x,v]=linprog(c,a,b,aeq,beq,lb,ub)
>> appare soluzione: x=(val ottimo)
```
### Intlinprog

$$
\begin{cases} min \ c^T x \\ Ax \leq b \\ A_{eq} = b_{eq} \\ LB \leq x \leq UB \\ x \end{cases}
$$

`[x,v]=intlinprog(c,int,a,b,aeq,beq,lb,ub)`
dove `intcom` è la lista degli indici di variabili che devono essere intere.
se per esempio ho 4 variabili e le voglio tutte intere: `int=[1 2 3 4]` oppure `int=[1;2;3;4]` 
### Quadprog

$$
\begin{cases} 
\min \frac{1}{2}x^THx+f^Tx \\
A\cdot x≤b \\
Aeq\cdot x=beq \\
lb ≤ x ≤ub
\end{cases}
$$

```Matlab
[x,fval,exitflag,output,lambda]=quadprog(h,f,a,b,aeq,beq,lb,ub,x0,options)
``` 
esempio: $f(x)=\frac{1}{2}x^2+y^2 -xy-2x-6y$ 
`h = [1 -1 ;-1 2]` 
`f = [-2 ; -6]` 
`a = [1 1; -1 2; 2 1];`
`b = [2; 2; 3];` 
######### exitflag
![[Pasted image 20250107122104.png]]
### Assignment
Restituisce l'assegnamento di costo minimo del TSP, per fare poi l'algoritmo delle toppe. 
```Matlab
assignment([matricespecchiatadeicostiTSP])
```
### fgh_display(f,g,h,x,range,c)
Disegna il dominio e il valore della funzione su questo dominio.
```Matlab
f=x1*2+3*x1*x2 ...
g1= x2+3 ..
..
g4= ..
fgh_display(f, [g1;g2;g3;g4], [], [],[],[])
```
### minsearch
```Matlab
[x,fval]= fminsearch('6*x(1)^2+3*x(2)-9*x(1)*x(2) ecc',x0)
```
![[Pasted image 20250125184419.png]]
### Gradiente proiettato
esegue un passo del gradiente proiettato, inserire bene le matrici vettore, b e x, non possono essere inserite matrici righe.
MINIMIZZA
```Matlab
RicOp.gradienteProiettato(f,a,b,xk,100)
```
### Gomory
esegue un taglio di gomory a partire da una certa X di base.
Vanno inseriti i dettagli della forma duale std, quindi con gli scarti!!!
MI RACCOMANDO I PUNTI E VIRGOLI PER I VETTORI COLONNA.
```Matlab
gomory(c,x,a,b)
x
%es:
%per trovare gli scarti (vanno messi nella x), vettore s=b-a*x dove b e a NON %hanno i vincoli di positività (sono già nel duale)
c=[43 45 0 0]
x=[32 ; 12 ; s1 ; s2]
a=[123 132 1 0 ; 3 98 0 1]
b=[12 ; 1]
```
### Simplex
esegue un passo del simplesso, MASSIMIZZA ATTENZIONE!!!!!
```Matlab
RicOp.pSimplex(f,A,b,base,iter)

⎰ max f'*x
⎱ A*x<=b
            % EXAMPLE
            % f = [-7 1]
            % A = [
            % 	-3 2;
            % 	-1 -3;
            % 	0 1;
            % 	3 2;
            % 	1 0;
            % 	2 -1; ]
            % b = [4; -6; 5; 22; 6; 16]
            % base = [4 5]
```
# Esempi
## Plot di Grafico, funzione definita a tratti, ascissa in scala logaritmica, ordinata in radianti
```Octave
function funzione3;

w = logspace(-3, 3, 1000); % w on log scale from 10^
T = 1;                   % TAU constant
y = -atan(T*w);       % arctan

hold on %appende tutti i grafici nella stessa finestra

% ------------------- Grafico Asintotico
w1 = w(w < 1e-1);
y1 = zeros(size(w1));
w2 = w((w >= 1e-1) & (w <= 1e1));
y2 = -pi/4 * log10(w2) - pi/4;
w3 = w(w > 1e1);
y3 = -pi/2 * ones(size(w3));
plot(w1, y1, 'r', 'linewidth', 2);
plot(w2, y2, 'r', 'linewidth', 2);
plot(w3, y3, 'r', 'linewidth', 2);
% -------------------

% ------------------- arcotangente con diversi valori di tau
plot(w, -atan(0.1*w), 'g--', 'linewidth', 1);
plot(w, -atan(10*w), 'y--', 'linewidth', 1);
plot(w, y, 'b', 'linewidth', 2); % grafico arcotangente
% -------------------

ylim([-2,0.5]) % limiti ordinata

plot([min(w), max(w)], [-pi/4,-pi/4], '--k'); %linea tratteggiata su fase=pi/4
plot([1,1],ylim,'--k'); %linea tratteggiata su w=1


% ------------------- etichette in radianti
yticks = [-pi/2, -pi/4, 0];
yticklabel = {'-\pi/2', '-\pi/4', '0'};
% -------------------


set(gca,'ytick', yticks, 'yticklabel', yticklabel ,'XScale', 'log');

xlabel('\omega rad/s');
ylabel('\phi G  rad')
title('Fase della Risposta in Frequenza di un Polo Semplice')
legend('','Grafico Asintotico','', '\tau=0.1','\tau=10' ,'\phi G = atan(\omega*(\tau=1))')


% ------------ salvataggio come svg
print -dsvg "exponential_plot.svg"

endfunction
```
![[rispostaarmonicafasepolosemplice.svg]]