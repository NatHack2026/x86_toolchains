This script, named "x86_toolchain.sh," is a versatile tool designed for assembling, compiling, linking, and executing x86 assembly code on a Linux system.
trust me it's useful
- It supports the assembly of both 32-bit and 64-bit x86 code, determined by the "--x86-64" option.

Key Features:
- Assembles x86 assembly code using NASM (Netwide Assembler).
- Compiles and links the assembly code using GCC (GNU Compiler Collection), allowing for the linking of external libraries.
- Easily debugging with GDB (GNU Debugger) by setting breakpoints 
- Offers emulation with QEMU (Quick Emulator) for running the resulting executable.

Command-Line Options {#I might have messed up with some syntax}:
- "-g" or "--gdb": Initiates GDB debugging on the generated executable.
- "-o" or "--output <filename>": Specifies the desired output filename for the executable.
- "-v" or "--verbose": Provides verbose output, displaying detailed information about the steps performed.
- "-64" or "--x86-64": Compiles for 64-bit (x86-64) architecture.
- "-q" or "--qemu": Runs the executable in the QEMU emulator.
- "-r" or "--run": Automatically runs the program in GDB after setting breakpoints.
- "-b" or "--break <break point": Sets a breakpoint in GDB, with the default breakpoint being "_start."
- "-l" or "--library <library nam>": it will link an external library to the executable during compilation.

= Example:
- To assemble and compile an x86 assembly file named "my_program.asm" for a 64-bit system, link an external library named "my_library.so," and set the output filename as "my_program," you can execute the following command:
