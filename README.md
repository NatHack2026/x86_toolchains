I call it THE BETTER TOOL , the x86_toolchain.sh script is an all-encompassing solution for managing and compiling assembly projects. It is crafted with a special focus on x86 architecture and is equipped with placeholders for ARM-specific commands, ensuring broad compatibility and flexibility.

Description:

**The script is adept at both x86 and ARM architectures, modifying its assembly and linking commands based on the selected compilation target. It features robust error-checking to capture and handle any issues encountered during the assembly or linking phases.

**Linux Compatibility: It is designed to work on Linux-based systems like Ubuntu and Debian*
This script initiates its workflow with a check_dependencies function that determines the operating system and installs essential tools such as NASM, LD, GCC, QEMU, and GDB. This guarantees that all the required software is available for seamless operation.
_____________________________________________________________________________________________
The parse_arguments function is designed to interpret user-input command-line arguments, managing various flags and options efficiently. Additionally, the -l or --library option allows you to link external libraries into your assembly program.

Designed to function on Linux-based systems such as Ubuntu and Debian, the script also includes conditional checks to ensure compatibility with macOS. For Windows users, guidance is provided for using CYGWIN, which emulates a POSIX environment, or MinGW, a minimalist GNU for Windows.

macOS Compatibility: The script also includes support for macOS by using the brew package manager to install the necessary tools, the script should work on macOS, provided that it has Homebrew installed, which is a common package manager for macOS.

Windows Instructions: For Windows users, the script provides instructions for manual installation of the necessary tools when working within Cygwin or MinGW environments. However, it doesn't automate the process and relies on the user/me to set up my environment accordingly.

Cygwin and MinGW Recognition: The script acknowledges the use of Cygwin and MinGW, which are both sets of tools that allow the running or compilation of Unix-like applications in a Windows environment.

Conditional Checks: The script uses conditional statements based on the output of uname -s to determine the operating system and run the appropriate commands for dependency installation.




COMMANDS:
______________________________________________________________________________
Compiling x86 Assembly with External Libraries
To compile an x86 assembly file and link it with an external library, use:
./x86_toolchain.sh file.asm -l libraryname

For example, to link with the standard math library:
./x86_toolchain.sh file.asm -o outputfile -l m
______________________________________________________________________________


Compiling for ARM Architecture
The script is set up to compile for ARM architectures and run the output with QEMU. However, the actual ARM assembly commands are currently placeholders and require further customization:
./x86_toolchain.sh -a -p 3B file.asm -q



Debugging with GDB
To enable debugging with GDB and a breakpoint at _start, use:-->
--------->       ./x86_toolchain.sh -g -b _start file.asm



PREREQUISITES AND SETUP
For x86 Assembly
Ensure NASM, GCC, and GDB are installed. You can add the toolchain script to your PATH for easy access:

echo 'export PATH=$PATH:~/ITSC204/scripts' >> ~/.bashrc


For ARM Assembly
Install the ARM GCC cross-compiler and GDB-Multiarch:
apt-get install gcc-arm-linux-gnueabihf
apt-get install gdb-multiarch


To compile and run ARM assembly with QEMU:
./x86_toolchain.sh -a -p 3B file.asm -q


Installation of GDB for Debugging
sudo apt-get update && sudo apt-get install gdb

To enhance GDB, install GEF with curl or wget, then add it to your PATH.
1 Install GEF
#-USE wget 
bash -c "$(wget https://gef.blah.cat/sh -O -)"
add toolchain script to PATH:
echo 'export PATH=$PATH:~/ITSC204/scripts' >> ~/.bashrc


Features
Verbose Output: The -v or --verbose flag offers detailed output for each operation.
GDB Integration: The -g flag enables the use of GDB for debugging executables.
Breakpoint Management: The -b flag sets breakpoints within GDB, defaulting to the _start label.
Automatic Execution: The -r flag automates the running of programs within GDB post-breakpoint setup.
QEMU Support: The -q flag allows running the compiled executable in the QEMU emulator.
Output Specification: The -o flag lets users define the output filename, enhancing build management.
Library Linking: The -l flag allows for the linking of external libraries during compilation.
For x86 architecture, the script employs NASM for assembly and LD for linking, adjusting compilation flags for 32-bit (-32 or --x86-32) or 64-bit (-64 or --x86-64) as per the user's choice.

RUNNING CODE:

For x86: 
32 bits---->
-->      ./x86_toolchain.sh --x86-32 -o math math.s
This tells the script to compile math.s for 32-bit x86 architecture and name the output math. 
then-->
-->       ./math

64bits----->
-->        ./x86_toolchain.sh --x86-64 -o program program.asm
then-->
-->        ./program

MAKE TOOLCHAIN EXECUTABLE:
ls ~/itsc204
sudo mv ~/itsc204/x86_toolchain.sh /usr/local/bin/
mkdir -p ~/bin
mv ~/itsc204/x86_toolchain.sh ~/bin/
echo 'export PATH="$PATH:$HOME/bin"' >> ~/.bashrc
source ~/.bashrc  <----------------- // Not always neccessary/depends \\
chmod +x ~/bin/x86_toolchain.sh
