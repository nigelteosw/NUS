# Pointers and Functions#
## Pointers ##
- It has pointers that allow direct manipulation of memory contents
- It has a set of bit manipulation operators for bitwise operations

A variable has:
- a name
- [[Data Types]]
- an address

- It is possible to refer to the address of the variable using the **address operator &** 
- %p is used as the format specifier for addresses
- addresses are printed out in [[Hexadecimal]] (base 16)

### Pointer variable ###
A variable that contains the address of another variable is called the pointer variable, or a pointer
Variable a_ptr is said to be pointing to variable a

### Declaring a Pointer ###
Syntax: `type *pointer_name;`
Type is the data type of the variable this pointer is pointing to

### Assigning Value to a Pointer ###
```C
int a = 123;
int *a_ptr;
a_ptr = &a;
```

### Accessing Variable Through Pointer ###
Accessing a variable using a pointer variable using a indirection operator (or dereferencing operator)
```C
printf("a = %d\n", *a_ptr);
printf("a = %d\n", a);
// *a_ptr is synonymous with a

int i = 10, j = 20;
int *p;

p = &i; // p now stores the address of var i

printf("value of i is %d\n", *p); // value of i is 10

*p = *p + 2;
// same effect as: i = i + 2 

p = &j; // p now stores the address of variable j

*p = i; // same effect as j = i since (*p is now j)
```

### Tracing Pointers ###
``` c
int a = 8, b = 15, c = 23;
int *p1, *p2, *p3;

p1 = &b;
p2 = &c;
p3 = p2;
printf("1: %d %d %d\n", *p1, *p2, *p3);

*p1 *= a;
while (*p2 > 0) {
  *p2 -= a;
  (*p1)++;
}

printf("2: %d %d %d\n", *p1, *p2, *p3);
printf("3: %d %d %d\n", a, b, c);
```

### Incrementing a Pointer ###
- p = p + 1 (or p++)
```C
int a; float b; char c; double d;
int *ap; float *bp;
char *cp; double *dp;

ap = &a; bp = &b; cp = &c; dp = &d;
printf("%p %p %p %p\n", ap, bp, cp, dp);

ap++; bp++; cp++; dp++;
printf("%p %p %p %p\n", ap, bp, cp, dp);

/* 
The variable will increment its value by the number of bytes equivalent to its size

e.g. int by 4 bytes, float by 4 bytes, char by 1 byte and double by 8 bytes
*/

ap += 3;
printf("%p\n", ap);
```

### Common Mistake ###
Segfault (segmentation fault)
- Happens when memory that is part of another program is reassigned
- Result: Segmentation Fault (core dumped)
	- Remove the file "core" from your directory

### Why Do We Use Pointers ###
- The purpose of a pointer:
	- To pass the address of two ore more variables to a function so that the function can pass back to its caller new values for the variables
	- To pass the address of the first element of an array to the function so that the function can access all elements in the array

# Functions
## Calling Functions
`scanf()` and `printf` requires `<stdio.h>`
To use math functions we need to include `<math.h>` and compile program with `-lm` option in sunfire
- `-lm` is a link to the math library when using `#include <math.h>`

Required to pass in the address of variables to `scanf`

## User-Defined Functions
```C
#include <stdio.h>
#include <math.h>
#define PI 3.14159

int main(void) {
    double d1, // inner diameter
           d2, // outer diameter
	         thickness, outer_area, inner_area, rim_area, volume;     

    // read input data
    printf("Enter inner diameter, outer diameter, thickness: ");
    scanf("%lf %lf %lf", &d1, &d2, &thickness);

    // compute volume of a washer
    outer_area = PI * pow(d2/2, 2);
    inner_area = PI * pow(d1/2, 2);
    rim_area = outer_area - inner_area;
    volume = rim_area * thickness;
    printf("Volume of washer = %.2f\n", volume);

    return 0;

}
```

### Modularize It ###
Since area of the circle is computed twice, we can use a area of circle function.
```C
double circle_area(double);

// This function returns the area of a circle
double circle_area(double diameter) {
  return PI * pow(diameter/2, 2);
}
```

## Pass-by-Value and Scope Rule ##
- Formal parameters are local to the function they are declared in.
- Local parameters and variables are only accessible in the function they are declared – **scope rule.**
- Variable that is passed is actually a value
- When a function is called, an activation record is created in the call stack, and memory is allocated for the local parameters and variables of the function.  
- Once the function is done, the activation record is removed, and memory allocated for the local parameters and variables is released. 
- Hence, local parameters and variables of a function exist in memory only during the execution of the function. They are called *automatic variables*.
- In contrast, *static variables* exist in the memory even after the function is executed.

```C
#include <stdio.h>  
void g(int, int);  

int main(void) {  
	int a = 2, b = 3;  
	printf("In main, before: a=%d, b=%d\n", a, b);  // 2,3
	g(a, b);  
	printf("In main, after : a=%d, b=%d\n", a, b);  // 2,3
	return 0;  
}  

void g(int a, int b) {  
	printf("In g, before: a=%d, b=%d\n", a, b);  // 2,3
	a = 100 + a;  
	b = 200 + b;  
	printf("In g, after : a=%d, b=%d\n", a, b);  // 102,203
}
```

### Void Function ###
- A function that may not return any value

### Swapping Values ###
- Using pointers effectively
```C
#include <stdio.h>  

void swap(int *, int *);  

int main(void) {  
	int a, b;  
	printf("Enter two integers: ");  
	scanf("%d %d", &var1, &var2);  
	swap( &a, &b );  
	printf("var1 = %d; var2 = %d\n", var1, var2);  
	return 0;  
}  

void swap(int *ptr1, int *ptr2) {  
	int temp;  
	temp = *ptr1; *ptr1 = *ptr2; *ptr2 = temp;
}
```

Example
```c
#include <stdio.h>

void f(int *, int *, int *);

int main(void) {
    int a = 9, b = -2, c = 5;
    f(&a, &b, &c);
    printf("a = %d, b = %d, c = %d\n", a, b, c);
    return 0;
}

void f(int *x, int *y, int *z) {
    *x = 3 + *y;
    *y = 10 * *x;
    *z = *x + *y + *z;
    printf("*x = %d, *y = %d, *z = %d\n", *x, *y, *z);
}
```
