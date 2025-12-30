#self-taught 
Make is a tool that lets automate compilation of programs, using instructions written in a Makefile.
Make only recompiles changed files.
# Makefile
The Makefile is a file where you put the compilation rules for the make command: when make is launched it will execute the compile command as specified in the rules in the Makefile.

Note that make with no arguments executes the first rule in the file. Furthermore, by putting the list of files on which the command depends on the first line after the :, make knows that the rule `ruleName` needs to be executed if any of those files change.
Immediately, you have solved problem #1 and can avoid using the up arrow repeatedly, looking for your last compile command. However, the system is still not being efficient in terms of compiling only the latest changes.

One very important thing to note is that there is a tab before the gcc command in the makefile. There must be a tab at the beginning of any command, and make will not be happy if it's not there.

If you were to make a change to hellomake.h, for example, make would not recompile the .c files, even though they needed to be. In order to fix this, we need to tell make that all .c files depend on certain .h files. We can do this by writing a simple rule and adding it to the makefile.
## Syntax
```Makefile
CC=desiredCompiler
DEPS = fileDependencies.h
OBJ = filesToCompile
IDIR = pathToDirectoriesForIncludeFiles
CFLAGS=desiredCompilerFlags -I$(IDIR)

%.o: %.c $(DEPS)
	$(CC) -c -o $@ $^ $(CFLAGS)

nameForTheEXE: &(OBJ)
	$(CC) $^ -o $@ $(CFLAGS)
	
.PHONY: clean
clean:
	rm -f $(ODIR)/*.o
```
- `$@` gets replaced with the item on the left side of the `:`
- `$^` gets replaced with the item on the right side of the `:`
- `make clean` executes the `clean` rule, which removes the object files
- `.PHONY` tells make that clean is not a file, so if you have files named clean they will not be targeted by make