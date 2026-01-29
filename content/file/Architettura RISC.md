#uni 
Attorno al 1980 sono nati nelle università i processori **RISC** (per Reduced Instruction Set Computer), sviluppati per risolvere i problemi dei **CISC**. 
L'architettura RISC è quella prevalente al giorno d'oggi (anche i processori "CISC" odierni in realtà sono RISC, traducono le istruzioni più complicate in più istruzioni RISC).

Un set di istruzioni RISC prevede tipicamente:
- istruzioni tutte della stessa grandezza (per esempio 4 byte)
- pochi e semplici formati
- istruzioni operative che lavorano esclusivamente sui registri o al massimo su operandi immediati
- istruzioni separate di load/store per accedere alla memoria senza fare altre elaborazioni

Le ultime due caratteristiche definiscono una cosiddetta **Architettura Load/Store**.

La tipica istruzione RISC ha il seguente formato: `op src1, src2, dst`.