# MIPS Part 2

## Memory Organization##
- The main memory is viewed as a large, **single-dimension array**
- Each location of the memory has an **address**
	- Given a k-bit address, the address space is of size 2<sup>k</sup>

### Transfer Unit###
- Using distinct memory address
	- a single byte (byte addressable)
	- a single word (word addressable)
- Word is usually **2<sup>n</sup>** bytes
	- Also commonly coincide with the register size, the integer size and instruction size

### Word Alignment###
- Words are aligned in memory if they begin at a byte
	- Only can start at address 0, 4, 8

## Memory Instructions###
- MIPS is a load store register architecture
	- 32 registers, each 32-bit long (4 bytes)
	- Each word contains 32 bits
	- Memory addresses are 32 bits-long
	- 2<sup>30</sup> memory words as 2<sup>32</sup> /2<sup>2</sup> bits
	- **MIPS uses byte addresses, so each consecutive word differs by 4**


## Load and Store Instructions
- Only **load** and **store** instructions can access data in memory
```
// in C
A[7] = h + A[10];

# in MIPS Code
lw $t0, 40($s3) # load word at Mem[40] and store into temp
add $t0, $s2, $t0 # add $s2 into word and store as temp
sw $t0, 28($s3) # store word at Mem[28]
```
- each array element occupies a word
- `$s3` contains the base address (address of first element, A[0])  of array A. Variable h is mapped to `$s2`


### Load Word###
```
lw $t0, 4($s0) // instruction, dest, display(address)
```
1) Memory Address = $s0 + 4 = 8000 + 4 = 8004
2) Content of $t0 is stored into word at `Mem[8004]`

### Store Word###
```
sw $t0, 12($s0) // instruction, dest, display(address)
```
1) Memory Address = $s0 + 12 = 8000 + 12 = 80012
2) Content of $t0 is stored into word at `Mem[8012]`

## Others##
Other than load word (lw) and store word (sw),  
there are other variants, example:  
- load byte (lb)  
- store byte (sb)  
Similar in format:
```
lb $t1, 12($s3) # 1 byte
sb $t2, 13($s3) # 1 byte
```
- Similar in working except that one byte, instead of one word, is loaded or stored  
- Note that the offset no longer needs to be a multiple of 4
- MIPS disallows loading/storing unaligned word using lw/sw
	- Pseudo-Instructions **unaligned load word (ulw)** and **unaligned store word (usw)** are provided for this  purpose

## Array##
```
// C statement to translate
A[3] = h + A[1];

# in MIPS
lw $t0, 4($s3)
add $t0, $s2, $t0
sw $t0, 12($s3)
```

## Address vs Value##
**Registers do NOT have types**
- A register can hold any 32-bit number
```
add $t2, $t1, $t0 # $t0 and $t1 should contain data values
lw $t2, 0($t0) # $t0 should contain a memory address
```

## Byte vs Word##
**Consecutive word addresses in machines with byte-addressing do not differ by 1**
- Common error: assuming the address of the next word can be found just by incrementing the address in a register by 1
- Must be offset by a value of 4

## Swapping Elements##
```c
// C Statement
swap( int v[], int k )  
{  
	int temp;  
	temp = v[k]  
	v[k] = v[k+1];  
	v[k+1] = temp;  
}

/*
k -> $5  
Base address of v[] -> $4  
temp -> $15
*/

swap:
	# getting the correct address
	sll $2, $5, 2  # 12, 3, 2
	add $2, $4, $2  # 2012, 2000, 12
	# now $2 stores 2012 which is the address
	# now do the swap
	lw $15, 0($2)  
	lw $16, 4($2)  
	sw $16, 0($2)  
	sw $15, 4($2)

```

## Making Decisions##
To perform general computing tasks, we need to:  
- Make decisions (if-else)
- Perform iterations (loop)
- `goto` is discouraged in high-level languages but necessary in MIPS

Two types of decision-making statements in MIPS
1) Conditional (branch)
```
# Branch on Not Equal
# if both $t0 and $t1 are equal, the control will be taken to the next instruction, else it will branch to the label (index to another instruction)
bne $t0, $t1, label  

# Branch is Equal
# if both $t0 and $t1 are equal, will branch to the label
beq $t0, $t1, label
```
2) Unconditional (jump)
```
# will just immediately branch to the label
j label
```
- A label is an "anchor" in the assembly code to indicate point of interest, usually as branch target
	- **Labels are NOT instructions!** 

### BEQ###
`beq $r1, $r2, L1 ` 
- Go to statement labeled L1 if the value in register $r1 equals the value in register $r2  
- `beq `is “branch if equal”  
- C code: if (a == b) goto L1

### BNE###
`bne $r1, $r2, L1`
- Go to statement labeled L1 if the value in register $r1 does not  
equal the value in register $r2  
- `bne` is “branch if not equal”  
- C code: if (a != b) goto L1

### Unconditional Jump: j###
- Processor always follows the branch
`j L1`
- Jump to label L1 unconditionally
- C code: goto L1

### IF statement###
```c
if (i == j) {
	f = g+h
}

beq $s3, $s4, L1
j Exit
L1: add $s0, $s1, $s2
Exit:
```

## Inequalities
``` c
if ($s1 < $s2) {
	goto L;
}

slt $t0, $s1, $s2
bne $t0, $zero, L
# BLT is the pseudo-instruction
```

## Array and Loop##
```
# initialize
		addi $t8, $zero, 0   # result
		addi $t1, $zero, 0   # accumulator
		addi $t2, $zero, 40  # end point
	
loop: beq $t1, $t2, end   # if reach end point goto end
		sll $t3, $t1, 2       # address: i * 4 
		add $t4, $t0, $t3     # update the new address
		lw $t5, 0($t4)        # load up the value at the address
		bne $t5, $zero, skip  # if that item is not zero, skip
		addi $t8, $t8, 1      # add 1 to the result if item is zero
	
skip: addi $t1, $t1, 1    # add 1 to the accumulator
		j loop                # loop again
end:
```

I-format