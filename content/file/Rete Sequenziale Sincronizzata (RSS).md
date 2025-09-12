#uni 
# Modello di Moore
```Verilog
module Rete_di_Moore( z, x, clock, reset_); //o (Xn-1,...,x=X0, Zm-1,...,Z0,etc)
	input clock, reset_;
	input[N-1:0] x;
	output[M-1:0] z;
	reg[W-1:0] STAR;
	parameter S0 = codifica0, S1 = codifica1, Sk-1 = codificak-1;
	assign {zM-1,...,z0} = (STAR == S0) ? ZS0 :
		(STAR == S1) ? ZS1 :
		...
		/*(STAR == Sk-1) */ ZSk-1;
	always @(reset_ == 0) #1 STAR<=statointernoiniziale;
	always @(posedge clock) if (reset_ == 1) #3
		casex(STAR)
			S0 : STAR <= AS0(xN-1,...,x0);
			S1 : ...
			..
			Sk-1 : STAR <= ASk-1(xN-1,...,x0);
		endcase
	endmodule
```
Le reti di Moore sono reti ___NON trasparenti___.
Sono composte da due [[Rete Combinatoria]] e un Registro STAR.
- La rete RCa, funzione di SIP e X, definisce il SIS
- Il registro STAR contiene il SIP
- la rete RCz, funzione di STAR, definisce Z
### Leggi di Temporizzazione
- $T ≥ T_{hold} + T_{amonte} + T_A + T_{setup}$ 
- $T≥ T_{propagation} + T_A + T_{setup}$ $\to$ meno stringente della prima e può essere ignorata
- $T≥ T_{propagation} + T_Z + T_{avalle}$ 
# Modello di Mealy
Se si combinano due reti di Mealy ottieni un anello combinatorio, no good.
L'unica differenza rispetto al [[#Modello di Moore]] è che qua anche RCB ha in ingresso le variabili di ingresso, oltre al registro STAR.
# Modello di Mealy Ritardato
L'unica differenza rispetoo al [[Modello di Mealy]] è che questo presenta un registro OUTR a supporto delle varaibili di uscita, che la rende una rete ==___non trasparente___== (nessun pericolo di _anello combinatorio_).
# RSS complesse
- ___microoperazioni___: i $K\cdot Q$ assegnamenti `Rq<=Rsk,q(x,Rq-1,...,R0)` relativi ai registri operativi.
- ___microsalti___: i $K$ assegnamenti `STAR<=(x,R1-1,...,R0)` relativi al registro di stato.
- ___statement di etichetta $S_i$___ : gli statement completi all'interno al costrutto `casex .. endcase`.
### Precisazioni sulle microooperazioni
1. $C=\{A,B\}$ descrive l'assegnamento del registro $C$ con i contenuti di $A,B$.
2. $\{A,B\}<=C$ equivale a DUE microoperazioni:
	1. $A<=C[l-1:m]$ 
	2. $B<=C[m-1:0]$ 
3. $C[m-1:0]<=B$ è sostanzialmente scorretta, in quanto A OGNI clock TUTTO il registro viene riassegnato, quindi equivarrebbe a: $C<=\{C[l-1:m],B\}$ 
# Handshake /dav, rfd
- /dav : _data valid_: se \dav=1 allora il dato fornito non è attendibile, se \dav=0 il dato è corretto e disponibile
- rfd : _ready for data_: se rfd=1, il consumatore è pronto a ricevere, se rfd=0 allora il consumatore non è pronto a leggere il dato
Funzionamento:
0. S0: $\text{/dav,rfd}=1,1$ : il dato del produttore non è pronto, il consumatore è pronto a ricevere
1. S1: $\text{/dav,rfd}=0,1$ : il dato è pronto
2. S2: $\text{/dav,rfd}=0,0$ : il consumatore ha prelevato il dato e non è pronto a riceverne altri
3. S3: $\text{/dav,rfd}=1,0$ : il produttore è pronto a produrre un nuovo byte
4. S0: $\text{/dav,rfd}=1,1$ : ritorno allo stato iniziale
Partendo da una condizione iniziale in cui rfd=1 e \dav=1:
Il produttore compie la prima mossa: aggiorna il dato e pone \dav=0, ad indicare che il dato è adesso valido.
Il consumatore, legge \dav=0, pone quindi rfd=0, preleva il dato, e lo elabora.
Il produttore riporta allora \dav=1 e attende che il consumatore riport rfd=1, per ritornare alal condizione iniziale.
Tutte queste variabili di handshake necessitano di un registro di supporto, ognuno dello stesso nome della variabile.
# Handshake soc, eoc
- soc: _start of computation_: soc=0 consumatore non ha bisogno di nuovo byte, soc=1 indica al produttore di fornire un nuovo byte.
- eoc: _end of computation_: eoc=0 produttore ha iniziato la preparazione di un nuovo byte, eoc=1 il produttore è pronto a preparare un nuovo byte.
Funzionamento:
SOC ha bisogno di un registro.
0. S0: $soc,eoc = 0,1$ : consumatore non è pronto a nuovo byte e produttore è disponibile ad iniziarne una nuova
1. S1: $soc,eoc=1,1$ : consumatore è pronto
2. S2: $soc,eoc=1,0$ : produttore inizia produzione
3. S3: $soc,eoc=0,0$ : consumatore notifica di aver capito e non chiede più altri dati
4. S0: $soc,eoc=0,1$ : il produttore ha finito e il consumatore preleva il dato
```Verilog
S0R: begin
	SOC = 1;
	STAR <= (eoc == 1'b0) ? S1R : S0R;
end

S1R: begin
	SOC = 0;
	STAR <= (eoc == 1'b1) ? S2R : S1R;
end

S2R: begin
	X0 <= x;
	STAR <= MJR;
end
```