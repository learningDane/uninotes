#uni 
La sintassi dipende dall'assemblatore che usi:
- GAS -> sintassi AT&T
- nasm -> sintassi
Il set di istruzioni invece dipende dal processore.
Sullo stesso set di istruzioni, assembly diversi, una volta assemblati hanno come risultato finale lo stesso linguaggio macchina.
# Set di Istruzioni x86-64
### Base comune
Tutte le CPU moderne compatibili x86-64 supportano:
	•	x86 a 16/32 bit (retrocompatibilità storica).
	•	x86-64 (AMD64) → introdotto da AMD, poi adottato da Intel.
	•	MMX, SSE, SSE2 → obbligatori da anni (usati in multimedia e calcoli vettoriali di base).
Questa è la parte di assembly che puoi usare ovunque, indipendentemente dalla CPU.
### Estensioni opzionali (dipendono dalla CPU)
Oltre al set base, ogni generazione aggiunge istruzioni nuove.
Esempi:
	•	SSE3, SSSE3, SSE4.1, SSE4.2 → ottimizzazioni multimediali (Intel/AMD).
	•	AVX, AVX2 → registri a 256 bit per calcolo vettoriale.
	•	AVX-512 → registri a 512 bit (presente su CPU server Intel e alcune desktop high-end, ma non su tutte).
	•	BMI1/BMI2 (Bit Manipulation Instructions) → operazioni bit-level più veloci.
	•	FMA (Fused Multiply-Add) → molto utile in calcoli scientifici e AI.
	•	AES-NI → accelerazione hardware per crittografia AES.
	•	SHA, VAES, VPCLMULQDQ → accelerazioni per sicurezza e crittografia.
	•	TSX (Transactional Synchronization Extensions) → supporto a transazioni hardware (presente su alcune CPU, poi rimosso in altre per bug di sicurezza).
	•	AMX (Advanced Matrix Extensions) → introdotto da Intel per AI/ML (Alder Lake e successive).
# Assemblatori
==Alcuni asemblatori sono case sensitive (GAS, NASM), altri no (MASM)==.
### a sintassi AT&T
- GAS e basta praticamente, è lo standard per Linux
Nota che GAS può utilizzare anche sintassi Intel.
### a sintassi Intel
- **Sviluppo Bare-Metal**: NASM, FASM.
- **Per sistemi Windows** e progetti che richiedono integrazione con Visual Studio: MASM è una scelta storica. 
- **Per progetti cross-platform, open-source o quando preferisci un'alternativa libera:** NASM e FASM sono ottime opzioni. 
- **Per integrare codice assembly direttamente nel tuo codice C/C++:** Gli assembler integrati sono la soluzione.
- Assemblatori integrati: cgg, clang
- altre opzioni: yasm
## Scelta di un Assemblatore
- **NASM** (Netwide Assembler): sintassi Intel
  - Didattica (imparare assembly)
  - Exploit/shellcode (molto usato in sicurezza)
  - OS development bare-metal (bootloader, kernel in assembly)
  - Programmi x86/AMD64 multipiattaforma
- **GAS** (GNU Assembler, parte di binutils): sintassi AT&T o Intel
  - Kernel Linux e driver
  - Toolchain GCC/Clang
  - Cross-compilazione (ARM, MIPS, RISC-V, ecc.)
  - Progetti accademici con GNU/LLVM
- **MASM** (Microsoft Macro Assembler): sintassi Intel
  - Programmazione di sistema su Windows
  - Driver, applicazioni che interagiscono con WinAPI
  - Retrocompatibilità con codice storico MS-DOS/Windows
# Sintassi AT&T
`MOVs source, destination`
- tutte le etichette sono seguite da «:»
- registri hanno prefisso % : %eax
- valori immediati hanno prefisso $ : $4
- utilizzo di suffisi per indicare la lunghezza degli operandi (MOVL/W/Q/B)
- parentesi tonde per indirizzamento
- valori immediati esadecimali: $0xValore
- valori immediati decimali: $valore
- commenti iniziano con #
`MOVL (%edi), %eax`
`MOVL 3(%edi), %eax`
# Sintassi Intel
`MOVs destination, source`
- solo le etichette istruzioni sono seguite da «:»
- registri e valori immediati non hanno prefisso
- nessun prefisso per indicare lunghezza degli operandi, si POSSONO usare invece byte ptr, word ptr, dword ptr: "MOVL (%edi), %eax" diventa "MOV eax, dword ptr [edi]"
- parentesi quadre per indirizzamento
- valori immediati esadecimali:
  si indicano inserendo il suffisso «h», il prefisso «0» SE iniziano con una lettera; oppure utilizzando il prefisso «0x»
- valori immediati decimali: valore
- commenti iniziano con ;
- `MOV eax, dword ptr [edi]` oppure `MOV eax, [edi]`
  in quanto nella sintassi intel la dimensione dell'operazione dipende dagli operandi, quindi l'uso di "DIMENSIONE ptr" è opzionale
- `MOV eax, [edi+3]
# Istruzioni
- inb %dx, %al/%ax
  prende un byte dalla porta di I/O all'offset in %dx e lo mette in dest
# x86_64 Standalone Assembly compiling with GCC
File must be **file.s** extension.
```asm
.global _start

.data
# data declared here

.section .text
_start:
    ; your instructions here
    
	mov $60, %rax     # sys_exit
    mov $0, %rdi      # exit code 0
    syscall
```

compiling:
```bash
gcc -nostdlib -o myprog file.s
```