# Data Representation and Number Systems #
## Data Representation ##

Data is internally represented in a sequence of bits (binary digits)

Other units:
- Byte: 8 bits
- Nibble: 4 bits
- Word: Multiples of bytes depending on computer architecture (power of 2)

N bits can represent up to 2<sup>n</sup> values 
To represent M values log<sub>2</sub>M (ceiling) bits required

## Decimal (base 10) Number System
- A weighted-positional number system
- Base (also called radix) isn 10
- Each position has a weight of power of 10

## Other Number Systems ##
- Binary (base 2)
- Octal (base 8)
- Hexadecimal (base 16)

For programming language C
- Prefix 0 for octal. E.g. 032 is actually 26 decimal
- Prefix 0x for hexadecimal. E.g. 0x32 will represent the number (32)<sub>16</sub>

## Base-R to Decimal Conversion ##
![[Pasted image 20220811135621.png]]

## Decimal to Binary Conversion ##
### Repeated Division-by-2 ###
Only for whole numbers.
Keep dividing by 2 and get the remainder each time.
![[Pasted image 20220811140926.png]]

### Repeated Multiplication-by-2 ###
![[Pasted image 20220811140950.png]]

## Conversion Between Decimal and Other Bases ##
- Base-R to decimal: multiply digits with corresponding weights
- Decimal to base-R
	- Whole numbers: repeated division-by-R
	- Fractions: repeated multiplication-by-R

### Conversation Between Bases ###
In general, conversion between bases to be done via decimal.

## Binary to Octal/Hexadecimal Conversion ##
![[Pasted image 20220811141510.png]]

## ASCII Code ##
- ASCII code and Unicode are used to represent characters
- 7 bits, plus 1 parity bit (odd or even parity)
	- Parity allows for error detection 

A 32-bit signed integer. It has a minimum value of -2,147,483,648 and a maximum value of 2,147,483,647 (inclusive).

## Negative Numbers ##
- Unsigned numbers: only non-negative
- Signed numbers: includes both positive and negative


### Sign-and-Magnitude ###
- Using a sign bit, 0 for + 1 for -
- Largest value for 8 bit is +127<sub>10</sub>
- Smallest value for 8 bit is -127<sub>10</sub>
- For magnitude representation range is 2<sup>n-1</sup> -1
- Sign and magnitude cannot be used for arithmetic
- Sign and magnitude has 2 0s


### 1s Complement ###
- Just negate the value of the bits to get its 1s complement value
- Simply invert all the bits
- Negated value can be obtained in 1s-complement representation using: **-x = 2<sup>n</sup> - x - 1**
- 00001100<sub>2</sub> = 2<sup>8</sup> -12 - 1
			= 244
			= 11110011<sub>2s</sub>
- for 8 bits: -127 to 127
- for n bits: -(2<sup>n-1</sup>-1) to 2<sup>n-1</sup>-1
  

### 2s Complement ###
- Negated value can be obtained in 1s-complement representation using:  **-x = 2<sup>n</sup> - x 
- 00001100<sub>2</sub> = 2<sup>8</sup> -12
			= 244
			= 11110100<sub>2s</sub>
- *To find the negative, just invert the bits and add 1 to the values,*
- for 8 bits: -128 to 127
- -2<sup>n-1</sup> to 2<sup>n-1</sup>-1

## 2s Complement on Addition/Subtraction ##
### Addition of integers, A + B ###
1. Perform binary addition of the two numbers
2. Ignore the carry out of the MSB
3. Check for overflow. Overflow occurs if the 'carry in' and 'carry out' of the MSB are different, or if result is opposite sign of A and B.

### Addition for subtraction of integers, A - B
1. Take the 2s-complement of B. Add the 2s-complement of B to A

## Overflow ##
- Signed numbers are of a fixed range
- When addition/subtraction goes beyond the range
- positive add positive -> negatice
- negatice add negatice -> positive

## Excess Representation ##
- Allows range of values to be evenly distributed between the positive and negative values
- Excess 2<sup>n - 1</sup> usually to keep an almost even positive and negative number distribution

# Real Numbers #
There always exists a finite number of bits.

## Fixed-Point Representation
- In a fixed-point representation, number of bits allocated for whole numbers and fractions are fixed
- For example, in an 8 bit representation, 6 bits are for whole number and 2 bits are for fractional parts.
- Limited use
- ![[Pasted image 20220812190548.png]]


## Floating-Point Representation ##
- Can be used to represent very large or very small numbers/
- E.g. 0.23 * 10<sup>23</sup>
- 3 Components: sign, exponent and mantissa (fraction)
- ![[Pasted image 20220812190854.png]]
- The base is assumed to be 2.
- Two Formats:
	- Single-precision (32 bits) 1-bit sign, 8-bit exponent with bias 127, 23 bit-mantissa
	- Double-precision (64 bits) 1-bit sign, 11-bit exponent with bias 1023, and 52-bit mantissa
- Mantissa is normalised with an implicit leading bit 1
	- 110.1<sub>2</sub> -> 1.101<sub>2</sub> * 2<sup>2</sup> -> only 101 is stored in the mantissa field.

## [[IEEE Standard 754 Floating-Point Representation]] ##
- -6.5<sub>10</sub> = -110.1<sub>2</sub> = -1.101<sub>2</sub> × 2<sup>2</sup>
- Exponent = 2 + 127 = 129 = 10000001<sub>2</sub>
- ![[Pasted image 20220812192009.png]]
- Can be represented in hexadecimal: C0D00000<sub>16</sub>





