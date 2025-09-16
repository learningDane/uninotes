[[Reti Logiche]]
# Esercizi Svolti
### 1
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
# Raccolta di Esercizi
### 2023/02/08
- Latch S-R: tabella di flusso, tabella di applicazione, sintesi e aggiunta delle variabili a reset
- Sintetizzare il circuito per il calcolo del segno di un numero in base 10, codifica BCD in traslazione
- Aggiungo un registro IC (Instruction Counter): modifica il codice Verilog del processore ovunque serva per supportare il nuovo registro, che deve tenere conto di tutte le istruzioni fatte. Si aggiungano due nuove istruzioni (RSIC e RDIC): la prima resetta il registro IC e la seconda copia il contenuto del registro dentro %AL
- Interfaccia di conversione A/D: interfaccia funzionale, vision e interna e software di input
- Data una base $\beta$ uguale a $\gamma \cdot \alpha$, e dato un numero A uguale a ( $A_{n-1}$, $A_{n-2}$, ..., $A_{0}$) in base $\beta$, dimostrare che **A mod $\alpha$** è uguale a **$A_{0}$ mod $\alpha$**.
### Primo Appello Sessione Invernale 2024 - (17/01/24)
 - Latch SR: sintesi, reset iniziale, transizioni multiple
 - Fase di esecuzione della Call
 - Interfaccia seriale, descrizione trasmettitore 
 - Sintesi a porte NAND di una mappa di karnaugh 
 - Divisione tra interi e disegno del circuito di fattibilità
### 2025/02/03
1. Si supponga di voler fornire al programmatore un registro `AX = {AH, AL}` e voler mettere a disposizione le istruzioni `INC %AX`, `SHL %AX`, `SHR %AX`, `SAR %AX`. Si discuta la fase di fetch, introducendo un nuovo formato se necessario o riconducendo a un formato esistente (motivare la risposta). Descriverne inoltre la fase di esecuzione.
2. Descrivere una rete combinatoria che raddoppia una cifra naturale in base 7, compresa di `C_in` riporto entrante e `C_out` riporto uscente. Fare la sintesi a porte NOR dell'uscita `C_out`
3. Sintetizzare la parte operativa relativa al registro `MJR` e la parte di controllo a partire da questa descrizione e disegnare gli schemi di entrambe.
   Scrivere la ROM della parte di controllo.
```verilog
reg A, X;
...
casex (STAR)
    S0: begin ... STAR <= (A == 0) ? S2 : S1; end
    S1: begin ... STAR <= S3; end
    S2: begin ... STAR <= (X == A) ? S4 : S2; end
    S3: begin ... STAR <= (X == 1) ? S6 : S5; end
    S4: begin ... STAR <= S5; end
    S5: begin ... MJR <= (X == 1) ? S1 : (A == 0) ? S3 : S4; end
    S6: begin ... STAR <= MJR; end
endcase
```

4. Dato A naturale di n cifre in base β, dimostrare che |A|m = 0 se e solo se |A0|m = 0, con m = α·β (α >= 1, β >= 1)
   ==___questa domanda non mi torna.___==
5. Montare due chip di ram 128k x 8 bit in modo che rispondano agli indirizzi più alti di un calcolatore con spazio di indirizzamento di 2^20 locazioni
### 2025/07/02
- fase di reset del calcolatore
- calcolo dell'opposto in base B + disegno del circuito in base 2
  ingresso $X$, uscita $Y=| \overline X + 1|_{{\beta^n}}$ e $ow=(X==\frac{\beta^n}{2}) ? 1 : 0$. 
- sintesi di un registro multifunzionale che conserva un numero, che lo moltiplica per 2, che fa il quadrato di quel numero
- definire la fase di esecuzione dell' istruzione di SETcond al, SETcond indirizzo, SETcond (DP)
- sintetizzare una rete di moore sintesi a porte NOR