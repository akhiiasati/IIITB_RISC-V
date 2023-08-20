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
- [Features of RISC-V](#features-of-risc-v)
- [RISC-V Foundation and RISC-V International](#risc-v-foundation-and-risc-v-international)
### RISC-V: A Transformative ISA for Innovation

RISC-V, known as "Reduced Instruction Set Computing - Five," is a transformative open-source instruction set architecture (ISA) born from a commitment to advancing computer architecture research and education. With its roots tracing back to the pioneering work of Prof. David Patterson and Prof. John Hennessy, RISC-V redefines chip design, embodying decades of research. It follows a RISC approach, strategically positioning instruction bit fields for simplified CPU design and employing IEEE 754 floating-point precision. Unlike traditional ISAs, RISC-V operates under open-source licenses, offering an edge in flexibility, scalability, and innovation. Led by Prof. Krste Asanović, Yunsup Lee, and Andrew Waterman, its accessible framework empowers ease of processor creation and customization, signifying a new era in instruction set architectures.

![riscv_social](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/d180be06-b618-466d-82ef-7fe5bf0fd92a)


### Features of RISC-V:
Free and Open-Source: RISC-V operates on an open-source model, eliminating the need for IP payment. Unlike other commercial ISAs, RISC-V encourages accessibility and collaboration.

Simplicity: RISC-V's footprint is notably smaller compared to conventional ISAs. Its streamlined design promotes efficiency and ease of implementation.

Modularity: RISC-V boasts a compact standard base ISA, accompanied by various standard extensions. This modular approach enables tailoring to specific application needs.

Stability: The base and initial standard extensions of RISC-V are already finalized and stable. This stability mitigates concerns about disruptive major updates.

Extensibility: RISC-V's architecture accommodates the addition of specific functionalities via extensions. The ongoing development of extensions, such as the Vector extension, enhances RISC-V's capabilities.

In essence, RISC-V’s open nature, simplicity, modularity, stability, and extensibility redefine the landscape of instruction set architectures, setting it apart from established ARM and x86 alternatives.

### RISC-V Foundation and RISC-V International

Established in 2015, the RISC-V Foundation responded to the need for a stable instruction set architecture (ISA) suitable for prolonged commercial use. With a commitment to stability, it took charge of intellectual property related to RISC-V's definition. Among the founding members were innovative entities such as Andes, Google, IBM, SiFive, and even IIT Madras, collectively shaping RISC-V's journey. In 2019, the foundation's transformation into RISC-V International marked its relocation to Switzerland, underlining its commitment to openness and stability. This shift, while maintaining document accessibility, granted member organizations the power to endorse changes and use the trademarked compatibility logo, fostering a collaborative evolution.For more information visit the site : www.riscv.org

![risc-v-members](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/251e4e94-c95b-4001-8f2f-02d1be575fc6)

![Screenshot 2023-08-20 182714](https://github.com/akhiiasati/IIITB_RISC-V/assets/43675821/5a6ebdcb-952a-4db2-aa9f-175908a42fd6)

### Introduction to RISC-V basic keywords

