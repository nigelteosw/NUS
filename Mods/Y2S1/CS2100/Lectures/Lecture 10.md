# Instruction Set Architecture (ISA)

## RISC vs CISC
- Two major design philosophies for ISA
- Complex Instruction Set Computer (CISC)
	- e.g. x86-32 (IA32)
	- Single instruction performs complex operation
	- Smaller program size as memory was premium
	- Complex implementation, no room for hardware optimization
- Reduced Instruction Set Computer (RISC)
	- e.g. MIPS, ARM
	- Keep the instruction set small and simple, makes it easier to build/optimize hardware
	- Burden on software to combine simpler operations to implement high-level language statements

## Data Storage
- General Purpose Register Architecture 
- Operations may be implicit or explicit

- Stack Architecture:
	- Operands are implicitly on top of the stack

- Accumulator Architecture:
	- One operand is implicitly in the accumulator (special register)

- General-purpose register architecture
	- Only explicit operands
	- Register-memory architecture
	- Register-register (load-store) architecture
		- e.g. MIPS

- Memory-memory architecture
	- All operands in memory

![[Pasted image 20220905104616.png]]

For modern processors:
- General-Purpose Register is the most common choice for storage design
- RISC computers typically use Register-Register design

## Memory Addressing Mode
- Each slot in memory can store 8 bits

### Endianness
- The relative ordering of the bytes in a multiple-byte word stored in memory
- Big-endian
	- Most significant byte is stored in lowest address
- Little-endian
	- Least significant byte is stored in the lowest address

### Addressing Mode
- Register
	- Operand in register
- Immediate
	- Operand in the instruction directly
- Displacement
	- Operand in memory stored in base + offset

## Operations in Instruction Set
- Data Movement
- Arithmetic
- Shift Logical
- Control flow
- Subroutine Linkage
- Interrupt
- Synchronization
- String
- Graphics

## Instruction Formats
- Instruction Length
- Instruction Fields
	- Type and Size of Operands

- Variable-length instructions
	- For intel: can vary from 1 to 17 bytes long
- Fixed-length instructions
	- Instructions are 4 bytes long
	- allow for easy fetch and decode
	- simplified through pipelining and parallelism

### Instruction Fields
- Instruction consists of:
	- opcode: unique code to specify the desired operation
	- operands: zero or more additional information needed for the operation
- The operation designates the type and size of the operands
- Expectations for any new 32-bit architecture
	- Support for 8-, 16-, 32-bit integer and 32-bit and 64-bit floating point operations

## Encoding the Instruction Set
Three encoding choices: variable, fixed, hybrid

- Fixed length instruction presents an instruction challenge"
	- Expanding Opcode scheme

![[Pasted image 20220930113617.png]]
