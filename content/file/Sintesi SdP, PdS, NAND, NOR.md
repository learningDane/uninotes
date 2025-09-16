#uni 
# Sintesi SP a costo minimo
1. Disegno la Mappa di Karnaugh
2. Individuo La lista degli implicanti principali
3. Individuo Gli implicanti essenziali
4. Individuo gli implicanti assolutamente eliminabili
5. Individuo gli implicanti semplicemente eliminabili
6. Valuto le possibili liste di copertura in base al criterio di costo
7. Scelgo la lista di copertura a costo minimo
# Sintesi PS
Data $F$ da sintetizzare PS:
1. sintetizzo $\overline{F}$ in forma SP
2. Applico NOT alle variabili indipendenti
3. Sostituisco le AND con OR e le OR con AND
4. Ho ottenuto la PdS di $F$.
___Se la sintesi SP di $\overline z$ è a costo minimo, lo è anche la sintesi PS di $z$.___
$$
\overline z = (\overline a \cdot \overline b \cdot \overline c)+ (\overline a \cdot \overline b \cdot c) \dots \implies z = (a+b+c) \cdot (a+b+ \overline c )\dots
$$
# Sintesi a porte NAND di z
1. trovo la forma SdP di z
2. applico NOT solo ai termini costituiti da una sola variabile indipendente
3. rimpiazzo ogni AND e ogni OR con NAND
$$
z = \overline a + (b \cdot \overline c) \implies z=a \uparrow (b \uparrow \overline c)
$$
# Sintesi a porte NOR di z
1. trovo la forma SdP di $\overline z$ 
2. applico NOT esclusivamente alle variabili che compaiono in termini AND
3. sostituisco ogni operatore AND e ogni operatore OR con una NOR.
$$
\overline z = \overline a + ( b \cdot \overline c) \implies z = \overline a \downarrow(\overline b \downarrow c)
$$