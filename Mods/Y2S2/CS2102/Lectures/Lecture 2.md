# Relational Algebra
### Operators
- Unary
	- selection (σ), projection (π), renaming (ρ)
- Binary 
	- cross product (×), union (∪), intersection (∩), difference (−)


### Closure Property
We say that a _set_ of values is **closed** under the set of operators if any combination of the operators _produces only values in the given set_.


![[Pasted image 20230221012000.png]]

![[Pasted image 20230221012204.png | 320]] ![[Pasted image 20230221012237.png | 320]]


### Selection
σ symbol

### Projection
π symbol

### Rename
ρ symbol


## Joins
### Inner Joins
#### θ-Join
The θ-join (**_R ⋈[θ] S_**) of two relations _R_ and _S_ is defined as: **_R ⋈[θ] S = σ[θ]_(R × S)_**

#### Equi Join
Equi join (**_R ⋈= S_**) is a special θ-join where the only relational operator that can be used is equality (e.g., = or ≡)

#### Natural Join
-   The join is performed over all **_common attributes_** between _R_ and _S_ (i.e., (B1, B2, ..., Bj))
    -   We only combine if the value of the common attributes are **_equal_**
    -   The output relations contains the common attribute of _R_ and _S_ **_only once_** (via projection)

### Outer Joins
![[Pasted image 20230221013800.png]]