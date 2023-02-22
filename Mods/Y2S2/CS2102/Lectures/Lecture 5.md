# SQL 02

### SQL vs Relational Algebra
|          | Relational Algebra                          | SQL                                                  |
| -------- | ------------------------------------------- | ---------------------------------------------------- |
| Paradigm | Imperative (query language using operators) | Declarative (language built upon relational algebra) |
| Semantic | Set (no duplicate rows/tuples)              | Multiset/Bag (allows duplicate rows/tuples)          |
| Query    | Relational algebra expression               | SELECT statement                                                     |

#### Select Statement
```sql
SELECT [ DISTINCT ] <target-list>
FROM <relation-list>
[ WHERE <conditions> ];

/* 
π[a1, a2, ..., am](σ[c](r1 × r2 × ... × rn))
*/
```

- `DISTINCT` (by default duplicates are not eliminated hence explicit specification)
- `<target-list>` list of attributes/columns of the output
- `<relation-list>` list of relations that are relevant to answer the given query
- `<conditions>` conditions that specify a valid result row/tuple

- Order-Independent

#### Operations
- Mathematical  
- String 
	- || (concatenate)
	- LOWER(s)
	- UPPER(s)
- Date Time

#### Renaming
- column AS alias


## Join Operations
### Restriction
```sql
SELECT r1.rname, r2.rname
FROM   Restaurants AS r1, Restaurants r2
WHERE  r1.rname < r2.rname
  AND  r1.area = r2.area;
```
### Multi-Relational
```sql
SELECT DISTINCT rname, price
FROM   Sells S, Recipes R
WHERE  S.pizza = R.pizza
  AND  R.ingredient = 'Cheese';
```
### Natural Join
```sql
SELECT DISTINCT rname, price
FROM   Sells S NATURAL JOIN Recipes R
-- no need S.pizza = R.pizza, why?
WHERE  R.ingredient = 'Cheese';
```
### Outer Join
```sql
SELECT DISTINCT C.cname
FROM   Customers C LEFT JOIN Likes L
    ON C.cname = L.cname
WHERE  L.pizza IS NULL; -- keep only dangling tuples

```

