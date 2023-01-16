# MIPS Part 1#

## Instruction Set Architecture ##
- Adding in C/C++, Java: A+B
- Compiler using assembly language add A,B (for MIPS)
- Assembler using machine language instructions: 1000 1100 1010 0000

- An abstraction on the **interface** between the hardware and the low level software
- This abstraction allows many implementations of varying cost and performance to run identical software. 
- Example: Intel x86/IA-32 ISA has been implemented by a range of processors starting from 80386 (1985) to Pentium 4 (2005)
	- Think of it as an API between software and hardware


## Machine Code vs Assembly ##
| Machine Code | Assembly Language |
| -------- | -----------|
| instructions in binary | human readable language |
| hard and tedious to code | easier to write than machine code |

1000 1100 1010 0000 <- ASSEMBLER <- add A, B



## Walkthrough##
### Components###
- Processor and Memory
- Input/output devices omitted 
- Processor - Perform computations
- Memory - Storage of code and data
- The code and data reside in the memory
	- Transferred to the processor during execution
- To avoid frequent access of memory
	- Temporary storage in the processor known as registers

### Memory Instruction ###
- Instruction to move data into register
	- load
- Moving data from register into memory
	- store

### Arithmetic###
- Sometimes, arithmetic operation uses a **constant** value instead of regular value

### Execution###
- Instruction is executed sequentially by default
- We need instructions to **change** the control flow based on **condition:**
	- Repetition (loop) and Selection (if-else) can both be supported

### Memory Instruction###
- Now we can move back the values from the register to their "home" in memory

### Summary###
- The stored-memory concept:  
	- Both instruction and data are stored in memory  
- The load-store model:  
	- Limit memory operations and relies on registers for storage during execution  
- The major types of assembly instruction:  
	- Memory: Move values between memory and registers  
	- Calculation: Arithmetic and other operations  
	- Control flow: Change the sequential execution

## General Purpose Registers##
- Registers are fast memories in the processor
- Limited in number
- **No data type** - Machine/Assembly assumes the data is of the correct type
- There are **32 registers** in **MIPS** assembly language
![[Pasted image 20220827114508.png]]

## MIPS Assembly Language##
- Each instruction executes a simple command
- Each line contains at most 1 instruction
- (hex-sign) is used for comments
- MIPS arithmetic/logic must have 3 operands, 2 source and 1 destination
```
# addition
add $s0, $s1, $s2
```
- $s0 = $s1 + $s2
- Important concept: MIPS arithmetic operations are mainly **register-to-register**
```
# subtraction
sub $s0, $s1, $s2
```
- $s0 = $s1 - $s2

What if we wanted to chain operators
```
a = b + c - d

# MIPS Assembly Code
add $t0, $s1, $s2 # temp = b + c
sub $s0, $t0, $s3 # a = temp - d
```
Can use more than two temporary registers.

### Constant/Immediate Operands###
```
addi $s0, $s0, 4 # a = a + 4
```
- **Immediate** values are numerical constant
- "Add immediate" (addi)
	- Source2 is a constant instead of register
	- The constant ranges from -2<sup>15</sup> to 2<sup>15</sup>-1 (16 bit 2s complement)
- there is no subi as we can use addi with negative constant

### Register Zero ($0 or $zero)###
```
add $s0, $s1, $zero # f = g + 0
```
- pseudo-instruction (move)
	- "Fake" instruction that gets translated to the corresponding MIPS instruction(s)
	- Provided for convenience in coding
```
move $s0, $s1
```

### Logical Operations###
**New Perspective**
- View 32 raw bits rather than a single 32-bit number
![[Pasted image 20220827121619.png]]
- **AND**
	- 1 if both bits are 1, otherwise 0
	- masking bits
- **OR**
	- 0 if both bits are 0, otherwise 1
	- forcing some bits to be 1
- **NOR**
	- 1 if both bits are 0, otherwise 0
	- NOT operation
- **XOR**
	- 1 if A is NOT the same as B

### Bitwise AND
- and can be used for masking operation:
	- Place 0s into the positions to be ignored è bits will turn into 0s
	- Place 1s for interested positions è bits will remain the same as the original.

## Large Constant##
- Loading a 32-bit constant into a register
- Use "load upper immediate" (lui) to set the upper 16-bit:
```
lui $t0, 0xAAA 
```
- Use "or immediate" (ori) to set the lower-order bits:
```
ori $t0, $t0, 0xF0F0
```


![[Pasted image 20220930013307.png]]