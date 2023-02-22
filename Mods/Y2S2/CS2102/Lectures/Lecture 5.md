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
```

- Distinct (by default duplicates are not elmin)