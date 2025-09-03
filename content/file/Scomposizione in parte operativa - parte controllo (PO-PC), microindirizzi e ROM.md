#uni 
![[Pasted image 20250202194305.png]]
>La parte operativa è quella responsabile dell'interfacciamento col mondo esterno e della produzione degli stati interni dei registri operativa.
>È una RSS di Mealy ([[Rete Sequenziale Sincronizzata (RSS)]], [[Modello di Mealy]]).

>La parte di controllo è quella contentente la logica per l'aggiornamento dello stato interno.
>È una RSS di Moore ([[Modello di Moore]]).

Queste reti presentano la variabile di condizionamento e quella di comando
# Procedimento
1. Guardiamo ad ogni registro operativo come [[Registro Multifunzionale]] e isoliamo le loro relative µ-operazioni diverse. Per ogni registro operativo andiamo a sintetizzare la relativa rete combinatoria operativa. Ogni rete combinatoria operativa prende in ingresso le variabili di comando della parte di controllo e lo stato di uscita dei registri operativi.
2. Adesso guardiamo i µ-salti e sintetizziamo per ogni condizione indipendente (le condizioni che determinano i µ-salti) una rete combinatoria di condizionamento, che deve generare una ==variabile di condizionamento==, che deve valere $1$ se la condizione è vera e deve valere $0$ se la condizione è falsa.
3. Adesso che abbiamo le variabili di condizionamento dobbiamo sintetizzare la parte controllo.
# Riassunto
- Immaginiamo ogni registro operativo come un registro multifunzionale (cioè un registro preceduto da multiplexer).
* Nel codice Verilog cerchiamo tutte le funzioni che possono determinare il valore del registro operativo nell’assegnamento procedurale.
* ==Quale funzione sarà considerata dipenderà dalle variabili di condizionamento==, generate dalla Parte Controllo. La cosa non è strana: è lo stato interno della rete a dirci cosa fare con un certo registro operativo.
```Verilog
casex(STAR)
	S0 : begin 
	//legge per registro operativo1
	//reg op 2 ecc
	end
	S1 : //ecc
	...
	endcase
```
# Immagine Riepilogativa
![[immagine riepilogativa sintesi pc-po.png]]
# Modulo ABC
- Ricordati di collegare PO e PC tramite wire con variabili di condizionamento e di comando
```Verilog
module ABC (
    input clock, reset_,
    inout[7:0] data,

    output ior_, iow_,
    output[11:0] out,

    output[15:0] addr
);
    // wire...
    wire b2,b1,b0,c1,c0;
    wire[2:0] mjr;

    PO po(
        .clock(clock), .reset_(reset_), .data(data), .iow_(iow_),
        .ior_(ior_), .out(out), .addr(addr), .b2(b2), .b1(b1),
        .b0(b0), .c1(c1), .c0(c0), .mjr(mjr)
    );

    PC pc(
        .clock(clock), .reset_(reset_), .b2(b2), .b1(b1),
        .b0(b0), .c1(c1), .c0(c0), .mjr(mjr)
    );
endmodule
```
# Modello basato sui Microindirizzi
```Verilog
module PC(
input clock, reset_,
output b2,b1,b0,
input c0,c1,
input[2:0] mjr
);

reg[2:0] STAR;
localparam S0 = 3'b000,
S1 = 3'b001,
S2 = 3'b010,
S3 = 3'b011,
S0R = 3'b100,
S1RA = 3'b101,
S1RB = 3'b110;
// variabili di comando
assign { b2,b1,b0 } = STAR;

always @(reset_ == 0) #1 begin
STAR <= S0;
end

always @(posedge clock) if(reset_ == 1) #3 begin
casex(STAR)
S0: STAR <= (c0==1) ? S1 : S0R;
S1: STAR <= S0R;
S2: STAR <= S0R;
S3: STAR <= S0;
S0R: STAR <= (c1==1) ? S1RA : S1RB;
S1RA: STAR <= mjr;
S1RB: STAR <= mjr;
endcase
end
endmodule

/*
µ-indirizzo b2_b1_b0 µ-indT µ-indF c_eff µ-type
	S0         000    S1     S0R     c0   0
	S1         001    S0R    S0R     -    0
	S2         010    S0R    S0R     -    0
	S3         011    S0     S0      -    0
	S0R        100   S1RA   S1RB     c1   0
	S1RA       101     -      -      -    1
	S1RB       110     -      -      -    1
*/
```
