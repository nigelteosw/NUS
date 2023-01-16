
# Recitation 1 #
## Question 1 ##

Write a program that:
1. Asks for an operator, which can be “+”, “-“, “*”, “/” or “q”. 
2. If the operator is +, -, * or /, ask for two floating point numbers. 
3. Prints “Unrecognized operation” if the operator entered is not +, -, *, / or q. 
4. If the person enters ”q” the program says “Bye!” and exits. If the user enters +, -, *, /, the program performs the operation on the two numbers entered and prints the result in two decimal places.
5. If the user did not enter “q”, go to 1.

```C
#include <stdio.h>

int main() {
    // Write C code here
    char operation;
    double first, second, res;
    printf("Please enter an operation (+, -, *, / or q to quit): ");
    scanf("%c", &operation);
    
    if (operation == 'q') {
        printf("Bye!");
        return 0;
    } else if (operation != '+' 
			    && operation != '-' 
			    && operation != '*' 
			    && operation != '/') {
        printf("Unrecognized operation");
        return 0;
    }
    
    printf("Enter the first number: ");
    scanf("%lf", &first);
    
    printf("Enter the second number: ");
    scanf("%lf", &second);
    
    switch(operation){    
        case '+':    
            res = first + second; 
        break;   
         
        case '-':    
            res = first - second;    
        break;
         
        case '*':    
            res = first * second;    
        break; 
        
        case '/':    
            res = first / second;   
        break; 

        default:     
            printf("Unrecognized operation");
    }    
    printf("%.2f %c %.2f = %.2f \n", first, operation, second, res);
    return 0;
}
```

## Question 2 ##

Using what you know about number systems and C, show why this while loop may never end:

```C
float x = 0.0; 
while(x != 0.1) 
	x += 0.1;
```

