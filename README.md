The better toolchain provides a  toolchain for managing assembly projects, adaptable to both x86 and ARM architectures **I havent fully tested it for ARM.
{I put placeholders for ARM assembly and linking commands, because it needs to be replaced with actual commands suitable for ARM environment}.  The placeholders for ARM-specific commands are clearly marked, and the script includes more robust error handling and verbose output.

#{
#Prerequisites:
You need all required tools (like NASM* like in vscode or in terminal , GCC, QEMU, GDB) are installed on ur system for the script to function correctly. 


For ARM:
__________________________________
#1 GCC
Install ARM GCC:
apt-get install gcc-arm-linux-gnueabihf
***u can use qemu*
#3 GDB-Multiarch
Install Multiarchitecture GDB
apt-get install gdb-multiarch
______________________________________

For x86:
_______________________________________________________
Install GDB
sudo apt-get update && sudo apt-get install gdb

#1 Install GEF
#--use curl
$ bash -c "$(curl -fsSL https://gef.blah.cat/sh)"
#2 u can use wget
$ bash -c "$(wget https://gef.blah.cat/sh -O -)"
#3 PATH:
add toolchain script to PATH:
echo 'export PATH=$PATH:~/ITSC204/scripts' >> ~/.bashrc
________________________________________________________
#}


To compile an x86 assembly file with NASM and GCC, and optionally link an external library:
./x86_toolchain.sh file.asm -l libraryname

To compile for ARM (e.g., Raspberry Pi 3B) and run with QEMU:
./x86_toolchain.sh -a -p 3B file.asm -q    ** 3B is the model

For debugging with GDB:
./x86_toolchain.sh -g -b _start file.asm


1. Usage Instructions and Argument Parsing
The script begins by checking if an assembly file is provided. If not, it displays usage instructions and exits. This ensures that the user is aware of how to properly use the script.
2. Command-Line Options
General Options:
-v | --verbose: Enables verbose output, providing detailed information on each step performed by the script.
-g | --gdb: Enables GDB debugging for the compiled executable.
-b | --break <break point>: Sets a breakpoint in GDB, defaulting to _start.
-r | --run: Automatically runs the program in GDB after setting breakpoints.
-q | --qemu: Executes the compiled executable in the QEMU emulator.
-o | --output <filename>: Specifies the output filename for the executable.
-l | --library <library>: Links an external library to the executable during compilation.
Architecture-Specific Options:
-a | --arm: Switches the compilation target to ARM architecture.
-p | --pi <model>: Specifies the Raspberry Pi model (3B or 4) for ARM compilation. **I have played around with rasberry pi using python
-32 | --x86-32: Compiles for 32-bit x86 architecture; * the default is 64-bit.
3. Assembly and Linking
ARM Assembly and Linking:
If the ARM option is selected, the script differentiates between Raspberry Pi 3B and 4 models.  ** But, the actual assembly commands for these models are placeholders and need to be filled in with appropriate ARM toolchain commands.
Command-Line Options (continued):

-l | --library <library>: This option allows the user to link an external library with the executable. It's particularly useful when the assembly code depends on external functions or resources.
Architecture-Specific Options:

-32 | --x86-32: When this flag is set, the script will compile for 32-bit x86 architecture. By default, the script compiles for 64-bit, making this option useful for legacy or specific 32-bit applications.
-a | --arm: This option switches the compilation target to ARM architecture. It's essential for cross-compiling code for ARM-based systems like Raspberry Pi.
-p | --pi <model>: This option allows the user to specify the Raspberry Pi model (3B or 4) for ARM compilation,  good for optimizing the compiled code for a specific hardware model.

For x86, the NASM assembler is used with the appropriate flags (-f elf for 32-bit and -f elf64 for 64-bit). It  will assembles the source file into an object file.

The script supports running the compiled executable in QEMU{mimics different CPU architectures}. **useful for testing executables in an environment different from the host system, such as emulating ARM architecture on an x86 machine.

Error Checking: The script checks for the existence of the input file, ensuring that the compilation process doesn't proceed with a non-existent file.

Output File Customization: I have the flexibility to specify the output filename, which is useful for organizing and managing different versions or variants of the compiled executables.
Verbose Output: if enabled, the feature will give me a detailed log of the script's operations
