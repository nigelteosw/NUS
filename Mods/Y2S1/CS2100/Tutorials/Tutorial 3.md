# Tutorial 3

## Discussion Questions
1)  Given two integer arrays A and B with unknown number of elements, and their base addresses stored in registers $s0 and $s1 respectively, study the MIPS code below. Note that an integer takes up 32 bits of memory.
![[Pasted image 20220905132100.png]]

a) The purpose of `$t1` is to keep track of the memory address of `$s1`.

b) array A = {7,4,5,6,0,5,9,0}
    array B = {3,4,1,2,1,0,0,9}

c) 2 store word operations

d) 0x1460FFF7

e) ble $t3, $t4, skip


## Tutorial Questions
1) Below is a C code that performs palindrome checking. A palindrome is a sequence of characters that reads the same backward or forward. For example, “madam” and “rotator” are palindromes.
![[Pasted image 20220905134640.png]]

a) C code into MIPS
```mips
			addi $s0, $zero, 0        # low = 0
			addi $s1, $s5, -1         # high = size-1
			addi $s3, $zero, 1        # matched = 1
			
loop: slt $t0, $s0, $s1         # (lo < hi)?
			beq $t0, $zero, exit      # exit if (lo >= hi)
			beq $s3, $zero, exit      # exit if (matched == 0)
			
			add $t1, $s4, $s0         # addr of str[lo]
			lb $t2, 0($t1)            # $t2 = str[lo]
			
			add $t3, $s4, $s1         # addr of str[hi]
			lb $t4, 0($t3)            # $t4 = str[hi]
			
			beq $s2, $s4, else        # compare str[lo], str[hi]
			addi $s3, $zero, 0        # matched = 0
			j endW                    # can also be "j loop"
			
else: addi $s0, $s0, 1          # lo++
			addi $s1, $s1, 1          # hi++
			
endW: j loop
			
exit:
```

Instead of testing the condition, reverse the condition to make it an exit condition. Exit the loop if condition is met.
Careful when the data is a byte. One character is one byte.
Changing adding addresses to using pointers:
- Instead of incurring 20 executions, we only do 2 executions

2) You accidentally spilled coffee on your best friend’s MIPS assembly code printout. Fortunately, there are enough hints for you to reconstruct the code. Fill in the missing lines (shaded cells) below to save your friendship.

|Instruction Encoding| MIPS Code|
|----------------------|-------------|
| | # $s1 stores the result, $t0 stores a non-negative number|
| 0x24010000 | addi $s1, $zero, 0 # Inst. address is 0x00400028| 
| 0x00084042 | loop: srl $t0, $t0, 1 |
| 0x11000002 | beq $t0, $zero, 2 |
| 0x22310001 | addi $s1, $s1, 1|
| | j loop |
| | exit: |

|opcode|rs|rt|immediate|
|--------|--|--|-----------|
|6|5|5|16|
|00100|00000|10001|0000000000000000|
(20110000)<sub>16</sub>

|opcode|rs|rt|immediate|
|--------|--|--|-----------|
|6|5|5|16|
|4|8|0|2|
|beq|$t0|\$t0|2| 

`j loop`
**Address to jump to:** 0x0040002C
|opcode|target|
|--------|------|
|6|26|
|opcode: 2| target address, not relative address |
|000010| |

b) 2<sup>$s1</sup> = $t0
    $s1 = log<sub>2</sub>(\$t0)
    

3) [AY2012/13 Semester 2 Assignment 3]
![[Pasted image 20220905141641.png]]

a) 
```mips
1) srl $s4, $s4, 1
2) lw $t1, 0($t0)
3) slt $t9, $t1, $s1 
4) beq $t9, $zero, equal
5) j end
6) j loop
```

b) 16

c) DO NOT take relative to program counter
    JUMP is always direct addressing
    

d) The encoding is the same, this is because the target is no different in terms of direct addressing.
