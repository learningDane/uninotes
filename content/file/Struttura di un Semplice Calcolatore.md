#uni 
> Registri e variabili di uscita e bidirezionali del processore sEP8 (8 bit simple Educational Processor)![[processore_sEP8.svg|400]]

# Microsottoprogramma per le letture in memoria
Note:
	APP3 contiene il MSB, APP0 contiene eventualmente l'unico byte interesato, altrimenti il LSB
	NUMLOC contiene il numero di byte interessati
```Verilog
readB: begin DIR <= 0; MR_ <= ; NUMLOC <= 1; STAR <= read0; end
readW:
readM:
ReadL: begin DIR <= 0; MR_ <= ; NUMLOC <= 4; STAR <= read0; end
```