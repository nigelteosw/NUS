# Tutorial 2

## Discussion Questions##
**Exploration: C to MIPS**

### D1.###
```mips
main:
        addiu   $sp,$sp,-32
        sw      $fp,28($sp)
        move    $fp,$sp
        li      $2,3                        # 0x3
        sw      $2,8($fp)
        li      $2,5                        # 0x5
        sw      $2,12($fp)
        lw      $3,8($fp)
        lw      $2,12($fp)
        nop
        addu    $2,$3,$2
        sw      $2,16($fp)
        move    $2,$0
        move    $sp,$fp
        lw      $fp,28($sp)
        addiu   $sp,$sp,32
        j       $31
        nop
```

- `addiu`
	- add immediate unsigned
	-  is used to add constants to signed integers when we don't care about overflow
- `sw`
	- store word
	- copy from register to memory
- `move`
	- move from hi
	- copy from special register `hi` to general register
- `li`
	- load immediate
	- Pseudo-instruction (provided by assembler, not processor!) Loads immediate value into register
- `nop`
	- instruction that does nothing (has no side-effect)
- `addu`
	- add unsigned number

### D2.###
a)


## Tutorial Questions##
1. Bitwise Operations

```
a = 5;
b = 22;
a = 00000101
b = 00010110
```
- `|` (bitwise OR) 
	- `a|b = 00010111`
	- 1 when a or b has a 1
- `&` (bitwise AND) 
	- `a&b = 00000100`
	- only 1 when both a and b are 1 
- `^` (bitwise XOR) 
	- `a^b = 00010011`
	- exclusive or
	- 1 when only a or b is 1 and not when both are 1
- `~` (one’s complement) 
	- `~a = 11111010`
	- 1s complement of a
- `<<` (left shift) 
	- `a<<b = 00000000`
	- shift left by 5 bits
- `>>` (right shift)
	- `a>>b = 00000000`
	- shift right by 5 bits

2. Swapping
```c
/* 
Step 1: Find the binary equivalent of the given variables
Step 2: Find X^Y and store it in x, i.e. X = X ^ Y.
Step 3: Again, find X^Y and store it in Y, i.e. Y = X ^ Y.
Step 4: Find X^Y and store it in X, i.e. X = X ^ Y.
Step 5: the numbers are now swapped
*/

#include <stdio.h>

int main() {
    int a, b;
    a = 5; 
    b = 7;
    printf("a is: %d \nb is: %d \n", a, b);
		a = a ^ b;        // 0010 = 0101 ^ 0111
    b = a ^ b;        // 0101 = 0010 ^ 0111
    a = a ^ b;        // 0111 = 0010 ^ 0101
    printf("a is now: %d \nb is now: %d \n", a, b);
}

void swap(int *a, int *b) {
	*a = *a ^ *b
	*b = *a ^ *b
	*a = *a ^ *b
}
```

**NOTE:** WEP, WPA and DES uses XOR
http uses public key to do modulo arithmetic, uses private key to form communications

3. MIPS Bitwise Operations
```
a.
lui $t0, 1
ori $t0, $t0, 0b0100001100000100
or $s1, $s1, $t0

b.
andi $0, $s1, 0b0000000010001010
# zero the corresponding bits in a
lui $t1, 0b111111111111111
ori $t1, $t1, 0b1111111101110101
and $s0, $s0, $t1
or $s0, $s0, $t0

c. 
lui $t0, 0000 0000 0000 0000 0000 0000 0100 0101 # bit masking
andi $t0, $t0, $s1
sll $t0, $t0, 1
or $s2, $t0, $t2

xori $t0, $s1, 0b10001010
andi $t0, $t0, 0b10001010 # sore the 1,3,7 bits into t0
sll $t0, $t0, 1
lui $t1, $t1, 0b111111111111111
ori $t1, $t1, 0b111111011101011
and $s2, $s2, $t1 
or


```


4. MIPS Arithmetic
```mips
a.
add $s2, $s0, $s1    # c = a + b

b.
sub $t0, $s1, $s2    # t0 = b - c
add $s3, $s0, $t0    # d = a + t0

c.
subi $t0, $s0, 2     # t0 = a - 2
sll $s1, $s1, 2      # b = 2b
add $s2, $t0, $s1    # c = 2b + t0

d.
sll $t0, $s0. 1      # a = 2a
add $t0, $t0, $s1    # 2a + b
sll $t1, $s2, 1      # c = 2c
sub $t0, $t0, $t1    # 2a + b - 2c
sll $s3, $t0, 2      # 4(2a + b - 2c)

```

5. [AY2013/14 Semester 2 Exam]
a) 
```mips
# standard design pattern
# checking if bit zero is a '1' or a '0'

$s0 = 0 0...00011111
$t1 = 1000 0000 0000 0000 0000 0000 0000 0000
$t2 = 0 0...00000001

# at most 31 iterations
# what happens in each iteration?
# Toggle the MSB of $s0 if $t2 = 1
# this is actually the even parity bit scheme

ai)
$s0 = 0000 0000 0000 0000 0000 0000 0001 1111
$s0 = 1000 0000 0000 0000 0000 0000 0001 1111

aii)
$s0 = 0101 0101 0101 0101 0101 0101 0101 0101
$s0 = 1101 0101 0101 0101 0101 0101 0101 0101

```
