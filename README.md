# RISC-V

### Course of content
- [Day 1: Introduction to RISC-V ISA and GNU compiler toolchain](#day-1-introduction-to-risc-v-isa-and-gnu-compiler-toolchain)
- [](#)


# Day 1: Introduction to RISC-V ISA and GNU compiler toolchain
- [RISC-V Toolchain Installation Guide](#risc-v-toolchain-installation-guide)
## RISC-V Toolchain Installation Guide

This guide outlines the steps to install a RISC-V toolchain on a Linux system. The toolchain is necessary for RISC-V development and includes various dependencies.

### Installation Steps
#### 1. Install Dependencies

Install the required dependencies using the following command:
```bash
sudo apt-get install libboost-regex-dev
```
#### 2. Clone the Repository

Clone the RISC-V workshop collaterals repository:

```bash
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh
```
Ignore any make errors that may occur during this step.
#### 3. Install Icarus Verilog

Navigate to the Icarus Verilog directory and set up Icarus Verilog:

```bash
cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull
chmod 777 autoconf.sh
./autoconf.sh
./configure
make
sudo make install
```
#### 4. Set up PATH Variable

To use the installed toolchain, add its path to your PATH variable. Open your .bashrc file:

```bash
gedit ~/.bashrc
```
Add the following line at the end of the file, replacing '<username>' with your actual username:

```bash
export PATH="/home/<username>/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH"
```
Save and close the .bashrc file.
#### 5. Update Environment

Update your environment by sourcing the .bashrc file:

```bash
source ~/.bashrc
```
### Instruction Set Architecture (ISA)
An Instruction Set Architecture (ISA) is a set of rules and specifications that define the instructions that a computer's processor can execute. It serves as a crucial interface between the hardware (the physical components of the computer) and the software (the programs and applications that run on the computer). The ISA essentially provides a standardized way for software to communicate with and utilize the underlying hardware resources.

Key aspects of an ISA include:

1. Instruction Formats: The ISA specifies the structure of instructions that the processor can execute. This includes fields for the operation to be performed, the operands involved, and addressing modes.
2. Operations: The ISA defines the set of basic operations or instructions that the processor can execute. These operations include arithmetic operations (add, subtract, multiply, divide), logical operations (AND, OR, NOT), memory operations (load, store), and control operations (branch, jump).
3. Registers: The ISA specifies the number and types of registers available in the processor. Registers are used to hold data temporarily during calculations, improving processing speed.
4. Memory Organization: The ISA outlines how the computer interacts with memory, including addressing modes and instructions for loading and storing data.
5. Data Types: The types of data that the processor can handle, such as integers, floating-point numbers, characters, and more, are defined in the ISA.
6. Addressing Modes: How memory addresses are calculated and used to access data in memory is detailed in the ISA.
7. Control Flow: The ISA provides instructions for controlling the flow of program execution, including branching to different parts of the program and handling interrupts and exceptions.
8. Privilege Levels: Some ISAs have multiple privilege levels to manage access to system resources and ensure security.
9. Endianness: The order in which multi-byte data is stored in memory (little-endian or big-endian) is specified by the ISA.

Different computer architectures (like x86, ARM, and RISC-V) have their own distinct ISAs. The ISA is crucial because it enables software developers to write code that is compatible with a specific processor or family of processors. It also allows hardware designers to create processors that can execute a wide range of software written for that ISA.



### RISC-V ISA
RISC-V (Reduced Instruction Set Computing - Five) emerges as an innovative instruction set architecture (ISA) initially designed to foster research and education in computer architecture. The RISC-V ISA comprises a foundational base integer ISA, which is obligatory in all implementations, supplemented by optional extensions that can be integrated with the base ISA. The base integer ISA echoes the principles of early RISC processors while eliminating branch delay slots and incorporating support for variable-length instruction encodings. The core is intentionally confined to a minimal set of instructions, adequate to serve as a practical target for compilers, assemblers, linkers, and operating systems (alongside additional supervisor-level operations). This approach establishes a functional ISA and software toolchain "framework" that can be tailored to create more specialized processor ISAs. The basic integer ISA is denoted as "I" (prefixed by RV32 or RV64, based on integer register width) and encompasses integer computational instructions, integer loads, integer stores, and control-flow instructions, being mandatory for all RISC-V implementations. The standard integer multiplication and division extension is labeled "M" and introduces instructions for multiplying and dividing values stored in integer registers. The standard atomic instruction extension, identified as "A," introduces instructions for atomic memory read-modify-write operations, facilitating inter-processor synchronization. The standard single-precision floating-point extension, referred to as "F," adds single-precision floating-point registers, computational instructions, and data transfer operations. The standard double-precision floating-point extension, termed "D," expands the floating-point register set and introduces double-precision computational instructions and data transfers. An integer base combined with these four standard extensions ("IMAFD") is abbreviated as "G," delivering a versatile scalar instruction set.


### Introduction to RISC-V basic keywords

