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
This command is used to compile a C source file named sum1ton.c into an object file named sum1ton_O1.o using the RISC-V GCC compiler (riscv64-unknown-elf-gcc). Here's what each flag does:

-O1: Specifies the optimization level. In this case, optimization level 1 is used.
-mabi=lp64: Sets the ABI (Application Binary Interface) to use 64-bit integers and pointers.
-march=rv64i: Specifies the target architecture, in this case, the base integer instructions of the RV64I architecture.

Disassembly:

To view the disassembled code, use the riscv64-unknown-elf-objdump command:
```bash
riscv64-unknown-elf-objdump -d sum1ton_O1.o | less
```
This command disassembles the compiled object file sum1ton_O1.o using the riscv64-unknown-elf-objdump tool. The -d flag tells objdump to display the disassembled code. The | less part of the command pipes the output of objdump into the less command, which allows you to view the disassembled code interactively.

Execution on Spike Simulator:

```bash
spike pk sum1ton_O1.o
```

This command uses the spike simulator to execute the compiled program sum1ton_O1.o. The pk argument indicates that you want to run a "proxy kernel" program. In this case, the program sum1ton_O1.o is executed on the simulated RISC-V architecture provided by the Spike simulator.


This series of steps transforms the C code into RISC-V assembly code, compiles it, and then executes it using the Spike simulator, providing insights into how the C program operates in terms of RISC-V instructions. The -O1 optimization level in the compilation can affect the generated assembly code, optimizing it for performance while maintaining the functional behavior of the original C code.
