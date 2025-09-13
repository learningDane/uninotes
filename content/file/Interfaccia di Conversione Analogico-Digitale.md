#uni 
>![[interfacciaAD1.svg|350]]
>Schema Funzionale di una semplice interfaccia per la conversione analogico-digitale.

>![[interfacciaAD2.svg|600]]
>Struttura interna di una semplice interfaccia per la conversione analogico-digitale.

# Software di input
```C
byte inputAD {
	#define RCR_offset ...
	#define RSR_offset ...
	#define RBR_offset ...
	byte tmp;
	
	outport(RCR_offset, 0x02); // metto soc==1
	do (tmp = ( inport(RSR_offset) & 0x01 ) while (tmp == 1);
	// ora eoc == 0
	outport(RCR_offset, 0x00); // metto soc==0
	do (tmp = ( inport(RSR_offset) & 0x01 ) while (tmp == 0);
	// ora eoc == 1
	return inport(RBR_offset);
}
```