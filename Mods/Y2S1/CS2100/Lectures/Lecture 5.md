# Arrays, Strings and Structures#

### Advanced Data Types ###
- Arrays
- Strings

## Arrays ##
Declaration of array requires **element type, array name and size.**
- C arrays are 0 indexed
- Arrays occupy continuous memory locations
```C
#include <stdio.h>  
#define MAX 5  

int main(void) {  
	int numbers[MAX] = {4,12,-3,7,6};  
	int i, sum = 0;  
	
	for (i=0; i<MAX; i++) {  
		sum += numbers[i];  
	}  
	
	printf("Sum = %d\n", sum);  
	return 0;  
}
```

### Arrays and Pointers ###
- When the array name a appears in an expression, it refers to the address of the first element (i.e. &a[0]) of that array.
- memcopy()

### Modifying Array in a Function ###
- Have to pass in the address of the variable.
- In an array the array name is a pointer (address to the first element)

## Strings ##
- We can turn an array of characters into a **string** by adding a null character `\0` at the end of the array.
	- ASCII value of 0
- Can use string functions `<string.h>` to manipulate strings.
```C
char fruit_name[] = "apple";
// '\0' is automatically added
char fruit_name[] = {'a', 'p', 'p', 'l', 'e', '\0'};
```
- Read string from stdin (keyboard)
```C
fgets(str, size, stdin); 
// reads size -1 char or until newline
// never use gets(str) because of security reasons use fgets() function instead
scanf("%s", str);
// reads until white space

puts(str); // terminates with newline
printf("%s\n", str);
```
- Remove vowels
``` c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main(void) {
  int i, len, count = 0;
  char str[101], newstr[101];

  printf("Enter a string (at most 100 characters): ");
  fgets(str, 101, stdin); //what happens if you use scanf() here?
  len = strlen(str); // strlen() returns number of char in string
  if (str[len – 1] == '\n') {
	  str[len – 1] = '\0';
	}
	
  len = strlen(str); // check length again
  
  for (i=0; i<len; i++) {
	  switch (toupper(str[i])) {
		  case 'A': case 'E':
		  case 'I': case 'O': case 'U': break;
		  default: newstr[count++] = str[i];
		 }
  }

  newstr[count] = '\0';
  printf("New string: %s\n", newstr);
  return 0;

}
```


## Structures ##
- Structures allow grouping of heterogenous members of different types
- A group can be a member of another group
- Such a group is called a structure type
```C
typedef struct {  
	int stuNum;
	float score;
	char grade;  
} result_t;
```

- Declaring Ordinary Variables
```C
result_t result1, result2;
result_t result1 = {123321, 93.5, 'A'}
```

- Accessing Members of a Structure Variable
	- Use the dot(.) operator
```C
result_t result2;  
result2.stuNum = 456654;  
result2.score = 62.0;  
result2.grade = 'D';
```

- Reading a Structure Member
```C
result_t result1;  
printf("Enter student number, score and grade: ");  
scanf("%d %f %c", &result1.stuNum, &result1.score, &result1.grade);
```

- Assigning Structures
```C
result2.stuNum = result1.stuNum;  
result2.score = result1.score;  
result2.grade = result1.grade;
```

- Passing Structure to Function
```C
// #include statements and definition  
// of player_t are omitted here for brevity  
void print_player(char [], player_t);  

int main(void) {  
	player_t player1 = { "Brusco", 23, 'M' }, player2;  
	
	strcpy(player2.name, "July");  
	// cannot simply assign strings need use strncopy
	player2.age = 21;  
	player2.gender = 'F';  
	
	print_player("player1", player1);  
	print_player("player2", player2);  
	return 0;  
}  
// Print player’s information  
void print_player(char header[], player_t player) {  
	printf("%s: name = %s; age = %d; gender = %c\n", header, player.name, player.age, player.gender);  
}
```

- Passing Address of Structure to Function
	- Like an ordinary variable (eg: of type int, char), when a structure variable is passed to a function, a separate copy of it is made in the called function.
	- To allow the function to modify the content of the original structure variable, you need to pass in the address (pointer) of the structure variable to the function.