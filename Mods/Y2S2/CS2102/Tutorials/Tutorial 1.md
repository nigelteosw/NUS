# Relational Model & Relational Algebra

### Superkey
a) Possible superkeys of R include:
- {A, B, C, D}
- {A, C}
- {A, D}
- {A, B, D}
- {A, C, D}


Why cant it be a tuple of 3 items i.e. {A, B, C}
They can if they produce unique results

b) The possible candidate keys of R given that {A,C} is definately a superkey is only {A, C} since it is a minimal superkey

c) Only {A, C}
Includes {A, D} and {A, B, D}

### Foreign Key
W, Y and Z

### Equivalent
i) equivalent
ii) not equivalent
iii) equivalent
iv) equivalent

### Algebra
i) `σ[cname='Moe'](Likes) - σ[cname='Lisa'](Likes)`
ii)  `π[cname, rname](Restaurants ⋈ Sells ⋈ Likes ⋈ Customers)`
iii) 
```
Q1 = π[cname](Customers)× Pizzas
Qans = Q1 - Likes
```