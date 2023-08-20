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

![Screenshot (30)](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/5ea8ed17-c77b-4b0d-b5d2-58ef6a980c1b)

In RISC-V and computer architecture in general, several terms relate to data representation and storage. Let's explore them:

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
![Screenshot 2023-08-20 230354](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/18a4af69-0424-4557-84be-f18ddc7cea61)
