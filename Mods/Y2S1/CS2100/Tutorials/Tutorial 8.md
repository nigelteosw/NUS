# Tutorial 8

## Tutorial Questions 

### Question 1
F(X, Y, Z) = $\prod$M(1, 5, 6) $\cdot$ D(4)
Since the product of maxterms is complement to the sum of minterms
$\sum$m(0, 2, 3, 7) $\cdot$ D(4)

| X | Y | Z | F | 
|-|-|-|-|
|0|0|0|1|
|0|0|1|0|
|0|1|0|1|
|0|1|1|1|
|1|0|0|X|
|1|0|1|0|
|1|1|0|0|
|1|1|1|1|

a) ![[Pasted image 20221017153809.png]]

b) ![[Pasted image 20221017153826.png]]


### Question 2
a) The circuit below shows two 2×4 decoders with 1-enable and active high outputs. What is the simplified SOP expression for K?

K(W,X,Y,Z) = $\sum$m(8, 11)

| W | X | Y | Z | K |
|-|-|-|-|-|
|0|0|0|1|0|
|0|0|1|0|0|
|0|0|1|1|0|
|0|1|0|0|0|
|0|1|0|1|0|
|0|1|1|0|0|
|0|1|1|1|0|
|1|0|0|0|0|
|1|0|0|1|1|
|1|0|1|0|0|
|1|0|1|1|0|
|1|1|0|0|1|
|1|1|0|1|0|
|1|1|1|0|0|
|1|1|1|1|0|


W$\cdot$Y'$\cdot$(X+Y)
= W$\cdot$X$\cdot$Y'$\cdot$Z' + W$\cdot$X'$\cdot$Y'$\cdot$Z
![[Pasted image 20221017155357.png]]


### Question 3
![[Pasted image 20221017161954.png]]


### Question 4

F(A, B, C, D) = $\sum$m (0,1,3,4,6,7,8,9,11,12,14,15)
F'(A, B, C, D) = $\sum$m (2, 5, 10 ,13)


| A | B | C | D | F |
|-|-|-|-|-|
|0|0|0|0|0|
|0|0|0|1|0|
|0|0|1|0|1|
|0|0|1|1|0|
|0|1|0|0|0|
|0|1|0|1|1|
|0|1|1|0|0|
|0|1|1|1|0|
|1|0|0|0|0|
|1|0|0|1|0|
|1|0|1|0|1|
|1|0|1|1|0|
|1|1|0|0|0|
|1|1|0|1|1|
|1|1|1|0|0|
|1|1|1|1|0|


![[Pasted image 20221017163219.png]]
