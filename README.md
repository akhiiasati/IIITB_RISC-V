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
- [RISC-V: A Transformative ISA for Innovation](#risc-v-a-transformative-isa-for-innovation)
### RISC-V: A Transformative ISA for Innovation

RISC-V, short for "Reduced Instruction Set Computing - Five," introduces a groundbreaking instruction set architecture (ISA) born from a commitment to advancing computer architecture research and education. Embracing an open-source ethos and adaptability, RISC-V empowers diverse implementations and customizations.

The origin of the RISC acronym dates back to 1980, attributed to Prof. David Patterson of UC Berkeley and Prof. John Hennessy of Stanford University. Their pioneering work culminated in acclaimed books and an ACM Turing Award in 2017. The fifth evolution, RISC-V, emerged around 2010.

As a RISC architecture, RISC-V follows a load-store approach and employs IEEE 754 floating-point for precision. It boasts noteworthy features, including strategically positioned instruction bit fields for simplified CPU design, architectural neutrality, and an optimized sign-extension mechanism.

In essence, RISC-V stands as an emblem of innovation, backed by decades of research, embodying open principles, and poised to reshape the landscape of instruction set architectures.


- Base and Optional Extensions:

At its core, the RISC-V ISA comprises a foundational base integer ISA, known as "I." This base ISA serves as the foundation for all RISC-V implementations and forms a practical target for compilers, assemblers, linkers, and operating systems. Unlike traditional architectures, RISC-V eliminates branch delay slots and introduces support for optional variable-length instruction encodings.

The base integer ISA, designated as "I," consists of instructions essential for integer computations, integer loads, integer stores, control-flow instructions, and additional supervisor-level operations. This minimalistic approach ensures practicality and serves as a building block for customization.

RISC-V also features optional extensions that can be added to the base ISA according to specific requirements. These extensions enhance the architecture's capabilities and tailor it to various application domains

- Standard Extensions:

    "M" Extension (Integer Multiplication and Division): The standard integer multiplication and division extension, named "M," introduces instructions that enable the multiplication and division of values stored in integer registers.

    "A" Extension (Atomic Instructions): The standard atomic instruction extension, denoted as "A," adds instructions for atomic memory operations. These instructions facilitate inter-processor synchronization by enabling memory reads, modifications, and writes in an atomic manner.

    "F" Extension (Single-Precision Floating-Point): The "F" extension enhances RISC-V with single-precision floating-point capabilities. It introduces floating-point registers, computational instructions for single-precision operations, and instructions for single-precision loads and stores.

    "D" Extension (Double-Precision Floating-Point): Extending the floating-point capabilities further, the "D" extension augments the architecture with double-precision floating-point operations. It introduces double-precision computational instructions, along with loads and stores for double-precision values.

- General-Purpose Scalar Instruction Set:

The combination of the base integer ISA ("I") and its four standard extensions ("IMAFD") creates a versatile general-purpose scalar instruction set, often referred to by the abbreviation "G." This comprehensive set of instructions forms the backbone of the RISC-V architecture, providing the foundation for a wide range of computing tasks.

In summary, RISC-V is not only a novel open-source ISA but also a flexible framework that allows for customization and specialization. With its base integer ISA and optional extensions, it caters to a diverse set of requirements across various industries and applications, making it a noteworthy advancement in the realm of computer architecture.

![Screenshot 2023-08-20 182714](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/5a6ebdcb-952a-4db2-aa9f-175908a42fd6)

### Introduction to RISC-V basic keywords

