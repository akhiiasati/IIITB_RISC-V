# RISC-V

### Table of content
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
- [RISC-V Introduction](#risc-v-introduction)
  - [RISC-V: A Transformative ISA for Innovation](#risc-v-a-transformative-isa-for-innovation)
  - [RISC-V Characteristics](#risc-v-characteristics)
  - [RISC-V Foundation and RISC-V International](#risc-v-foundation-and-risc-v-international)
  - [RISC-V Architecture](#risc-v-architecture)
  - [ISA base and extensions](#isa-base-and-extensions)
  - [From Application Software to Hardware Execution: A Flow Overview](#from-application-software-to-hardware-execution-a-flow-overview)
- [Labwork for RISC-V software toolchain](#labwork-for-risc-v-software-toolchain)
- [Data Representation and Storage in RISC-V](#data-representation-and-storage-in-risc-v)
  - [Unsigned Numbers](#unsigned-numbers)
  - [Signed Numbers](#signed-numbers)
  - [Exploring Unsigned Number Representation in RISC-V](exploring-unsigned-number-representation-in-risc-v)
  - [Exploring Signed Number Representation in RISC-V](exploring-signed-number-representation-in-risc-v)


### RISC-V: A Transformative ISA for Innovation

RISC-V, known as "Reduced Instruction Set Computing - Five," is a transformative open-source instruction set architecture (ISA) born from a commitment to advancing computer architecture research and education. With its roots tracing back to the pioneering work of Prof. David Patterson and Prof. John Hennessy, RISC-V redefines chip design, embodying decades of research. It follows a RISC approach, strategically positioning instruction bit fields for simplified CPU design and employing IEEE 754 floating-point precision. Unlike traditional ISAs, RISC-V operates under open-source licenses, offering an edge in flexibility, scalability, and innovation. Led by Prof. Krste Asanović, Yunsup Lee, and Andrew Waterman, its accessible framework empowers ease of processor creation and customization, signifying a new era in instruction set architectures.

![riscv_social](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/d180be06-b618-466d-82ef-7fe5bf0fd92a)


### RISC-V Characteristics

- Is a proven ISA and follows established RISC design principles
- Has single-cycle instructions
- Uses a load-store architecture
- Features a simple, stable, software-centric design (small, fixed base with modular fixed-standard extensions)
- Is modular, layered and extensible, allowing for software and hardware freedom on architecture
- Flexible and scalable (i.e., suitable for microcontrollers to personal computers to supercomputers)
- Has 32- and 64-bit variants and extensions to support floating point instructions
- Is supported by various language compilers (e.g., GNU Compiler Collection and Linux operating system)
- Offers a range of hardware support from microcontrollers to systems on module, systems on chip and field programmable gate arrays
- Accelerates the design-to-market timeline through collaboration and open source IP reuse

### RISC-V Foundation and RISC-V International

Established in 2015, the RISC-V Foundation responded to the need for a stable instruction set architecture (ISA) suitable for prolonged commercial use. With a commitment to stability, it took charge of intellectual property related to RISC-V's definition. Among the founding members were innovative entities such as Andes, Google, IBM, SiFive, and even IIT Madras, collectively shaping RISC-V's journey. In 2019, the foundation's transformation into RISC-V International marked its relocation to Switzerland, underlining its commitment to openness and stability. This shift, while maintaining document accessibility, granted member organizations the power to endorse changes and use the trademarked compatibility logo, fostering a collaborative evolution.For more information visit the site : www.riscv.org

![risc-v-members](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/251e4e94-c95b-4001-8f2f-02d1be575fc6)

### RISC-V Architecture
![RV12_Arch](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/37da2807-71df-4938-876f-18fde63a8edb)

### ISA base and extensions

The RISC-V instruction set architecture (ISA) is organized into a core "base" instruction set and optional "extensions" that provide additional functionality. This modular design allows for flexibility and customization, enabling different implementations tailored to specific application requirements.

| Component          | Description                                        |
|-------------------|----------------------------------------------------|
| **ISA Base**      |                                                    |
| Base Integer      | Integer arithmetic and logical operations          |
| Base Load/Store   | Load and store instructions                        |
| Base Control Flow | Control flow instructions (branches and jumps)    |
| Base System       | System-related instructions (e.g., environment)   |
| **Extensions**    |                                                    |
| **M** Extension   | Integer multiplication and division instructions |
| **A** Extension   | Atomic memory operations                          |
| **F** Extension   | Single-precision floating-point operations       |
| **D** Extension   | Double-precision floating-point operations       |
| **C** Extension   | Compressed instructions                           |
| **G** Extension   | Additional general-purpose registers             |
| **I** Extension   | Custom fixed-point instructions                  |
| **V** Extension   | Vector processing instructions                   |
| **B** Extension   | Bit manipulation instructions                    |
| **T** Extension   | Transactional memory support                     |
| **J** Extension   | Dynamic linking and JIT compilation support      |
| **P** Extension   | Packed-SIMD instructions                         |


### From Application Software to Hardware Execution: A Flow Overview

When a C program is intended to run on hardware, it goes through several stages. Initially, it's translated into RISC-V assembly language. Then, this assembly language is converted into binary machine language, which the hardware understands. The link between RISC-V assembly language and the chip's physical layout is established using Hardware Description Language (HDL), closely tied to hardware operations.

To define a RISC specification, the architecture is implemented to facilitate data transfer through registers. This involves transitioning from the Register Transfer Level (RTL) to the chip layout in an RTL to GDSII flow. This ensures applications operate seamlessly on the hardware.

To make an application function on hardware, it navigates the software system, involving the Operating System (OS), compiler, and assembler. The OS manages I/O and memory, the compiler translates high-level code into hardware-specific instructions (like RISC-V for RISC-V systems), and the assembler converts these into binary machine language. This binary, the bridge between C and hardware, follows the Instruction Set Architecture (ISA), establishing a link between software and hardware through binary instructions.

![Screenshot 2023-08-20 182714](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/5a6ebdcb-952a-4db2-aa9f-175908a42fd6)
![Screenshot (28)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/2b71de6f-9d17-463b-a9c3-f62d7edb473c)
![Screenshot (29)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/2b592370-b9c6-460d-a128-89f858eaa589)

## Labwork for RISC-V software toolchain

Let's condsider the below C program
```bash
#include<stdio.h>
int main()
{
    int i, sum = 0, n = 9;
    for (i = 1; i <= n; i++)
        sum += i;
    printf("The sum of numbers from 1 to %d is %d\n", n, sum);
    return 0;
}
```

Compilation:

```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton_O1.o sum1ton.c
```
This command uses the RISC-V architecture-based GCC compiler to compile the C source file sum1ton.c into an object file named sum1ton_O1.o. Here's the breakdown of the flags used:

- -O1: Specifies the optimization level as 1, representing a basic level of optimization.
- -mabi=lp64: Sets the ABI to "Long and Pointer 64-bit," indicating the size of long integers and pointers is 64 bits.
- -march=rv64i: Generates code for the RISC-V ISA with the base integer instruction set.
- -o sum1ton_O1.o: Specifies the output filename as sum1ton_O1.o.

Disassembly:

To view the disassembled code, use the riscv64-unknown-elf-objdump command:
```bash
riscv64-unknown-elf-objdump -d sum1ton_O1.o | less
```
- This command disassembles the compiled object file sum1ton_O1.o using the riscv64-unknown-elf-objdump tool. The -d flag tells objdump to display the disassembled code. The | less part of the command pipes the output of objdump into the less command, which allows you to view the disassembled code interactively.

![Screenshot from 2023-08-20 21-55-14](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/60c2291e-e95a-4de8-8883-fe9b40dccba4)

Execution on Spike Simulator:

```bash
spike pk sum1ton_O1.o
```

- This command uses the spike simulator to execute the compiled program sum1ton_O1.o. The pk argument indicates that you want to run a "proxy kernel" program. In this case, the program sum1ton_O1.o is executed on the simulated RISC-V architecture provided by the Spike simulator.

![Screenshot from 2023-08-20 21-54-46](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/ae7cdd43-487a-46f0-b272-08bb0d4a9df6)

This series of steps transforms the C code into RISC-V assembly code, compiles it, and then executes it using the Spike simulator, providing insights into how the C program operates in terms of RISC-V instructions. The -O1 optimization level in the compilation can affect the generated assembly code, optimizing it for performance while maintaining the functional behavior of the original C code.


### Debugging with Spike:
```bash
spike -d pk sum1ton_O1.o
```
This command starts the Spike simulator in debug mode (-d) and specifies that the program sum1ton_O1.o should be executed using the proxy kernel (pk).

Setting Breakpoint:
```bash
until pc 0 10184
```
This command sets a breakpoint at address 0x10184. This breakpoint will pause the execution when the program's Program Counter (PC) reaches that specific address.

Inspecting Register:
```bash
reg 0 sp
```
This command inspects the value stored in register a0 (stack pointer) and displays its current value.

Executing Line by Line:
Press "Enter" to execute the program line by line after setting the breakpoint. The program will execute one line at a time, and you can observe the register values and memory changes as the program progresses.

Inspecting Another Register:

```bash
reg 0 a2
```
This command inspects the value stored in register a2 and displays its current value.
![Screenshot from 2023-08-20 22-12-37](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/addd4d61-1df4-4d74-9841-ad277a035e87)

Using these commands in the Spike simulator, you can step through the program's execution line by line, inspecting register values and memory changes at each step. This can be helpful for debugging and understanding the behavior of the program.

### Ofast Mode in GCC and RISC-V Assembly Compilation

The "Ofast" mode is an optimization level in the GNU Compiler Collection (GCC) that enables aggressive optimization options to maximize code performance. This mode goes beyond the usual optimization levels and can result in significantly faster code execution, but it might sacrifice some standards compliance or strictness in favor of performance.

Here, we will document the process of compiling a C program named "sum1ton.c" using the "Ofast" mode in the RISC-V architecture using the riscv-gnu-toolchain. The C program presumably calculates the sum of integers from 1 to N. The steps are as follows:

Compile the above C Program in Ofast Mode:

Use the riscv64-unknown-elf-gcc compiler from the RISC-V GNU Toolchain to compile the "sum1ton.c" program in Ofast mode. The -Ofast flag enables aggressive optimization. The -mabi=lp64 flag specifies the ABI (Application Binary Interface) to use 64-bit long and pointer types. The -march=rv64i flag specifies the target architecture as RISC-V 64-bit integer-only base.

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton_Ofast.o sum1ton.c
```

Disassemble the Compiled Object File:

Use the riscv64-unknown-elf-objdump tool to disassemble the compiled object file "sum1ton_Ofast.o" into human-readable assembly code. The less command is used to view the output one screen at a time.

```bash
riscv64-unknown-elf-objdump -d sum1ton_Ofast.o | less
```

Run the Assembly Code in the RISC-V Spike Simulator:
Use the "spike pk" command to run the compiled object file in the RISC-V Spike simulator. Spike is a functional RISC-V ISA simulator that can execute RISC-V binaries.

```bash
spike pk sum1ton_Ofast.o
```

The above steps summarize the process of compiling the "sum1ton.c" C program in "Ofast" mode using the RISC-V GNU Toolchain and then disassembling and simulating the compiled object file using the RISC-V Spike simulator.

![Screenshot from 2023-08-20 22-18-11](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/05910d07-007b-473f-8e4d-577d92399e7f)
![Screenshot from 2023-08-20 22-18-36](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/6bda54df-71c0-463a-8514-57de848aecba)

Note: When compiling the same C code in "Ofast" mode, it utilizes a smaller number of instructions in comparison to the "O1" mode. This discrepancy can be attributed to the "Ofast" mode's heightened level of aggressiveness in optimization, which seeks to extract superior code performance at the potential expense of adhering strictly to language standards or preserving certain code structures. Consequently, the resulting assembly code from "Ofast" mode is streamlined and efficient, accomplishing the same computational task with fewer instructions than the assembly generated under the relatively more conservative "O1" optimization mode.

### Data Representation and Storage in RISC-V

In RISC-V and computer architecture in general, several terms relate to data representation and storage. Let's explore them:

![Screenshot (45)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/b27c8370-7575-4622-9816-fb974851b1eb)

- Byte: A byte is the fundamental unit of data storage and representation in computers. It consists of 8 bits and can represent a single character or value.

- Word: A word typically refers to the natural data size that a processor operates with. In RISC-V, the term "word" can vary based on the architecture. For example, in RV32 (32-bit architecture), a word is 4 bytes (32 bits), while in RV64 (64-bit architecture), a word is 8 bytes (64 bits).

- Double Word: A double word is twice the size of a word. In RISC-V, for example, in RV32, a double word is 8 bytes (64 bits), and in RV64, a double word is 16 bytes (128 bits).

- Least Significant Bit (LSB): The least significant bit is the lowest-order bit in a binary representation.

- Most Significant Bit (MSB): The most significant bit is the highest-order bit in a binary representation. It has the greatest influence on the overall value of a number. The MSB is the bit that represents the largest power of two.

- Endianness: Endianness refers to how multi-byte data is stored in memory. In a big-endian system, the most significant byte is stored at the lowest memory address, while in a little-endian system, the least significant byte is stored at the lowest memory address. RISC-V supports both big-endian and little-endian modes.

- Byte Addressing: Byte addressing is a memory addressing scheme used in computer systems to identify and access individual bytes of data within the computer's memory. In byte addressing, each individual byte in the memory has a unique address, allowing direct access to and manipulation of single bytes of data. In RISC-V, like in many other computer architectures, memory is byte-addressable.

- Understanding these terms is crucial when working with data representation, memory allocation, and programming in computer systems, including the RISC-V architecture.

### Representation of Signed and Unsigned Numbers

#### Unsigned Numbers:

Unsigned numbers don't have any sign; they can only contain the magnitude of the number. The representation of unsigned binary numbers consists of all positive numbers. Since there is no sign bit in this representation, an N-bit binary number represents its magnitude only. Zero (0) is also an unsigned number. Every number in unsigned number representation has only one unique binary equivalent form, making it an unambiguous representation technique. The range of unsigned binary numbers is from 0 to ((2^n)-1).

#### Signed Numbers:
Generally, the 2's complement representation is used for signed numbers. The 2’s complement of a number is obtained by inverting each bit of the given number and adding 1 to the least significant bit (LSB). Positive numbers are represented in binary form, while negative numbers are represented in 2’s complement form. An extra bit is used for sign representation. If the value of the sign bit is 0, the number is positive and can be directly represented in a simple binary form. If the value of the sign bit is 1, the number is negative, and the 2’s complement of the given binary number should be taken. In this representation, zero (0) has only one (unique) representation, which is always positive. The range of 2’s complement form is from (-2^(n-1)) to ((2^(n-1))-1).

![Screenshot (52)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/a9a458ef-8715-4634-be75-58b533f29656)

### Exploring Unsigned Number Representation in RISC-V

This section focuses on a C code snippet that demonstrates the concept of unsigned numbers in the RISC-V architecture. The code's purpose is to calculate and illustrate the highest value that an unsigned number can represent within the RV64I instruction set. We provide in-depth explanations and instructions, thoroughly explaining the code's features and functionality:

```bash
#include<stdio.h>
#include<math.h>

int main()
{
    unsigned long long int max = (unsigned long long int)(pow(2,64)-1); //Line 1
    // unsigned long long int max = (unsigned long long int)(pow(2,127)-1);// Line 2
    // unsigned long long int max = (unsigned long long int)(pow(2,64)*-1);// Line 3
    // unsigned long long int max = (unsigned long long int)(pow(-2,64)-1);// Line 4
    // unsigned long long int max = (unsigned long long int)(pow(-2,63)-1);// Line 5
    // unsigned long long int max = (unsigned long long int)(pow(2,10)-1);// Line 6
    printf("Highest number represented by unsigned long long int is %llu \n", max);
    return 0;
}
```
#### Explanation and Execution:

    %llu: Format specifier for printing a 64-bit unsigned integer.
    %lld: Format specifier for printing a 64-bit signed integer.

By uncommenting different lines in the code, various scenarios are demonstrated along with their outcomes:

    Line 1: Calculates and prints the result of (2^64)-1. This represents the highest value that can be stored in a 64-bit unsigned integer.

    Line 2: While the code attempts to calculate (2^127)-1, it actually yields (2^64)-1 since the maximum value a 64-bit unsigned integer can represent is (2^64)-1.

    Line 3: Calculates and prints the result of 0. This occurs due to the fact that the minimum unsigned value that a 64-bit register can store is 0.

    Line 4: Calculates and prints the result of 0. Similar to Line 3, this result exceeds the representable range for a 64-bit unsigned integer.

    Line 5: Calculates and prints the result of 0. As with Lines 3 and 4, the minimum representable value in a 64-bit unsigned integer is 0.

    Line 6: Calculates and prints the result of 1024. In this case, the value of max is smaller than (2^64)-1.

#### Compiling and Executing the Code:

For compiling and executing the C code using the RISC-V GNU toolchain, follow these steps:
```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c
```
Execute the compiled object file using the RISC-V Spike simulator:

    spike pk unsignedHighest.o

![Screenshot from 2023-08-20 22-51-25](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/bc98fd52-aad8-4f35-a585-b0bce6517c79) 

### Exploring signed Number Representation in RISC-V

This section provides insights into a C code snippet that showcases the behavior of signed numbers within the RV64I instruction set of the RISC-V architecture. The code is designed to determine and demonstrate the maximum and minimum values that can be stored using signed 64-bit integers. The code snippet, along with compilation and execution instructions, is detailed below:

```bash
#include<stdio.h>
#include<math.h>

int main()
{
    long long int max = (long long int)(pow(2,63)-1);
    long long int min = (long long int)(pow(-2,63));
    printf("Highest number represented by long long int is %lld \n", max);
    printf("Smallest number represented by long long int is %lld \n", min);
    return 0;
}
```

#### Explanation and Execution:

By employing the mathematical function pow(), this code determines the maximum and minimum values that a 64-bit signed integer can hold:

    max: This variable calculates and displays the result of (2^63)-1. This represents the highest value that a 64-bit signed integer can represent.

    min: This variable computes and prints the result of -2^63, which is the smallest value that a 64-bit signed integer can represent.

The code then uses printf() to display the calculated values for both the maximum and minimum signed numbers.

#### Compiling and Executing the Code:

For compiling and running the C code using the RISC-V GNU toolchain, follow these steps:

Compile the C code using the RISC-V GCC compiler:

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signedHighest.o signedHighest.c 
```

Run the compiled object file using the RISC-V Spike simulator:

    spike pk signedHighest.o 

#### Output of the Execution:

Upon running the code with the provided instructions, you will see the output that displays the highest and smallest numbers representable by a long long integer in the RV64I architecture.

![Screenshot from 2023-08-20 22-57-53](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/4dc7a451-d51c-4c77-9f9a-5065d315d866)

#### Different Data-Types:
![Screenshot 2023-08-20 230354](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/4a00b43f-9659-45f1-a76c-9db335328ee1)

# Day 2: Introduction to ABI and basic verification flow
- [Base Integer Instruction Set RV64I](#base-integer-instruction-set-rv64i)
  - [General-Purpose Registers and Operand Types](#general-purpose-registers-and-operand-types)
  - [Instruction Formats and Types](#instruction-formats-and-types)
- [Application Binary Interface (ABI) in RISC-V](#application-binary-interface-(abi)-in-risc-v)
  - [Introduction](#introduction)
  - [Key Points about ABI in RISC-V](key-points-about-abi-in-risc-v)
  - [Register File](#register-file)
  - [Types of Instructions](#types-of-instructions)
  - [Register Accessibility and Representation](#register-accessibility-and-representation)
- [Labwork](labwork)
  - [Labwork Using ABI Function Calls](#labwork-using-abi-function-calls)
  - [ASM Flow Chart](#asm-flow-chart)
  - [Verification Flow Description](#verification-flow-description)


## Base Integer Instruction Set RV64I

RV64I serves as the base integer instruction set for the 64-bit architecture, building upon the RV32I variant. While RV64I shares most instructions with RV32I, there are differences in register width and additional instructions in RV64I. The base integer instruction set comprises 47 instructions, derived from both RV32I and RV64I (35 from RV32I and 12 from RV64I). Below are the instructions:

| **Opcode** | **Name**                  | **Format** | **Description**                                                        |
|-----------|---------------------------|------------|------------------------------------------------------------------------|
| LUI       | Load Upper Immediate      | U-Type     | Load a 20-bit immediate into the upper 32 bits of a register.         |
| AUIPC     | Add Upper Immediate to PC | U-Type     | Add a 20-bit immediate to the PC and store the result in a register.  |
| JAL       | Jump and Link            | J-Type     | Jump to a target address and store the return address in a register.  |
| JALR      | Jump and Link Register    | I-Type     | Jump to a target address using an offset and store the return address.|
| BEQ       | Branch Equal             | B-Type     | Branch to a target address if two registers are equal.                |
| BNE       | Branch Not Equal         | B-Type     | Branch to a target address if two registers are not equal.            |
| BLT       | Branch Less Than         | B-Type     | Branch to a target address if one register is less than another.      |
| BGE       | Branch Greater Equal     | B-Type     | Branch to a target address if one register is greater than or equal.  |
| BLTU      | Branch Less Than (Unsigned) | B-Type | Branch if one register is less than another (unsigned comparison).    |
| BGEU      | Branch Greater Equal (Unsigned) | B-Type | Branch if one register is greater than or equal (unsigned comparison). |
| LB        | Load Byte                | I-Type     | Load a byte from memory into a register with sign extension.         |
| LH        | Load Half                | I-Type     | Load a halfword from memory into a register with sign extension.     |
| LW        | Load Word                | I-Type     | Load a word from memory into a register.                              |
| LBU       | Load Byte (Unsigned)     | I-Type     | Load a byte from memory into a register without sign extension.      |
| LHU       | Load Half (Unsigned)     | I-Type     | Load a halfword from memory into a register without sign extension.  |
| SB        | Store Byte               | S-Type     | Store the low byte of a register into memory.                         |
| SH        | Store Half               | S-Type     | Store the low halfword of a register into memory.                     |
| SW        | Store Word               | S-Type     | Store a word from a register into memory.                             |
| ADDI      | Add Immediate            | I-Type     | Add an immediate value to a register.                                 |
| SLTI      | Set Less Than Immediate  | I-Type     | Set a register to 1 if less than immediate; otherwise, set to 0.     |
| SLTIU     | Set Less Than Immediate (Unsigned) | I-Type | Set a register to 1 if less than immediate (unsigned); otherwise, 0.|
| XORI      | XOR Immediate            | I-Type     | Perform bitwise XOR with an immediate value.                          |
| ORI       | OR Immediate             | I-Type     | Perform bitwise OR with an immediate value.                           |
| ANDI      | AND Immediate            | I-Type     | Perform bitwise AND with an immediate value.                          |
| SLLI      | Shift Left Logical Immediate | I-Type | Shift a register left by an immediate number of bits.                |
| SRLI      | Shift Right Logical Immediate | I-Type | Shift a register right by an immediate number of bits (logical).     |
| SRAI      | Shift Right Arithmetic Immediate | I-Type | Shift a register right by an immediate number of bits (arithmetic).  |
| ADD       | Add                      | R-Type     | Add two registers and store the result in a destination register.    |
| SUB       | Subtract                 | R-Type     | Subtract one register from another and store the result.             |
| SLL       | Shift Left Logical       | R-Type     | Shift a register left by a variable number of bits.                  |
| SLT       | Set Less Than            | R-Type     | Set a register to 1 if one register is less than another.            |
| SLTU      | Set Less Than (Unsigned) | R-Type     | Set a register to 1 if one register is less than another (unsigned). |
| XOR       | XOR                      | R-Type     | Perform bitwise XOR with two registers.                              |
| SRL       | Shift Right Logical      | R-Type     | Shift a register right by a variable number of bits (logical).       |
| SRA       | Shift Right Arithmetic   | R-Type     | Shift a register right by a variable number of bits (arithmetic).    |
| OR        | OR                       | R-Type     | Perform bitwise OR with two registers.                               |
| AND       | AND                      | R-Type     | Perform bitwise AND with two registers.                              |
| FENCE     | Fence                    | I-Type     | Synchronize the execution of memory operations.                      |
| ECALL     | Environment Call         | I-Type     | Invoke


### General-Purpose Registers and Operand Types

RV64I employs 31 general-purpose registers, x1–x31, to hold integer values. x0 is fixed as the constant 0. Unlike some architectures, there is no hardwired link register for subroutine returns; instead, x1 is commonly used to store return addresses. For RV32, registers are 32 bits wide, while for RV64, they are 64 bits wide. The term XLEN is used to denote the current width of an x register in bits (either 32 or 64).

| Register   | Description                                        |
|------------|----------------------------------------------------|
| `x0`       | Hardwired to constant 0.                          |
| `x1`       | Often used for return addresses in subroutine calls. |
| `x2` to `x31` | General-purpose registers holding integer values. |


### Instruction Formats and Types

In the RISC-V instruction set architecture, instructions are categorized into different formats based on their opcode and operand types. Each format is denoted by a single-letter abbreviation. Here's an explanation of each type:

- R-Type (Register Type): These instructions perform operations on two source registers and store the result in a destination register. They cover arithmetic, logical, and bitwise operations. The format is: opcode rd, rs1, rs2.

- I-Type (Immediate Type): These instructions involve an immediate (constant) value as an operand. They work with a source register to perform operations like arithmetic, logical, and memory operations. The format is: opcode rd, rs1, imm.

- S-Type (Store Type): S-type instructions are used for storing data into memory. They combine a source register, a destination address (base register), and an immediate offset to determine where the data should be stored. The format is: opcode rs2, imm(rs1).

- B-Type (Branch Type): B-type instructions are used for conditional branching. They compare values from two source registers and use an immediate offset to determine the branching target. These instructions support operations like equality, inequality, and comparison. The format is: opcode rs1, rs2, imm.

- U-Type (Upper Immediate Type): U-type instructions are for loading immediate values into registers, including unconditional jump instructions. They operate on a single source register and use an immediate value to specify the upper bits of the result. The format is: opcode rd, imm.

- J-Type (Jump Type): J-type instructions are used for unconditional jumps. They involve using an immediate offset to determine the target address of the jump. These instructions are typically used for implementing function calls and other control flow changes. The format is: opcode rd, imm.

![Summary+of+RISC-V+Instruction+Formats](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/7e0129e9-2102-4d91-9935-0dc1e39fc0e6)

## Application Binary Interface (ABI) in RISC-V:

### Introduction
The Application Binary Interface (ABI), also referred to as the System Call Interface, allows application programmers to directly access the registers of the RISC-V architecture through system calls. This mechanism enables programmers to interact with hardware resources via registers, facilitated by the ABI. The RISC-V ABI defines standardized functions for registers, promoting software interoperability.

The ABI consists of two primary components: the set of user instructions and the system call interface through the operating system layer.

The RISC-V architecture comprises 32 registers, labeled from x(0) to x(31), with their width determined by XLEN (32 bits for RV32 and 64 bits for RV64). Application programmers can access each of these registers using their ABI names.

![ABI](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/f837dc3a-9290-4fa2-91f0-81f9ca69f0f8)

#### Key Points about ABI in RISC-V:

- The RISC-V architecture employs byte-addressable memory.
- RISC-V follows the little-endian memory addressing system.
- Loading data into registers can be done directly or via memory access.
- Direct loading into registers is limited by the number of available registers, necessitating the use of memory for larger data sets.
- Understanding the ABI in RISC-V is crucial for developers working with the architecture, as it provides a standardized approach for interacting with registers and hardware resources.

#### Register File

RISC-V Architecture includes a register file with a total of 32 integer registers and 32 floating-point registers. These registers have specific designated purposes based on their ABI names. The naming convention is crucial for managing these registers efficiently within the architecture. Here are some key points regarding register usage:

Registers starting with 't' (e.g., t0, t1, t2, ..., t6) are temporary registers and can be employed for various purposes as needed.

Registers beginning with 'a' (e.g., a0, a1, ..., a7) serve as argument registers for passing arguments to functions.

Registers that have names starting with 's' (excluding 'sp') are saved registers. They are preserved across function calls and their values are maintained.

<img width="267" alt="regfile" src="https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/a4319fc5-296c-40ca-b14f-95c289aa4770">

#### Types of Instructions
RISC-V architecture encompasses diverse types of instructions, each designed to operate on different types of data. Among them, Base Integer Instructions are prominent. These instructions facilitate operations on both signed and unsigned integer numbers. Some noteworthy points regarding these instructions are as follows:

There exist around 47 distinct types of Base Integer Instructions in the RISC-V architecture.

Some common categories of Base Integer Instructions are R-type, I-type, and S-type instructions, each having specific functionalities.

R-type Instructions: These instructions exclusively work with registers. For instance: add x8, x24, x8 performs addition using registers.

I-type Instructions: These instructions operate on both registers and immediate values. For example: ld x8, 16(x32) loads data from memory using an immediate offset.

S-type Instructions: These instructions operate on source registers and immediate values and are often used for storing data. For example: sd x8, 8(x23) stores data in memory using an immediate offset.

![MUKIE](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/a82a2136-5452-45a1-8725-c4e138d06de1)

#### Register Accessibility and Representation
In the RISC-V architecture, the registers accessed by R-type, I-type, or S-type Instructions are limited to 5 bits. Consequently, the total number of representable registers is 2^5 = 32. As a result, there are 32 registers available (from x0 to x31) in the RISC-V architecture. Proper management of these registers through different instruction formats ensures efficient and effective execution of programs.

## Labwork

### Labwork Using ABI Function Calls

Consider the following example involving C and assembly code:

```bash
#include <stdio.h>

extern int load(int x, int y);

int main()
{
    int result = 0;
    int count = 9;
    result = load(0x0, count + 1);
    printf("Sum of numbers from 1 to %d is %d\n", count, result);
}
```

#### Assembly Code (ASM)

```bash
.section .text
.global load
.type load, @function

load:
	add 	a4, a0, zero //Initialize sum register a4 with 0x0
	add 	a2, a0, a1   // store count of 10 in register a2. Register a1 is loaded with 0xa (decimal 10) from main program
	add	a3, a0, zero // initialize intermediate sum register a3 by 0
loop:	add 	a4, a3, a4   // Incremental addition
	addi 	a3, a3, 1    // Increment intermediate register by 1	
	blt 	a3, a2, loop // If a3 is less than a2, branch to label named <loop>
	add	a0, a4, zero // Store final result to register a0 so that it can be read by main program
	ret
```

In this example, the C code interacts with the assembly code via the load function. The flowchart of the function performed by the assembly code is illustrated visually.

The ABI enables the C code to pass values to the assembly code through the load function. The assembly code executes the function, returns the result to the C code, and the C code displays the value.

#### Steps to Perform the Lab Task:

Compile the C and assembly code using riscv64-unknown-elf-gcc with optimization, ABI, and architecture flags:

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.S
```
Disassemble the compiled object file using riscv64-unknown-elf-objdump and view the output using less:

```bash
riscv64-unknown-elf-objdump -d 1to9_custom.o | less
```
Run the compiled code using the Spike RISC-V simulator:
```bash
spike pk 1to9_custom.o
```

#### Outputs of the Lab

![Screenshot from 2023-08-21 13-20-24](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/6b283f1d-2d65-4c56-9d13-c1e4a3ac4c7a)

Flow Chart and ABI Illustration
The flow chart below represents the sequence of operations performed by the assembly code within the load function:

### ASM Flow Chart

This flow chart is crucial in understanding how the assembly code iterates and accumulates the sum of numbers, demonstrating the algorithm's execution visually.

#### ABI Interaction

The provided C code serves as the conduit through which the Application Binary Interface (ABI) principles are demonstrated. The interaction unfolds as follows:

- The C code initializes the count and result variables to appropriate values.
- It invokes the load function from the assembly code, passing the arguments 0x0 and count + 1.
- The assembly code executes the load function, performing the summation operation using the provided algorithm.
- Upon completion, the assembly code returns the computed result via the ABI mechanism to the calling C code.
- Back in the C code, the returned value is captured and then displayed using the printf function.
- This interaction elegantly showcases how the ABI enables seamless communication between different parts of the codebase, allowing the C code to utilize the assembly routine for computation and receive the results effectively.

The combined effect of the flow chart and the ABI interaction demonstration provides a comprehensive understanding of how the given C and assembly code work together to achieve their desired functionality.

![Screenshot (54)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/17aec548-945a-456b-86e4-bd7244845ca7)

## RISC-V Basic Verification Flow using Iverilog Demo

This section outlines the verification process for a RISC-V CPU using the Iverilog simulator. The verification involves converting C code to a HEX file, providing it to the RISC-V CPU, and then verifying the output. The following block diagram illustrates the verification flow:

![Screenshot (56)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/8a8274ba-fc42-4756-a2b2-c5706f2643fe)

### Verification Flow Description

- Conversion to HEX File: The first step involves converting the C code into a HEX file. This file will contain the machine code representation of the C program that the RISC-V CPU can understand.
- Providing HEX File to RISC-V CPU: The HEX file is fed to the RISC-V CPU. The CPU processes the instructions and performs computations based on the provided program.
- Output and Verification: After executing the program, the RISC-V CPU produces an output. This output is then verified to ensure it matches the expected outcome, validating the correctness of the CPU's execution.

### Demonstration

To observe this verification flow in action, follow these steps:

Navigate to the lab directory using the following command:

```bash
cd ~/riscv_workshop_collaterals/labs/
```
Make the script executable with the following command:

```bash
chmod 777 rv32im.sh
```
Execute the script rv32im.sh which contains the necessary commands to convert C code to a HEX file and run the verification process:

```bash
./rv32im.sh
```

#### Outputs 
![Screenshot from 2023-08-21 13-45-31](https://github.com/akhiiasati/Akhil_IIITB/assets/43675821/1d7d1736-7c9e-436d-8c37-a91f2f8b1eaa)

# Day 3: Digital Logic with TL-Verilog and Makerchip

- [Logic Gates](#logic-gates)
- [Transaction-Level Verilog (TL-Verilog): An Overview](#transaction-level-verilog-(tl-verilog)-an-overview)
  - [Overview](#overview)
  - [TL-Verilog Advantages](#tk-verilog-advantages)
  - [TL-Verilog vs. SystemVerilog: A Comparison](#tl-verilog-vs-systemverilog-a-comparison)
  - [Timing Abstract in TL-Verilog](#timing-abstract-in-tl-verilog)
- [Makerchip IDE](#makerchip-ide)
  - [Key Features](#key-features)
  - [Benefits](#benefits)
  - [Examples: Pythagorean](#examples-pythagorean)
- [Comabinational Circuits](#comabinational-circuits)
- [Labs: Combinational Logic on MackerChip IDE](#labs-combinational-logic-on-mackerchip-ide)
  - [Inverter](#inverter)
  - [AND Gate](#and-gate)
  - [OR Gate](#or-gate)
  - [XOR Gate](#xor-gate)
  - [Vector Addition](#vector-addition)
  - [2:1 Multiplexer](#2-1-multiplexer)
  - [Combinational Calculator using TL-Verilog](#combinational-calculator-using-tl-verilog)
- [Sequential Circuits](#sequential-circuits)
- [Labs: Sequential Logic on MackerChip IDE](#labs-sequential-logic-on-mackerchip-ide)
## Logic Gates

Logic gates are fundamental components of digital electronic circuits, serving as the building blocks for logical operations. These gates process input signals and generate output signals based on predefined logic rules. By manipulating binary signals, typically represented as "0" and "1," logic gates enable complex digital systems such as processors, memory units, and controllers. They function by performing logical operations and are designed to work with discrete voltage levels representing binary values.

Here are some common types of logic gates:

![Screenshot (62)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/b199aeef-e660-49da-981d-a8d0aa6aa048)

These gates can be combined to create intricate digital circuits. Notably, NAND and NOR gates are referred to as universal gates because they can be used to construct all other logic gates. The Verilog representation of logic gates is shown below:

![Screenshot (68)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/f9fd4caf-434e-44e3-a1c7-eee94f816eb4)

Multiplexer Using Ternary Operator
A multiplexer is a crucial component for selecting one of multiple input signals and forwarding it as the output. In Verilog, a simple 2:1 multiplexer can be realized using the ternary operator as shown below:

```bash
assign f = s ? x1 : x0;
```
Here, the output f follows x1 when s is 1; otherwise, it follows x0. The corresponding hardware and logic gate representation is illustrated:

![Screenshot (70)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/ec47ff05-e330-4add-8da1-9f7b544677f4)

For more complex scenarios, higher bit multiplexers can be created using the conditional operator. Consider the Verilog code for a 4:1 multiplexer below:

```bash
assign f = sel[0] ? a : (sel[1] ? b : (sel[2] ? c : d));
```
In this code, input a holds the highest priority, and input d holds the lowest. This code doesn't create a single 4:1 multiplexer; instead, it forms a series of interconnected 2:1 multiplexers. Here, the sel signal is a one-hot vector, with only one bit set to high at a time. The hardware realization of this concept is depicted below:

![Screenshot (74)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/1307f539-2b65-43b8-ae26-cb357e6a8762)

## Transaction-Level Verilog (TL-Verilog): An Overview

### Overview:

Transaction-Level Verilog (TL-Verilog) is an emerging extension to SystemVerilog, offering a new design methodology known as transaction-level design. This approach simplifies the design process by introducing concepts that focus on transactions and abstracting away lower-level hardware details. In this project, TL-Verilog has been chosen as the Hardware Description Language (HDL) of choice, enabling the complete design of projects using this innovative approach.

### TL-Verilog Advantages:

- Simpler Syntax: TL-Verilog introduces a more intuitive and concise syntax, streamlining the design process.
- Shorter Codes: TL-Verilog enables the creation of shorter and more readable code, enhancing productivity.
- Easy Pipelining: The language inherently supports easy pipelining of designs, simplifying complex data processing.
- Timing Abstract: TL-Verilog allows for timing abstraction, enabling specification of pipelines where tools generate sequential elements from the pipelined specification.

### TL-Verilog vs. SystemVerilog: A Comparison

Consider the following comparison between a design written in TL-Verilog and SystemVerilog:

#### TL-Verilog Example:

```tl
// Example TL-Verilog code
pipeline pipe {
    input a, b, c;
    output x, y, z;
    
    stage A { x = a + b; }
    stage B { y = x + c; }
    stage C { z = y * x; }
}
```
#### SystemVerilog Example:

```systemverilog
// Equivalent SystemVerilog code
module pipeline (
    input a, b, c,
    output x, y, z
);
    reg [31:0] x_reg, y_reg, z_reg;
    
    always @(posedge clk) begin
        x_reg <= a + b;
        y_reg <= x_reg + c;
        z_reg <= y_reg * x_reg;
    end
endmodule
```
### Timing Abstract in TL-Verilog

One notable feature of TL-Verilog is its support for timing abstraction. This feature is particularly useful in designing pipelines where sequential elements are generated by tools based on the pipelined specification. Timing abstraction allows for easy retiming without the risk of introducing functional bugs. For further information on timing abstract in TL-Verilog, refer to the IEEE paper "Timing-Abstract Circuit Design in Transaction-Level Verilog" by Steven Hoover.

## Makerchip IDE
Makerchip IDE is a powerful integrated development environment tailored for digital design and hardware description language (HDL) programming. It offers a comprehensive platform that caters to engineers, students, and enthusiasts, enabling them to design, simulate, and validate digital circuits and systems effectively.

![MakerchipSplash](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/858f8922-b7df-4215-ab9d-3e6014d60647)

### Key Features
- User-Friendly Interface: Makerchip IDE boasts an intuitive and user-friendly interface that simplifies the design process.
- Multi-HDL Support: The IDE supports various hardware description languages (HDLs) including TL Verilog, SystemVerilog, Verilog, and VHDL,enhancing flexibility.
- Component Library: Users can construct intricate digital systems using a combination of pre-built and custom logic elements such as logic gates, flip-flops, multiplexers, and more.
- Virtual Canvas: Makerchip provides a virtual canvas where users can visually build their designs by interconnecting these logic components, enhancing the design experience.
- Real-Time Simulation: One of its standout features is real-time simulation, allowing users to observe their designs' behavior before physical implementation. This aids in identifying and rectifying errors early.

### Benefits
- Early Error Detection: Virtual prototyping through Makerchip IDE's simulation helps catch errors in the design phase, preventing potential issues in the final hardware.

- Learning Platform: Both beginners and experienced designers can explore, learn, and experiment with digital logic design, promoting innovation in the field of digital electronics.

- Efficient Iteration: The IDE's iterative design process allows for quick refinements and modifications, accelerating the development cycle.

### Examples: Pythagorean

![Screenshot (76)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/40325c1d-344a-4c77-8322-fa03f3ee8795)

## Labs: Combinational Logic on MackerChip IDE

### Inverter

The TL-Verilog code for an inverter is shown below:

```tl
$out = $in;
```

![Screenshot (77)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/3001e778-6097-4f65-85bf-d6232faba243)
![Screenshot (78)](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/8a565e8a-49cc-47e9-a299-84c963249d4a)

### AND Gate

The TL-Verilog code for an AND gate is shown below:

```tl
$out = $in1 && $in2;
```
![Screenshot 2023-08-21 173654](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/d651de4c-10fe-4f9b-80e8-55881fa0b92e)
![Screenshot 2023-08-21 173721](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/0037eb2f-2d09-44f1-8e80-e610bfb35837)

### OR Gate

The TL-Verilog code for an OR gate is shown below:

```tl
$out = $in1 || $in2;
```	

![Screenshot 2023-08-21 173852](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/dadcd127-a468-41f0-bc0d-7655aae628ad)
![Screenshot 2023-08-21 173909](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/5255d6bd-ae68-4619-9bf8-2d6ac0631dfb)

### XOR Gate

The TL-Verilog code for an XOR gate is shown below:

```tl
$out = $in1 ^ $in2;
```

![Screenshot 2023-08-21 180836](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/20e8342c-cdb9-45a6-93e8-b77991c36d4b)
![Screenshot 2023-08-21 180903](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/ded4bceb-3e9c-459a-b332-8ed0a883edf5)

### Vector Addition

The TL-Verilog code for vector addition is shown below:

```tl
$out[5:0] = $in1[4:0] + $in2[4:0];
```

![Screenshot 2023-08-21 181015](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/4b221228-7ac4-4b91-8c3e-fdb68d05ba9c)
![Screenshot 2023-08-21 181035](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/dd35e70a-6689-4f92-a2ab-bb24eb67becf)

### 2:1 Multiplexer

The TL-Verilog code for a 2:1 multiplexer is shown below:

```tl
$out = $sel ? $in1 : $in0;
```
![Screenshot 2023-08-21 181228](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/cade91f7-f7b9-43f5-9507-8a2682a31acb)
![Screenshot 2023-08-21 181240](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/92cb2fa3-8e06-4c93-8b10-ace6fd5c5a01)


### The TL-Verilog code for a 2:1 vector multiplexer is shown below:

```tl
$out[7:0] = $sel ? $in1[7:0] : $in0[7:0];
```

![Screenshot 2023-08-21 181354](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/a9165b98-5695-4ea8-9590-db43e52c7c2c)
![Screenshot 2023-08-21 181405](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/328067c7-d12a-4b95-9fa4-9c95e3a71ab2)

### Combinational Calculator using TL-Verilog
This documentation presents a Combinational Calculator implemented using Transaction-Level Verilog (TL-Verilog). The calculator performs various arithmetic operations based on the provided opcode.

#### TL-Verilog Code

The TL-Verilog code for the Combinational Calculator is shown below:

```tl
$reset = *reset;
$op[1:0] = $random[1:0];

$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];
$sum[31:0] = $val1 + $val2;
$diff[31:0] = $val1 - $val2;
$prod[31:0] = $val1 * $val2;
$div[31:0] = $val1 / $val2;

$out[31:0] = $op[1] ? ($op[0] ? $div : $prod) : ($op[0] ? $diff : $sum);
```
#### Function Table

The function table for the Combinational Calculator is provided below:

| Opcode | Function         |
|--------|------------------|
| 2'b00  | Addition         |
| 2'b01  | Subtraction      |
| 2'b10  | Multiplication   |
| 2'b11  | Division         |


#### How it Works

- The calculator receives a reset signal (*reset) to initialize the calculations.
- A 2-bit opcode ($op[1:0]) is randomly generated, determining the arithmetic operation to be performed.
- Two 4-bit random values ($rand1[3:0] and $rand2[3:0]) are generated as operands.
- The calculator performs addition, subtraction, multiplication, and division operations on the operands.
- Based on the opcode, the output ($out[31:0]) is determined by selecting the appropriate result.

![Screenshot 2023-08-21 183813](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/965101d9-cc6c-4103-a88d-faa31ade6ec9)
![Screenshot 2023-08-21 183827](https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog/assets/43675821/6a6fedc6-d773-49ef-9964-0ce874676f24)
