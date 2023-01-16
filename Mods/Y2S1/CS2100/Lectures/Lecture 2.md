# Introduction to C #

``` c
#include <std.io>
#define KMS_PER_MILE 1.0609

int main(void) {
	float miles, kms;

	/* Get the distance in miles */
	printf("Enter distance in miles: ");
	scanf("%f", &miles);

	// Convert the distance to kilometres
	kms = KMS_PER_MILE * miles;

	// Display the distance in kilometres
	printf("That equals %9.2f km. \n", kms);

	return 0;
}
```

## von Neumann Architecture ##
- Central Processing Unit (CPU)
	- Registers
	- A control unit containing an instruction register and program counter
	- An arithmetic/logic unit (ALU)
- Memory
	- Stores both program and data in random-access memory (RAM)
- I/O devices

## Variables ##
C is a statically typed language
i.e. int count;

## [[Data Types]] ##
- int: For integers
	- 4 bytes (8 bits)
- float or double: For real numbers
	- 4 bytes for float and 8 bytes for double
- char: For characters
	- Enclosed in a pair of single quotes (e.g. 'A', '2', '*')

C is a strongly typed language: every variable to be declared with a data type.


## Program Structure ##
1. Preprocessor directives:
	- e.g. #include <stdio.h> 
	- Inclusion of header files
		- scanf() and printf() requires <stdio.h> 
	- Conditional compilation
	- Macro expansions
		- define a macro for a constant value
		- e.g. 
```c
#define PI 3.142
```

2. Input: through stdin (using scanf)
Placeholder | Variable Type | Function Use
------------ | ------------ | ------------- 
%c | char | printf / scanf
%d | int | printf / scanf
%f | float or double | printf
%f | float | scanf
$lf | double | scanf
%e | float or double | printf (for scientific notation)

3. Compute: through arithmetic operations and assignment statements
4. Output: through stdout (using printf), or file output

## Compute ##
Function body has...
- Declaration Statements
	- case sensitive
	- Cannot use reserved words
		- special meaning in C
		- e.g. int, void, double return
	- Standard identifiers
		- names of common functions such as printf, scanf
	- May consistof letters, digits and underscores but must not begin with a digit

- Executable Statements
	- Assignment Statements 
		- (Note: ‘=’ means ‘assign value on its right to the variable on its left’; it does NOT mean equality)
	- Side effects
		- z = a = 12 is the same as z = (a = 12)
		- a = 5 + (b = 10); // assign 10 to b, and 15 to a
		  
```C
int main(void) {
	/* Dec;araton Statements */
	/* Executable Statements */
	return 0;
}
```


## Arithmetic Operators ##
```C
// To illustrate some arithmetic operations in C

#include <stdio.h>

int main(void) {

  int x, p, n;

  // to show left associativity

  printf("46 / 15 / 2 = %d\n", 46/15/2);

  printf("19 %% 7 %% 3 = %d\n", 19%7%3);

  // to show right associativity

  x = -23;

  p = +4 * 10;

  printf("x = %d\n", x);

  printf("p = %d\n", p);

  // to show truncation of value

  n = 9 * 0.5;

  printf("n = %d\n", n);

  return 0;

}
```

## Selection Structures ##
If Else Statements

```C
if (condition) {

  /* Execute these statements if TRUE  */

}

else {

  /* Execute these statements if FALSE */ 

}
```

Switch Statements

```C
/* variable or expression must be of discrete type */

switch ( <variable or expression> ) {

  case value1:
  // Code to execute if <variable or expr> == value1
  break;

  case value2:
  // Code to execute if <variable or expr> == value2
  break;

  /* ... */

  default:
  /* Code to execute if <variable or expr> does not
  equal to the value of any of the cases above */*
  break;

}
```

## Truth Values ##
There is **no** Boolean type in ANSI C.
integers: 
- 0 to represent false
- Any other value to return true

## Logical Operators ##
Complex condition: combining two or more Boolean expressions.
Logical operators are needed: &&(and), || (or), ! (not).

| A | B | A && B | A \|\| B | !A |
|---|---|---|---|---|
| False | False | False | False | True |
| False | True | False | True | True |
| True | False | False | True | False |
| True | True | True | True | False |





## Short-Circuit Evaluation ###
### Or Lazy Evaluation ###

## Repetition Structures ##
### While Loop ###
```C
while ( condition )
{
   // loop body
}
```

### Do Loop ###
```C
do
{
   // loop body
}  while ( condition );
```

### For Loop ###
```C
for ( initialization; condition; update )
{
    // loop body
}
```

## Continue and Break ##
### Break ###
The `break` statement ends the loop immediately when it is encountered.

### Continue ###
The `continue` statement skips the current iteration of the loop and continues with the next iteration.




