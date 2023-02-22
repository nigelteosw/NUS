# Relational Algebra & SQL (Part 1)

## Discussions
### RA Operator
#### a)
FIrst find all the Restaurants that sells the pizzas that maggie likes
`Q1 = π[rname, pizza](Sells) / π[pizza](σ[cname='Maggie'](Likes))`

Then find the Restaurants that sells the pizzas that Ralph likes
`Q2 = π[rname](Sells ⋈ σ[cname='Ralph'](Likes))`

Then remove those restaurants from Q1
`Qans = Q1 - Q2`

#### b)
`π[A](R) - π[A]((π[A](R) x S) - R)`

### SQL DDL
```sql
CREATE TABLE Offices (
	office_id INTEGER
	building TEXT NOT NULL,
	floor INTEGER NOT NULL,
	room_number INTEGER NOT NULL,
	area INTEGER NOT NULL
	PRIMARY KEY (office_id)
	UNIQUE (building, floor, room_number)
);

CREATE TABLE Employees (
	emp_id INTEGER
	name TEXT 
	office_id INTEGER NOT NULL
	manager_id INTEGER
);
```