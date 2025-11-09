#self-taught 
[link github](https://github.com/bergercookie/asm-lsp/tree/master)
Provide hovering, autocompletion, signature help, go to definition, and view references for assembly files written in the GAS/NASM or GO assembly flavors. It supports assembly files for the x86, x86_64, ARM, RISCV, z80, AVR, and 6502 instruction sets. Supported assemblers include the Gas, Go, Masm, Nasm, ca65, AVR, and FASM assemblers.

This tool can serve as reference when reading the assembly output of a program. This way you can query what each command exactly does and deliberate about whether the compiler is producing the desired output or whether you have to tweak your code for optimisation.
# .asm-lsp.toml
[[asm-lsp toml file for CE]] 
```toml
[default_config]
# Configure documentation available for features like hover and completions
assembler = "gas"
instruction_set = "x86/x86-64"

[opts]
# The `compiler` field is the name of a compiler/assembler on your path
# (or the absolute path to the file) that is used to build your source files
# This program will be used to generate diagnostics
compiler = "xxxxxxxxxxxx" # need "cc" as the first argument in `compile_flags.txt`
diagnostics = true
default_diagnostics = true

# Configure the server's treatment of source files in the `arm-project` sub-directory
[[project]]
path = "arm-project"
assembler = "xxxxxxxxxxxxxxx"
instruction_set = "xxxxxxxxxx"

[project.opts]
compiler = "zig"
compile_flags_txt = [
  "cc",
  "-x",
  "assembler-with-cpp",
  "-g",
  "-Wall",
  "-Wextra",
  "-pedantic",
  "-pedantic-errors",
  "-std=c2y",
  "-target",
  "aarch64-linux-musl",
]
```
### instruction_set
Valid options for the `instruction_set` field include:
- `"x86"`
- `"x86-64"`
- `"x86/x86-64"` (Enable both)
- `"arm"`
- `"arm64"`
- `"riscv"`
- `"z80"`
- `"6502"`
- `"avr"`
- `"mips"`
### assembler
Valid options for the `assembler` field include:
- `"gas"`
- `"go"`
- `"masm"`
- `"nasm"`
- `"ca65"`
- `"avr"`
- `"fasm"`
- `"mars"`
