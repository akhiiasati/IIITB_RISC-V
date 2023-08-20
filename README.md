# RISC-V

### Course of content
- [RISC-V Toolchain Installation Guide](#risc-v-toolchain-installation-guide)
- [Day 1: Introduction to RISC-V ISA and GNU compiler toolchain](#day-1-introduction-to-risc-v-isa-and-gnu-compiler-toolchain)
- [Day 2: Introduction to ABI and basic verification flow](#day-2-introduction-to-abi-and-basic-verification-flow)
- [Day 3: Digital Logic with TL-Verilog and Makerchip](#day-3-digital-logic-with-tl-verilog-and-makerchip)


# RISC-V Toolchain Installation Guide

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
Add the following line at the end of the file, replacing " < username > " with your actual username:

```bash
export PATH="/home/<username>/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH"
```
Save and close the .bashrc file.
#### 5. Update Environment

Update your environment by sourcing the .bashrc file:

```bash
source ~/.bashrc
```

# Day 1: Introduction to RISC-V ISA and GNU compiler toolchain

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
RISC-V, which stands for "Reduced Instruction Set Computer - Five", is an open and royalty-free instruction set architecture (ISA) designed for various computing tasks. It is characterized by its modular design, allowing for customization and specialization based on application needs. The RISC-V ISA comes in several standard variations, denoted by different letter extensions:

#### 1. Base Integer ISA:
- RV32I: 32-bit base integer ISA.
- RV64I: 64-bit base integer ISA.
- RV128I: 128-bit base integer ISA (less common).

#### 2. Integer Multiply and Divide (M) Extension:
- RV32M: 32-bit base integer ISA with multiplication and division instructions.
- RV64M: 64-bit base integer ISA with multiplication and division instructions.

#### 3. Single-Precision Floating-Point (F) Extension:
- RV32F: 32-bit base integer ISA with single-precision floating-point instructions.
- RV64F: 64-bit base integer ISA with single-precision floating-point instructions.

#### 4. Double-Precision Floating-Point (D) Extension:
- RV32D: 32-bit base integer ISA with double-precision floating-point instructions.
- RV64D: 64-bit base integer ISA with double-precision floating-point instructions.

#### 5. Atomic (A) Extension:
- Adds atomic memory operations.

#### 6. Vector (V) Extension:
- Adds vector processing instructions.

#### 7. Floating-Point Extension (F and D combined):
- RV32F and RV64F: Base integer ISAs with both single-precision and double-precision floating-point instructions.

#### 8. Privileged Architecture (P) Extension:
- Adds supervisor and hypervisor modes, virtual memory support, and privilege levels.

#### 9. Custom Extensions:

- Beyond the standard extensions, RISC-V allows custom extensions to tailor the architecture for specific applications.

It's worth noting that RISC-V is designed to be modular, which means that specific implementations can choose which extensions to include based on their requirements. This flexibility makes RISC-V suitable for a wide range of applications, from embedded systems to high-performance computing.


### Introduction to RISC-V basic keywords

