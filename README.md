# RISC-V

# Course of content
- [Day 1: Introduction to RISC-V ISA and GNU compiler toolchain](#day-1-introduction-to-risc-v-isa-and-gnu-compiler-toolchain)


## Day 1: Introduction to RISC-V ISA and GNU compiler toolchain

### Instruction Set Architecture (ISA)
An Instruction Set Architecture (ISA) is a set of rules and specifications that define the instructions that a computer's processor can execute. It serves as a crucial interface between the hardware (the physical components of the computer) and the software (the programs and applications that run on the computer). The ISA essentially provides a standardized way for software to communicate with and utilize the underlying hardware resources.

Think of the ISA as the "language" that software uses to communicate with the processor. It defines the types of operations that the processor can perform, the formats of instructions that the processor understands, and the organization of registers (small, fast memory locations within the processor) that store data during computations.

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

