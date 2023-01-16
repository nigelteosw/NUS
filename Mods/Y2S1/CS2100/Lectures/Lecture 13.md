# Boolean Algebra

## Digital Circuits

**Two Voltage levels**
- high/true/1/asserted
- low/false/0/deasserted

**Advantages of digital vs analog circuits**
- More reliable 
- Specified accuracy
- Consume less energy
- Ease design, analysis and simplification of digital circuit

Can be:
- Combinatorial: no memory, dependent of input
	- Gates
	- Decoders, multiplexers
	- Adders
- Sequential: with memory, output depends on input and current state
	- Counters, registers
	- Memories

**Boolean values:**
- True (T or 1)
- False (F or 0)

**Connectives:**
- Conjunction (AND)
	- $A \cdot B$
	- ![[Pasted image 20220924173502.png]]
- Disjunction (OR)
	- $A + B$
	- ![[Pasted image 20220924173530.png]]
- Negation (NOT)
	- $A'$
	- ![[Pasted image 20220924173541.png]]

**Precedence of Operators**
- Highest to Lowest
	- Not ($'$) 
	- And ($\cdot$)
	- Or ($+$)

**Laws of Boolean Algebra**
- Identity laws
- Inverse/complement laws
- Commutative laws
- Associative laws
- Distributive laws

**Duality**
- If the AND/OR operators and identity elements 0/1 in a Boolean equation are interchange, it remains valid.

**Theorems**
- Idempotency
- One element / zero element
- Involution
- Absorption 1
- Absorption 2
- DeMorgans'
- Consensus

**Standard Forms**
- Two standard forms:
	- Sum-of-Products (SOP)
	- Product-of-Sums (POS)
- Literals
	- A Boolean variable on its own or complemented form
- Product term
	- A single literal or a logical product (AND) of several literals
- Sum terms
	- A single literal or a logical sum (OR) of several literals
- Sum-of-Products (SOP)
	- A product term or a logical sum (OR) of several product terms
- Product-of-Sums (POS)
	- A sum term or a logical product (AND) of several sum terms
- Every Boolean expression can be expressed in SOP or POS form

**Minterms and Maxterms**
- A minterm is a product term that contains n literals from all the variables
- A maxterm is a sum term that contains n literals from all the variables
- In general with n variables we have up to 2<sup>n</sup> minterms and maxterms

![[Pasted image 20221004112435.png]]
