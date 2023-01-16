# Basic Probability Concepts and Definitions #
- **Statistical Experiment:** any procedure that obtains data
- **Sample Space:** (denoted by S): Set of all possible outcomes
- **Sample Point:** Every outcome(element) in a sample space
- **Events:** Subset of a sample space

### Tossing a die ###
- Sample space: S = {1,2,3,4,5,6}.
- Sample point: 1 or 2 or 3 or 4 or 5 or 6
- Events: (1) an event where an odd number occurs = {1,3,5}
- Sample space itself is an event called a **sure event.** 
- An event that contains no element is the empty set also known as a null event.

### Event Operations (Set Operations) ###
- Denote S by the sample space where $A$ and $B$ are two events
- Event operations include:
	- Union: $A \cup B$
		- Event containing all elements beloing to $A$ or $B$ or both
	- Intersection: $A \cap B$
		- Events containing elements that belong to both $A$ and $B$
	- Complement: $A'$
		- Events with elements in $S$, which are not in $A$
- Possible event relationshops:
	- Contained
		- If all elements in $A$ are also elements in $B$
	- Equivalent
		- If $A == B$ 
	- Mutually Exclusive
		- They $A$ and $B$ has no elements in common
	- Independent

![[Pasted image 20220814141420.png]]

### De Morgan's Law ###
![[Pasted image 20220814141656.png]]

## Counting Principles ##
### Multiplication Principle ###
Suppose that r different experiments are to be performed sequentially.

### Addition Principle ###
Suppose that the “ways" under different procedures are not overlapped. Then the total number of ways that we can perform the experiment is added up.

## Permutation ##
• A permutation is a selection and arrangement of r objects out of n. In this case, order is taken into consideration.
![[Pasted image 20220814143822.png]]

## Combintation ##
- A combination is a selection of r objects out of n, without regard to the order.
- $n \choose r$ 

## Probability ##
- Probability is understood as the chance or how likely an event will occur.
- $0 < x < 1$
- $P(S) == 1$
- For any 2 mutually exclusive events, $P(A \cup B) = P(A) + P(B)$
- Probability of an empty set is always 0
- $P(A') = 1 - P(A)$ 

![[Pasted image 20220901004603.png]]

## Conditional Probability
Specifically, we might need to compute the probability of an event B, given that we have the information “an event A has occurred".

$P(B | A) = \frac {P(A\cup B)} {P(A)}$ 

