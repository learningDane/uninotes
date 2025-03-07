#uni 
GNU Octave è un'applicazione software per l'analisi numerica in gran parte compatibile con [[MATLAB]].
Octave can be run un "traditional mode", which gives errore when trying to use octave-only syntax.
```shell
octave --gui --traditional
```
# Differences Octave-Matlab
- Octave supports C-style increments: `i++; i+=1; ++i; ecc`
- Matlab differentiates between character strings and character arrays, solution: use `strcat()` for character string concatenation in octave
- `!string` calls a shell with command "string" in Matlab, octave will not recognize ! because it is used as a logical operator. Always use `system(string)` in matlab.
- Matlab lets you load empty files, octave does not
- octave supports both `fprintf` and `printf` whereas matlab requires `fprintf`
- Matlab does not support whitespace before transpose operator `A'` whereas octave also support the whitespace `A '`, as it is considered like every other operator.
- Matlab requires `...` for line continuation
```MATLAB
rand(1, ...
2)
   ```
   where octave supports this:
```octave
rand(1,
2)
 ```
     in both programs
 ```Octave
 R=[1 2 3
 7 8 9]
```
	shifts to the next row:
```
R=
 1 2 3
 7 8 9
```
- Octave supports `z=y=x+3` where Matlab requires two different assignements
- Octave supports
```Octave
global isOctave = (exist('OCTAVE_VERSION')>0);

%where matlab requires
global isOctave;
isOctave = (exist('OCTAVE_VERSION')>0);
```
- as for the logical NOT operator octave supports both `~` and `!`, where matlab only supports `~` 
- comments in octave can start with both `#` and `%`, matlab `%`
- for exponentiation octave uses both `^` and `**`, matlab `^`
- to end block octave can use both `end` or specify the block with `endif, endfor ecc`, matlab `end`
- octave supports C-style hexadecimal notaion `0xAABB`, matlab requires the `hex2dec` function: `hex2dec('AABB')`
### Specific differences
- `dbstep,in` -> `dbstep` ; `dbstep` -> `dbnext`
- `eig(A,B)` -> `qz(A,B)`
- `time()` is not available in matlab, use `now()`
- `textscan()` is not included in octave, use `fscanf()`
- setting labels for plots
```Octave
Octave:        plot(x, y, ';label;')
MATLAB/Octave: plot(x, y); legend('label')
```