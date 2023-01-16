# Tutorial 4

1) Given below are the contents of some registers and memory locations, where mem(A) refers to the data word stored in the memory location at address A

![[Pasted image 20220912143508.png]]

| | Operand | Target Memory Address | Content |
| - | --------|----------------------------|----------|
| a) | $t1, $t2 | NA, NA | 15000, 20000 |
| b) | \$s2, 100($zero) | NA, 100 | 200, 1000 | 
| c) | \$t4 40($s2) | NA, 240| 30000, 2400|
| d) | \$s3 200($zero) |NA, 200|240, 2000|
| e) | \$t3 \$zero($t1)|NA, cannot use register for displacement|25000, illegal|
| f) | \$s1 140($s1) |NA, 300|160, 3000|

b) You are tasked to design a dedicated 16-bit processor to perform simple addition and would like to evaluate the design using the four different instruction set architecture (ISA) styles. For each of these architectures, the corresponding data movement and arithmetic operations are shown below. Note that the operands for the instructions are annotated with either @ for address, or $ for register.

| Stack | Accumulator | Memory-Memory | Register-Register |
|------|----------------|---------------------|-------------------|
| push @a1 | load @a1  | add @a0, @a1, @a2 | load $r1, @a1     |
| push @a2 | add @a2   | add @a1, @a0, @a2 | load $r2, @a2     |
| add      | store @a0 | add @a2, @a0, @a1 | add $r0, $r1, $r2 |
| pop @a0  | add @a2   |                   | store @a0, $r0    |
| push @a0 | store @a1 |                   | load $r0, @a0     |
| push @a2 | add @a0   |                   | load $r2, @a2     |
| add      | store @a2 |                   | add $r1, $r0, $r2 |
| pop @a1  |           |                   | store @a1, $r1    |
| push @a0 |           |                   | load $r0, @a0     |
| push @a1 |           |                   | load $r1, @a1     |
| add      |           |                   | add $r2, $r0, $r1 |
| pop @a2  |           |                   | store $r2, @a2    |
**Note:** For stack, to write the data to the address, we need to push the address

**Note:** For accumulator, there is no need to reload what is currently in the processor

3) This is a follow up on question 2. We studied the assembly code generated for four different storage architectures, namely stack, accumulator, memory-memory and register-register. For your reference, the code fragment corresponds to the following high level statements:

a)
- 3 bits opcode
- 7 bits for addressable memory
- 3 bits for general purpose register

Stack:
- 3 op, 7 for memory
- 10 bits for longest instruction
- 2 bytes for instruction

Accumulator:
- 3 op, 7 for memory
- 10 bits for longest instruction
- 2 bytes for instruction

Memory-Memory:
- 3 op, 7 memory, 7 memory, 7 memory
- 24 bits for longest instruction
- 4 bytes for instruction
	- We need to word align the memory since it is 16-bit architecture
	- We should always design it to be word aligned

Register-Register:
- 3 op, 3 register, 7 for memory
- 13 bits for longest instruction
- 2 bytes for instruction

b) 
Stack:
- 12 instructions * 2 bytes = 24 bytes

Accumulator:
- 7 instructions * 2 bytes = 14 bytes

Memory-Memory:
3 instructions * 4 bytes = 12 bytes

Register-Register:
8 instructions * 2 bytes = 16 bytes

4) [Past-year’s exam question] An ISA has 16-bit instructions and 5-bit addresses. There are two classes of instructions: class A instructions have one address, while class B instructions have two addresses. Both classes exist and the encoding space for opcode is completely utilized.

a) Minimum amount: 2<sup>6</sup> - 1 + 2<sup>5</sup>  = 63 + 32 = 95

b) Maximum amount: (2<sup>6</sup> - 1) * 2<sup>5</sup>  + 1 = 2016 + 1 = 2017 