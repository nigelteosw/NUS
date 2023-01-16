
# The Processor: Datapath

## Building a Processor: Datapath & Control

**Datapath**
- Collection of components that process data
- Performs the arithmetic, logical and memory operations

**Control**
- Tells the datapath, memory and I/O devices what to do according to program instructions

## MIPS Processor
- Simplest possible implementation of the MIPS ISA
	- Arithmetic and Logical operations
	- Data transfer instructions
	- Branches

## Instruction Execution Cycle (Basic)
1) Fetch:
   - Get instruction from memory
   - Address is in Program Counter(PC) Register
2) Decode:
   - Find the operation required
3) Operand Fetch:
   - Get operand(s) needed for operation
4) Execute:
   - Perform the required operation
5) Result Write (Store):
   - Store the results of the operation

## MIPS Instruction Execution

![[Pasted image 20220909155042.png]]

- Design changes:
	- Merge Decode and Operand Fetch - Decode is simple for MIPS
	- Split Execute into **ALU** (Calculation) and Memory Access

## Lets Build a MIPS Processor
- Look at each stage, figure out the requirements and processes
- Sketch a high-level block diagram, then zoom in for each elements  
- With the simple starting design, check whether different type of instructions can be handled:  
	- Add modifications when needed

## Fetch Stage
1) Use the *Program Counter (PC)* to fetch the instruction from memory
2) *Increment* the PC by 4 to get the address of the next instruction
   - How do we know next memory address is PC + 4
   - Exception using the branch/jump operation

![[Pasted image 20220909161129.png]]

**Instruction Memory**
- Storage element for the instructions  
	- It is a sequential circuit (to be covered later)  
	- Has an internal state that stores information
	- Clock signal is assumed and not shown

**Adder**
- Inputs:
	- Two 32-bit numbers A, B
- Output:
	- Sum of the input numbers, A + B

**Clocking**
- We are reading and updating the PC at the same time
- Magic of clock
	- PC is read during the first half of the clock period and it is *updated with PC+4 at the next rising clock edge*

## Decode Stage
- Instruction Decode Stage:  
- Gather data from the instruction fields:  
	1. Read the opcode to determine instruction type and field lengths  
	2. Read data from all necessary registers  
		- Can be two (e.g. add), one (e.g. addi) or zero (e.g. j)  
- Input from previous stage (**Fetch**):  
	- Instruction to be executed  
- Output to the next stage (**ALU**):  
	- Operation and the necessary operands


**Register File**
- Collection of 32 registers:
	- Each 32-bit wide
	- Read at most 2 registers
	- Write at most 1 register
- `RegWrite` is a control signal to indicate:
	- Writing of register
	- 1 (True) = Write, 0 (False) = No Write

### I-Format 
- Using a multiplexer to choose the correct write register number base on instruction type.
- For I-format, `RegDst` is always 0
- For R-format, `RegDst` is always 1 to pass the rt into the write register
- Take the immediate 16 bits and pass into operation 2.
	- Using sign extension to convert the 16 bits into 32 bits
- `ALUSrc` control signal to choose either "Read data 2" or the sign extended immediate 16 bits
	- `ALUSrc` will be 1

![[Pasted image 20220909172429.png]]

**Multiplexer**
- Function
	- Selects one input from multiple input lines
- Inputs:
	- n lines of same width
- Control:
	- m bits where n = 2<sup>m</sup>
- Output:
	- Select i'th output line if control = i


## ALU Stage
- Instruction ALU Stage:
	- ALU = Arithmetic-Logic Unit
	- Execution stage
	- Perform the real work for most of the instructions
- Input from previous stage (*Decode*)
- Output to the next stage (*Memory*)

**ALU (Arithmetic Logic Unit)**
- Inputs: Two 32 bit numbers
- Control: 4-bit to decide the particular operation
- Outputs: Result of arithmetic/logical operation
	- A 1-bit signal to indicate whether the results is zero

![[Pasted image 20220930115313.png]]

**Branch Instructions**
1. Branch Outcome:
   - Use ALU to compare the register
   - The 1-bit `isZero` signal is enough to handle equal/not equal check
 2. Branch Target Address:
    - Additional logic needed to calculate address
    - Need PC (from Fetch Stage)
    - Need Offset (from Decode Stage)
    - `ALUSRC` is set to 0 (exceptional case)


## Complete ALU Stage
![[Pasted image 20220909171357.png]]

## Memory Stage

![[Pasted image 20220909172240.png]]

### Data Memory
- Inputs:
	- Memory Address
	- Data to be written (Write Data) for store instructions
- Control:
	- Read and Write controls; only one can be asserted at any point in time
- Output:
	- Data read from memory (Read Data) for load instructions

`MemWrite` and `MemRead` are 1 or 0 depending on read and write

## Register Write Stage






![[Pasted image 20220910010138.png]]



