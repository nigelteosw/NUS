# The Processor: Control

## Identified Control Signals

![[Pasted image 20220921004312.png]]

- R-format instruction
	- `RegDst` = 1
	- rd should always be the write register
	- 6-bit "funct" determines ALU control
- Opcode -> Instruction Format
	- R -> 0
	- I -> Remaining Value
	- J -> 2
- MemToReg multiplexer 1 and 0 is reversed

### Control Unit
- Build the control unit using logic gates

### RegDst
Case 0:
If `RegDst = 0` rt[20:16] will be the write register
Case 1:
If `RegDst = 1` rd[15:11] will be the write register

### RegWrite
Determines if the `WD` should be written into `WR`
Case 0:
No register write
Case 1:
New value (WD) will be written (WR)

### ALUSrc
Case 0:
Operand 2 will be Register Read Data 2
Case 1:
Operand 2 will be Sign Extended (Inst[15:0])


### PCSrc (Branch)
Will make use of the isZero? output
Case 0:
PC + 4
Case 1:
PC + 4 + 4 * Immediate Operand


![[Pasted image 20220921012901.png]]

## Multilevel Decoding

Use a 2-bit ALUop signal

| Instruction Type | ALUop |
| ---------------| -----------|
| lw/sw | 00 |
| beq | 01 |
| R-type | 10 |

Use ALUop signal and Function Code field (for R-type instructions) to generate the 4-bit ALUcontrol signal

### Generating ALUcontrol Signal
![[Pasted image 20220930120237.png]]

## Outputs 

![[Pasted image 20220930120409.png]]
