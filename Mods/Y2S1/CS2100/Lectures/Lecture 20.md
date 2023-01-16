# Pipelining

- Pipelining doesn't help the latency of a single task: It helps the throughput of the entire workload
- Multiple tasks operating simultaneously using different resources
- Possible delays:
	- Pipeline rate limited by slowest pipeline stage
	- Stall for dependencies


## MIPS Pipeline Stages

### Five Execution Stages
- IF: Instruction Fetch
- ID: Instruction Decode and Register Read
- EX: Execute an operation or calculate an address
- MEM: Access an operand in data memory
- WB: Write back the result into a register

**Idea**
- Each execution stage takes 1 clock cycle
- General flow of data is from one stage to the next

**Exceptions**
- Update of PC and write back of register file 


## Datapath
- Single-cycle implementation:
	- Update all state elements at the end of a clock cycle

- Pipelined implementation:
	- One cycle per pipeline stage
	- Data required for each stage needs to be stored separately

Data used by *subsequent instructions:*
- Store in programmer-visible state elements: PC, register file and memory

Data used by the *same instruction* in later pipeline stages
- Additional registers in datapath called *pipeline registers*

Pipeline registers are a collection of registers.
Pipeline registers can store:
- Control signals
- Register values
- Sign-extended immediate operand
- 32 bit instruction
- PC+4 value
- Register number (e.g., RR1, RR2 & WR)
- ALU outputs

### IF Stage
- IF/ID stores
	- Instruction read from InstructionMemory[PC]
	- PC + 4
- PC + 4 
	- Also connected to one of the MUX's inputs


### ID Stage
- IF/ID register supplies
	- register numbers for reading two registers
	- 16-bit offset to be sign-extended to 32 bit
	- PC + 4

- ID/EX register receives
	- Data values read from the register file
	- 32-bit immediate value
	- PC + 4


### EX Stage
- ID/EX register supplies
	-  Data values read from the register file
	- 32-bit immediate value
	- PC + 4

- EX/MEM register receives 
	- (PC + 4) + (Immediate x 4)
	- ALU result
	- `isZero?` signal
	- Data Read 2 from register file


### MEM Stage
- EX/MEM register supplies 
	- (PC + 4) + (Immediate x 4)
	- ALU result
	- `isZero?` signal
	- Data Read 2 from register file

- MEM/WB register receives
	- ALU result
	- Memory read data


### WB Stage
- MEM/WB register supplies
	- ALU result
	- Memory read data

- At the end of the cycle
	- Result is written back to register file
	- There is a bug
		- Pass write write register number all the way through all the register stages


## Pipeline Control
- Same control signals as single-cycle datapath
- *Difference:* each control signal belongs to a particular pipeline stage

**Decode Stage**
- Signals generated at the decode stage
- Forwarded through each pipeline stage

**Execution Stage**
- RegDst
- ALUSrc
- ALUop (op1 and op0)

**Memory Stage**
- MemRead
- MemWrite
- Branch

**Write Back Stage**
- MemToReg
- RegWrite


## Different Implementations
![[Pasted image 20221026222927.png | 500]]
