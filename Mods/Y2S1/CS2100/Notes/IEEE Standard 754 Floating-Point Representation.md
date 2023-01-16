# IEEE Standard 754 Floating Point Numbers

There are several ways to represent floating point number but IEEE 754 is the most efficient in most cases. IEEE 754 has 3 basic components:

1.  **The Sign of Mantissa –**  
    This is as simple as the name. 0 represents a positive number while 1 represents a negative number.
2.  **The Biased exponent –**  
    The exponent field needs to represent both positive and negative exponents. A bias is added to the actual exponent in order to get the stored exponent.
3.  **The Normalised Mantissa –**  
    The mantissa is part of a number in scientific notation or a floating-point number, consisting of its significant digits. Here we have only 2 digits, i.e. O and 1. So a normalised mantissa is one with only one 1 to the left of the decimal.

**Single Precision**
![[Pasted image 20220929222734.png]]

**Double Precision**
![[Pasted image 20220929222741.png]]

