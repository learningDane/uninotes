#uni 
> Registri e variabili di uscita e bidirezionali del processore sEP8 (8 bit simple Educational Processor)![[processore_sEP8.svg|400]]

# Microsottoprogramma per le letture in Memoria
Note:
- APP3 contiene il MSB, APP0 contiene eventualmente l'unico byte interessato, altrimenti il LSB.
- NUMLOC indica il numero di byte interessati.
- A23_A0 è già stato stabilito nel sottoprogramma principale.
```Verilog
readB: begin DIR <= 0; MR_ <= 0; NUMLOC <= 1; STAR <= read0; end
readW: ...
readM: ...
readL: begin DIR <= 0; MR_ <= 0; NUMLOC <= 4; STAR <= read0; end

read0: begin APP0 <= D7_D0; A23_A0 <= A23_A0 + 1; NUMLOC <= NUMLOC - 1; STAR <= (NUMLOC == 1) ? read4 : read1; end
read1: ...
read2: ...
read3: begin APP3 <= D7_D0; A23_A0 <= A23_A0 + 1; STAR <= read4; end

read4: begin MR_ <= 1; STAR <= MJR; end
```
# Microsottoprogramma per le scritture in Memoria
```Verilog
writeB: begin DIR <= 1; D7_D0 <= APP0; NUMLOC <= 1; STAR <= write0; end
writeW: ...
writeM: ...
writeL: begin DIR <= 1; D7_D0 <= APP0; NUMLOC <= 4; STAR <= write0; end

write0: begin MW_ <= 0; STAR <= write1; end
write1: begin MW <= 1; STAR <= (NUMLOC == 1) ? write11 : write2; end

write2: begin A23_A0 <= A23_A0 + 1; D7_D0 <= APP1; NUMLOC <= NUMLOC - 1; STAR <= write3;
write3: begin MW_ <= 0; STAR <= write4;
write4: begin MW_ <= 1; STAR <= (NUMLOC == 1) ? write11 : write5;

write5: begin A23_A0 <= A23_A0 + 1; D7_D0 <= APP2; NUMLOC <= NUMLOC - 1; STAR <= write6;
write6: begin MW_ <= 0; STAR <= write7;
write7: begin MW_ <= 1; STAR <= (NUMLOC == 1) ? write11 : write8;

write8: begin A23_A0 <= A23_A0 + 1; D7_D0 <= APP3; STAR <= write9;
write9: begin MW_ <= 0; STAR <= write10;
write10: begin MW_ <= 1; STAR <= write11;

write11: begin DIR <= 0; STAR <= MJR; end
```
# Descrizione (dei punti salienti) del Processore
```Verilog
module Processore(d7_d0, a23_a0, mr_, mw_, ior_, iow_, clock, reset_);
	...
	inout[7:0] d7_d0;
	assign d7_d0 = (DIR == 0) ? 'Hzz : D7_D0
	reg ...;
	reg[6:0] STAR, MJR;
	parameter fetch0=0, ... , write11=86;
	parameter[2:0] F0='b000, ... , F7='b111;
	
	function valid_fetch; ... endfunction;
	function first_execution_state; ... endfunction;
	function jmp_condition; ... endfunction;
	function alu_result; ... endfunction;
	function alu_flag; ... endfunction;
	
	always @(reset_ == 0) #1 begin
		IP <= 'HFF0000;
		STAR <= fetch0;
		DIR <= 0;
		F <= 'H00;
		MR_ <= 1; ... ; IOW_ <= 1;
		end
	always @(posedge clock) if (reset_ == 1) #3 begin
		casex(STAR)
			// ---------------------------------
			//         FASE DI FETCH
			fetch0: begin A23_A0 <= IP; IP <= IP + 1; MJR <= fetch1; STAR <= readB; end
			fetch1: begin OPCODE <= APP0; STAR <= fetch2; end
			fetch2: begin MJR <= (OPCODE[7:5] == F0) ? fetchEND : 
				(OPCODE[7:5] == F1) ? fetchEND :
				(OPCODE[7:5] == F2) ? fetchF2_0 :
				(OPCODE[7:5] == F3) ? fetchF3
				
				STAR <= (valid_fetch(OPCODE) == 1) ? fetch3 : nvi;
				end
			fetch3: begin STAR <= MJR;
			
			fetchF2_0: begin A23_A0 <= DP; MJR <= fetchF2_1; STAR <= readB; end
			fetchF2_1: begin SOURCE <= APP0; STAR <= fetchEnd; end
			fetchF3_0: begin DEST_ADDR <= DP; STAR <= fetchEnd; end
			fetchF4_0: begin A23_A0 <= IP; IP <= IP + 1; MJR <= fetchF4_1; STAR <= readB; end
			fetchF4_1: begin SOURCE <= APP0; STAR <= fetchEND; end
			fetchF5_0: begin A23_A0 <= IP; IP <= IP + 3; MJR <= fetchF5_1; STAR <= readM; end
			fetchF5_1: begin A23_A0 <= {APP2 , APP1 , APP0}; STAR <= fetchEnd; end
			fetchF6_0: begin A23 <= IP; IP <= IP + 3; MJR <= fetchF6_1; STAR <= readM; end
			fetchF6_1: begin DEST_ADDR <= {APP2 , APP1 , APP0}; STAR <= fetchEnd;
			fetchF7_0: begin A23 <= IP; IP <= IP + 3; MJR <= fetchF7_1; STAR <= readM; end
			fetchF7_1: begin DEST_ADDR <= {APP2 , APP1 , APP0}; STAR <= fetchEnd;
			// fetch di F6 e F7 sono uguali
			
			nvi: begin STAR <= nvi; end //istruzione non valida
			fetchEND: begin MJR <= first_execution_state(OPCODE); STAR <= fetchEnd1; end
			fetchEND1: begin STAR <= MJR; end
			// fine fase di Fetch
			//----------------------------------------
			//            FASE DI ESECUZIONE
			nop: begin STAR <= fetch0; end
			hlt: begin STAR <= hlt; end
			ALtoAH: begin // MOV AL, AH
				AH <= AL; STAR <= fetch0; end
			...
			aluAL: begin AL <= alu_result(OPCODE, SOURCE, AL); F <= { F[7:4] , alu_flag(OPCODE, SOURCE, AL) }; STAR <= fetch0; end
			// aluAH: same as AL
			...
			jmp: IP <= (jmp_condition(OPCODE, F) == 1 ) ? DEST_ADDR : IP; STAR <= fetch0; end
			...
			call: begin A23_A0 <= SP - 3; SP <= SP - 3; APP2 <= IP[23:16]; APP1 <= IP[15:8]; APP0 <= IP[7:0]; MJR <= call1; STAR <= writeM; end
			call1: begin IP <= DEST_ADDR; STAR <= fetch0; end
			ret: begin A23_A0 <= SP; SP <= SP + 3; MJR <= ret1; STAR <= readM; end
			ret1: begin IP <= {APP2 , APP1 , APP0}; STAR <= fetch0; end
			... // in offset, al       F2 3byte
			in: begin A23_A0 <= IP; IP <= IP + 2; MJR <= in1; STAR <= readW; end
			in1: begin A23_A0 <= {8'H00 , APP2 , APP1}; STAR <= in2; end
			in2: begin IOR_ <= 0; STAR <= in3; end
			in3: begin AL <= d7_d0; IOR_ <= 1; STAR <= fetch0; end
			... // out al, offset
			out: begin A23_A0 <= IP; IP <= IP + 2; MJR <= out1; STAR <= readW; end
			out1: begin A23_A0 <= {8'H00 , APP1 , APP0}; DIR <= 1; D7_D0 <= AL; STAR <= out2; end
			out2: begin IOW_ <= 0; STAR <= out3; end
			out3: begin IOW_ <= 1; STAR <= out4; end
			out4: begin DIR <= 0; STAR <= fetch0;
		endcase
		end
endmodule
```