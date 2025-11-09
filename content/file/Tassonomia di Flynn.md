#uni 
Per classificare le architetture dei calcolatori utilizziamo la **Tassonomia di Flynn**.
Questa classifica un sistema di elaborazione secondo due punti di vista:
- in base alla capacità di avere più flussi di istruzioni
- in base alla capacità di avere più flussi di dati

|                           | SI (single instruction stream) | MI (multiple instruction stream) |
| ------------------------- | ------------------------------ | -------------------------------- |
| SD (single data stream)   | SISD                           | MISD                             |
| MD (multiple Data Stream) | SIM                            | MIMD                             |
# SISD
Un'unica istruzione è eseguita ad ogni step temporale.

>La tradizionale macchina sequenziale (o [[Macchina di Von Neumann]]) usata da tutti i calcolatori convenzionali è un esempio di macchina **SISD**.

# SIMD
Più unità di elaborazione eseguono contemporaneamente la stessa istruzione, lavorando però su flussi di dati differenti.
# SIMD
Modello di computazione asincrono.
- **Parallelismo temporale**: Pipeline: una istruzione viene divisa in fasi diverse ed ogni fase viene eseguita in parallelo alle altre su differenti moduli connessi in cascata.
- **Parallelismo spaziale**:  I medesimi passi sono eseguiti contemporaneamente su un array di processori perfettamente uguali, sincronizzati da un solo controllore.

> Esempi:
> - supercomputer vettoriali (per lavorare su grandi matrici)
> - vector processor con caratteristiche pipeline (parallelismo temporale)
> - array processor (parallelismo spaziale)
> - systolic array (parallelismo temporale/spaziale)

# MISD
Più flussi di istruzioni lavorano contemporaneamente su un unico flusso di dati.
# MIMD
Più flussi di istruzioni sono in esecuzione contemporaneamente su più processori, elaborando insiemi di dati dstinti, privati o condivisi.
### DM-MIMD
**Distributed Memory** MIMD.

> Tassonomia estesa: ![[tassonomiaFlynn.svg | 600]]

