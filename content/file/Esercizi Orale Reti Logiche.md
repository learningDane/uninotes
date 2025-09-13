[[Reti Logiche]]
# 1
>Aggiungo un registro IC (Instruction Counter): modifica il codice Verilog del processore ovunque serva per supportare il nuovo registro, che deve tenere conto di tutte le istruzioni fatte. Si aggiungano due nuove istruzioni (RSIC e RDIC): la prima resetta il registro IC e la seconda copia il contenuto del registro dentro %AL

a me torna che:
- aggiungo registro: reg[7:0] IC;
- mi occupo del reset iniziale: 
        always @(reset_ == 0) #1 begin
        ...
        IC <= 0;
        end

cambio lo stato fetch0:
fetch0: begin A23_A0 <= IP; IP <= IP +1; MJR <= fetch1; IC <= IC +1; STAR <= readB; end

passiamo alle istruzioni rsic e rdic
io le metterei entrambe in F0, quindi senza fase di fetch a parte l'opcode

aggiungo i nuovi opcode in valid_fetch() e first_execution_state()

aggiungo nel blocco always i seguenti stati:
rsic: begin IC <= 0; STAR <= fetch0; end
rdic: begin AL <= IC; STAR <= fetch0; end