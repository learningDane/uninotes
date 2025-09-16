#uni 
Queste comunicano con dispositivi esterni in accordo ad un vecchio standard del 1969, il **EIA-RS232**.
Si utilizza una unica linea di collegamento (normalmente chiamata __RXD__ o __TXD__), sulla quale vengono trasmessi l'uno dopo l'altro i bit, questi bit vengono inviati a gruppi, detti __Trame__. 
Non ci sono specifiche sul tempo che può trascorrere tra una trama e l'altra, i bit invece all'interno di una trama devono essere inviati con una cadenza regolare, intervallati di un tempo __T__, detto __tempo di bit__.
Il numero di bit inviati nell'unità di tempo, all'interno di una trama, è detto __bit-rate__, e vale $\frac{1}{t}$.
Le trame sono costituite da un numero di bit che va da 7 a 12.
Una parte di questi bit (detti __bit utili__) costituisce l'informazione vera.
In generale una trama contiente:
- un bit di start
- 8 bit utili
- un eventuale bit di parità
- uno o due bit di stop
# Funzionamento
Tra una trama e l'altra, la linea viene mantenuta in uno stato detto __marking__ (ovvero 1), il bit di start, ovvero la scesa della linea in stato __spacing__ (0), segna l'inizio della trasmissione, utilizzando la codifica __NRZ__ ogni bit utile è trasmetto tenendo la linea in marking o spacing a seconda che sia 1 o 0.
Dopo gli 8 bit utili arriva l'eventuale bit di parità e poi gli 1 o 2 bit di stop, dopodiché la linea viene mantenuta in marking fino al prossimo bit di start, a segnalare l'inizio della prossima trama.
> Il Bit meno significativo (__LSB__) segue temporalmente il bit di start.

```
              start   1     0              0   0    stop
marking: ---         ---         ---                --- ----------
             \     /     \     /      ecc         /
spacing:       ---         ---            --- ---
			<- LSB                         -> MSB
```
# Ricevitore Seriale
Per poter seguire con precisione l'evoluzione della linea di trasmissione __RXD__, il ricevitore viene pilotato con un clock _clock_ric_ che ha un periodo molto minore del tempo di clock __T__, per semplicità supponiamo che sia $\frac{T}{16}$.
1. Il ricevitore attende $\frac{T}{2}$: la __centratura del bit__
2. Preleva i bit uno alla volta, inserendoli in un registro _BUFFER_ tramite una operazione di shift destro.
3. Quando gli 8 bit utili sono nel buffer, l'informazione è completa.
# Interfaccia Seriale Start Stop UART
UART = Universal Asynchronous Receiver-Transmitter, modello 8250, presente nei primi Personal Computer IBM.
### Ricevitore
```Verilog
module ricevitore(
	input dav_in,
	// niente rfd_in perché il ricevitore non può permettersi di sostenere una handshake con la sottointerfaccia parallela, quando arriva il bit di start deve salvare nel Buffer.
	output rxd,
	input byte_in,
	input clock_ric
);
	reg[1:0] STAR;
	localparam S0 = 0,
		S1 = 1,
		wbit = 2,
		wstop = 3;
	reg[7:0] BUFFER;
	reg DAV_;
	assign dav_in = DAV_;
	reg[4:0] WAIT;
	reg[2:0] COUNT;
	localparam bitstart = 0, bitstop = 0;
	
	always @(reset_ == 0) #1 begin
		STAR <= S0;
		DAV_ <= 1;
		// BUFFER indifferente
	end
	always @(posedge clock_ric) if (reset_ == 1) #3 
		casex(STAR)
			S0: begin
				COUNT <= 8;
				DAV_ <= 1;
				WAIT <= 23;
				STAR <= ( rxd == bitstart ) ? wbit : S0 ;
			end
			S1: begin
				BUFFER <= { rxd , BUFFER[7:1] };
				WAIT <= 14;
				COUNT <= COUNT - 1;
				STAR <= (COUNT == 0) ? wstop : wbit;
			end
			wbit: begin
				WAIT <= WAIT - 1;
				STAR <= (WAIT == 0) ? S1 : wbit;
			end
			wstop: begin
				DAV_ == 0;
				WAIT <= WAIT - 1;
				STAR <= (WAIT == 0) ? S0 : wstop;
			end
		endcase
endmodule
```
### Trasmettitore
```Verilog
module trasmettitore(
	input dav_out,
	output rfd_out,
	output txd,
	input byte_out,
	input clock_tra
);
	reg[1:0] STAR;
	localparam S0 = 0,
		S1 = 1,
		S2 = 2;
	reg TxD;
	assign txd = TXD;
	reg[9:0] BUFFER;
	reg[3:0] COUNT;
	reg RFD;
	assign rfd_out = RFD;
	localparam mark = 1, space = 0;
	localparam bitstart = 0, bitstop = 0;
	
	always @(reset_ == 0) #1 begin
		STAR <= S0;
		RFD <= 1;
		TxD <= mark;
		end
	always @(posedge clock_tra) if (reset_ == 1) #3 
		casex(STAR)
			S0: begin
				RFD <= 1;
				BUFFER <= {bitstop , byte_out , bitstart};
				COUNT <= 9;
				STAR <= (dav_out == 0) ? S1 : S0;
				end
			S1: begin
				RFD <= 0;
				TxD <= BUFFER[0];
				BUFFER <= {mark , BUFFER[9:1]};
				COUNT <= COUNT - 1;
				STAR <= (COUNT == 0) ? S2 : S1;
				end
			S2: begin
				STAR <= (dav_out == 1) ? S0 : S2;
				end
		endcase
endmodule
```