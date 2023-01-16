# Tutorial 1#
1. For the positive numbers, it is obvious why sign extension is value-preserving as adding 0s to the front of the MSB (most significant bit) does not add anything to the value of the bits. However for negative numbers, after sign extension, the difference between the old representation and the new representation is 0. Hence, there is no difference in the value by performing sign extension on negative numbers.
   
(5)<sub>10</sub> = (0101)<sub>2s</sub> = (00000101)<sub>2s</sub>
(-3)<sub>10</sub> = (1101)<sub>2s</sub> = (11111101)<sub>2s</sub>
MSB in **1**101 represents -8
MSB in **11111**101 represents -128, 64, 32, 16, 8 which sums up to -8

Weight of the first MSB is - 2<sup>k</sup>
Weight of the second MSB is:
	= -2<sup>m</sup> + (2<sup>m-1</sup> + ... + 2<sup>k+1</sup> + 2<sup>k</sup>)
	= -2<sup>m</sup> + 2<sup>k</sup>(2<sup>m-k</sup> - 1)
	= -2<sup>m</sup> + 2<sup>m</sup> - 2<sup>k</sup>
	= - 2<sup>k</sup>
   
2. Radix diminished complement
   n = 3, m = 2
   To get the 1s complement, (2<sup>3</sup> - 2<sup>-2</sup>) which is 1000.00 - 0.01 = 111.11
   This results in 100.10 which is the inverse of 011.01.
   a) Need to find the complement of 010.0101, just invert all the bits to 101.1010.
   Then do a sign extension, 0101.1100 + 1101.1010 = **1**0011.0110 then bring the carry around to (11.0111)<sub>1s</sub>
   b) Complement is 1000101.00**1**. Then sign extend the first number to 0010111.101. 0010111.101 + 1000101.001 = 1011100.110<sub>1s</sub> 
   Why is the value of the extended bit 1?
   0111010.110  -> 1000101.001
   
3. a) (0001.110)<sub>2s</sub> 
   b) 11110.011<sub>2s</sub> 
   Not correct, a tip is to remove the binary point
   0010.100 -> 0010100
   1101011 + 0000001 = 1101100
   (1101.100)<sub>2s</sub>
   
   c) (00011.111)<sub>2s</sub> 
   This is 3.875, approx to 3.876
   
   d) (0010.001)<sub>2s</sub>
   0.1 * 2 = 0.2
   0.2 * 2 = 0.4
   0.4 * 2 = 0.8
   0.8 * 2 = **1**.6 
   
4. Sign: 1
   Exponent: -0.078125 = -(0.000101)<sub>2</sub> = -(1.01)<sub>2</sub> * 10<sup>-4</sup>
   Hence exponent = -4 + 127 = 123 = (01111011)<sub>2</sub>
   Mantissa = 01000000000000000000000 (total of 23 bits)
   
   IEEE 754 form: 1-01111011-01000000000000000000000
   To write into decimal group into chunks of 4:
   1011-1101-1010-0000-0000-0000-0000-0000
   BDA00000


5. Complete `readArray()` and `reverseArray()`
```C
#include <stdio.h>

int readArray(int arr[], int limit) { 
	// ...
	int count;
	printf("Enter up to %d integers, terminating with a negative integer.\n", limit); 
	for (count = 0; count < limit; count++) {
		scanf("%d", &arr[count]);
	}
	// ... 
}

// iterative
void reverseArray(int arr[], int size) { 
	// ...
	int start = 0,end = size - 1;
	int temp;
	while (start<end) {
		temp = arr[start];
		arr[start] = arr[end];
		arr[end] = temp;
		start++;
		end++;
	}
}


// recursive
void reverseArray(int arr[], int start, int end) { 
// ...
	int temp;
	if (start >= end) {
		return;
	}
	temp = arr[start];
	arr[start] = arr[end];
	temp = arr[end];
	
	reverseArray(arr[], start++, end--);
}
```

6. Trace Program
```C
#include int main(void) { 
	int a = 3, *b, c, *d, e, *f; 
	
	b = &a;
	*b = 5;
	c = *b * 3; 
	d = b; 
	e = *b + c; 
	*d = c + e; 
	f = &e; 
	a = *f + *b; 
	*f = *d - *b; 
	printf("a = %d, c = %d, e = %d\n", a, c, e); printf("*b = %d, *d = %d, *f = %d\n", *b, *d, *f); return 0; }
```
![[photo_2022-08-22_14-52-24.jpg]]
**D will point to A not B**
