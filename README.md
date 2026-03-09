LIPSI Processor
Overview

LIPSI is an ultra-small 8-bit processor designed for minimal resource consumption, particularly suited for auxiliary functions inside FPGA systems. It uses a single on-chip block RAM shared between instructions and data, enabling a compact and efficient implementation.

The processor follows an accumulator-based architecture with a simple but complete instruction set, making it suitable for:

1)Embedded utility tasks

2)FPGA-based systems

3)Educational purposes

Abstract

LIPSI is an ultra-small 8-bit processor designed for minimal resource consumption, particularly suited for auxiliary functions within FPGA systems. It leverages a single on-chip block RAM shared between instructions and data, enabling a compact and efficient implementation.

Built as an accumulator-based architecture, LIPSI supports a simple but complete instruction set, making it suitable for embedded utility tasks and educational purposes.

How LIPSI Works

LIPSI is an 8-bit accumulator-based processor designed primarily for auxiliary tasks in FPGA systems.

Key Characteristics

Uses single block RAM for both instructions and data

Sequential execution

Non-pipelined architecture

Core Components

The architecture consists of:

Program Counter (PC)

Arithmetic Logic Unit (ALU)

Accumulator Register (A)

Memory (shared for program and data)

Memory Structure

Memory is divided into program area and data area

The first 16 bytes of the data area are used as registers

Supported Operations

The processor supports:

1)Arithmetic operations

2)Logic operations

3)Memory access

4)Branching

5)Input/Output

All operations are centered around the accumulator.

Instruction Set

An instruction set is the collection of operations that a processor can understand and execute.

For LIPSI, the instruction set includes:

1)Arithmetic operations (ADD, SUB)

2)Logic operations (AND, OR)

3)Load and store instructions

4)Branch instructions

5)Input/Output instructions

These instructions allow the processor to perform computations and control program flow.

Datapath of LIPSI Processor

The datapath connects the core components:

1)Program Counter

2)ALU

3)Accumulator

4)Memory

5)Input/Output

It enables data flow between memory and the accumulator while instructions are executed sequentially.

Difference From Traditional LIPSI

Our implementation extends the traditional LIPSI processor by adding additional ALU shift operations.

1)Additional ALU Shift Operations

2)Encoding	Instruction	Operation

1110 --00	SHL	Left Shift

1110 --01	SHR	Right Shift

1110 --10	ROL	Left Rotate

1110 --11	ROR	Right Rotate

These instructions enable efficient bit manipulation operations.

Implementation

The processor was implemented as a Finite State Machine (FSM).

Total States

The processor uses 16 states.

Fundamental Execution Phases

Although the design uses multiple states, the processor operation can be broadly divided into:

1)Fetch

2)Decode

3)Execute

4)Writeback

Because the processor is non-pipelined, some instructions require multiple clock cycles, which results in additional intermediate states.

Instruction Execution States

Different instructions require different state transitions.

ALU Register
FETCH → ALUOP → FETCH

Store
FETCH → STORE → FETCH

Branch and Link
FETCH → BRLNK → FETCH

Load Indirect
FETCH → LOADIND1 → LOADIND2 → FETCH

Store Indirect
FETCH → STOREIND1 → STOREIND2 → FETCH

ALU Immediate
FETCH → DATA2 → DATA → DATA3 → FETCH

Branch
FETCH → BRANCH2 → BRANCH → FETCH

ALU Shift
FETCH → ALUSHIFT → FETCH

Input/Output
FETCH → IO → FETCH

Exit
FETCH → EXIT

Special Implementation Details
Load Indirect

Requires an additional state because:

First cycle reads address from memory.

Second cycle accesses the actual data from that address.

Store Indirect

Requires two steps:

Read address stored in memory.

Store accumulator value at that address.

ALU Immediate

This is a two-byte instruction:

First byte → instruction

Second byte → data

Total execution time: 4 clock cycles

Branch Instruction

Also a two-byte instruction:

First byte → instruction

Second byte → branch address

Total execution time: 3 clock cycles

Instruction Usage and Importance
Instruction	Use	Importance
Store	Store accumulator to memory	Saves computed values
ALU	Arithmetic/logic operations	Enables computation
Branch and Link	Function call support	Saves PC and branches
Load Indirect	Pointer-based access	Useful for linked structures
Store Indirect	Indirect memory write	Useful in device drivers
ALU Immediate	Immediate arithmetic	Used in loop counters
Branch	Control flow	Used in loops and conditions
ALU Shift	Bit manipulation	Multiply/divide by powers of 2
Input/Output	Device communication	External data transfer
Exit	Program termination	Ends execution
LIPSI Schematic

The processor schematic illustrates the connection between:

Program Counter

ALU

Accumulator

Memory

I/O interfaces

Power Analysis

Power analysis was performed to evaluate the resource efficiency and energy consumption of the LIPSI processor when implemented on FPGA.

Timing Analysis

Timing analysis ensures that the processor operates correctly within clock constraints and validates the setup and hold timing requirements.

Limitations
Simple Architecture

The simplicity of the LIPSI processor limits its ability to handle complex tasks.

Limited Instruction Set

Complex operations often require multiple instructions, reducing efficiency.

Non-Pipelined Execution

Instructions are executed sequentially, leading to lower performance compared to pipelined processors.

Future Work
Pipelining

Introducing pipelining can improve throughput by allowing multiple instructions to execute simultaneously.

Additional Addressing Modes

More addressing modes would provide flexibility in accessing memory.

Interrupt Support

Adding interrupts would make the processor suitable for real-time applications.

Expanded Data Width

Expanding the architecture to 16-bit or 32-bit would support more complex computations.

Improved I/O

Enhancing I/O capabilities would allow connection to more peripherals.

FPGA Optimization

Further optimization can improve resource utilization and performance on FPGA platforms.
