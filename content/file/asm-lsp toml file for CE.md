```toml
[default_config]
# Configure documentation available for features like hover and completions
assembler = "gas"
instruction_set = "x86/x86-64"

[opts]
# The `compiler` field is the name of a compiler/assembler on your path
# (or the absolute path to the file) that is used to build your source files
# This program will be used to generate diagnostics
compiler = "g++" # need "cc" as the first argument in `compile_flags.txt`
diagnostics = true
default_diagnostics = true

# Configure the server's treatment of source files in the `arm-project` sub-directory
[[project]]
path = "/Users/davidesqueri/CE"
assembler = "gas"
instruction_set = "x86-64"

[project.opts]
compiler = "gas"
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