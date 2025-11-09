#uni 
Network Assembly

If you are using NASM in Ubuntu 18.04, the commands to compile and run an .asm file named hello.asm are:
```shell
nasm -f elf64 hello.asm # assemble the program  
ld -s -o hello hello.o # link the object file nasm produced into an executable file  
./hello # hello is an executable file
```