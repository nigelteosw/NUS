# MIPS Part 3

## Instruction Formats
How are we converting assembly code into binary representation

### Basics
Each MIPS instruction has a fixed-length of **32 bits**

To keep complexity of the processor down.

### R-format
- Instructions that use 2 source registers and 1 destination register
- e.g. add, sub, and, or, nor, slt, srl, sll
- opcode always 0

### I-format
- Instructions which use 1 source register, 1 immediate value and 1 destination register
- e.g. addi, andi, ori, slti, lw, sw, beq, bne

### J-format
- j instruction that only uses one immediate value

## How to turn instruction into Hexadecimal
1) Find field representation in decimal
2) Find field representation in binary
3) Split into 4 bit groups for hexadecimal conversion

## R-format

| opcode | rs | rt | rd | shamt | funct |
|-----|----|-----|-------|------|--------|

### opcode
- Partially specifies the instruction
- Equal to 0 for all R-Format instructions

### funct
- Combined with opcode exactly specifies the instruction

### rs (Source Register)
- Specify register containing first operand

### rt (Target Register)
- Specify register containing second operand

### rd (Destination Register)
- Specify register which will receive result of computation

### shamt
- Amount a shift instruction will shift by  
- 5 bits (i.e. 0 to 31)  
- Set to 0 in all non-shift instructions


## I-format
If instruction has immediate, then it uses at most 2 registers
- removing shamt, rd and funct

|opcode|rs|rt|immediate|
|---|---|---|---| 

### opcode
- 6 bits
- Since there is no funct field, opcode uniquely specifies an instruction

### rs
- 5 bits
- specifies source register operand (if any)

### rt
- 5 bits
- specifies the register to receive results
- **note the difference from R-format instructions**

### immediate
- 16 bits
- treated as a signed integer
	- except for bitwise operations
- can be used to represent a constant up to 2<sup>16</sup> values
- large enough to handle:
	- The offset in a typical `lw` or `sw`
	- Most of the values used in the `addi`, `slti` instructions
- This is why we cannot put 32 bit constants into the instruction

## Instruction Address for Branching
As instructions are stored in memory, they too have addresses

### Program Counter (PC)
- A special register that keeps address of next instruction being executed in the processor

Loops are generally small:
- typically up to 50 instructions

Solution:
- Specify target address relative to the PC
- Target address is generated as:
	- PC + the 16-bit immediate field
	- the immediate field is a signed two's complement integer
- Can branch to +- 2<sup>15</sup> bytes from the PC which should be enough to cover most loops 

Can the branch target range be enlarged?
- Instructions are word-aligned 
- Interpret the immediate as number of words, i.e. automatically multiplied by 4
- We can now branch 4 times further

If branch not taken: PC = PC + 4
If branch is taken: PC = PC + 4 + (immediate * 4)

**NOTE:** For branch instruction, the first register is NOT rt but rs instead

## J-format
For branches, PC-relative addressing was used because we do not need to branch too far

For general jumps, we may jump to anywhere in memory!

|opcode|target address|
|------|------|

### opcode
- identical to R-format and I-format for consistency
- 6 bits

### target address
- 26 bits of 32-bit addresses
- jumps will only jump to word aligned addresses so assume the address ends with `00` and leave them out
- Now we can specify 28 bits of 32-bit addresses
- To make up for the other 4 bits
	- MIPS chose to take the 4 most significant bits from PC+4
	- This means we cannot jump to anywhere in memory, but should be sufficient most of the time
- Maximum jump range: 256MB boundary

![[Pasted image 20220930112929.png]]

## Addressing Modes

- **Register addressing**: operand is a register
- **Immediate addressing**: operand is a constant within the instruction itself (addi, andi, ori, slti)
- **Base addressing** (displacement addressing): operand is at the memory location whose address is sum of a register and a constant in the instruction (lw, sw)
- **PC-relative addressing**: address is sum of PC and constant in the instruction (beq, bne)
- **Pseudo-direct addressing**: 26-bit of instruction concatenated with upper 4-bits of PC (j)

![[Pasted image 20220905102814.png]]

![[Pasted image 20220930113046.png]]