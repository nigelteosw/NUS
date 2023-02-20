
## What is a Database?
- A database is a collection of organised data, information, and records.


## ACID Properities
Let a transaction be T
- Atomicity (either all effects of T are reflected in the database or none)
- Consistency (T gurantees to yield the correct state of the database)
- Isolation (T is isolated from the effect of concurrent transactions)
- Durability (after a commit of T, its effects are permanent)


## Serialisation
### Equivalent Transaction
Two executions are equivalent if they have the same effect on the data.

### Serializability 
A concurrent execution of a set of transaction is serializable if this execution is equivalent to some serial execution of the same set of transactions.


## Keys
### Superkey
In a database, a **superkey** is a set of one or more attributes (columns) that can uniquely identify each record in a table. For example, in a table of customer information, a superkey might be a combination of the customer's name, phone number, and email address.

### Key
A **key** is a subset of a superkey that can uniquely identify each record in a table. In other words, a key is a minimal set of attributes that can still uniquely identify every record. For example, in the customer information table, a key might be just the customer's email address, since that's enough to uniquely identify each customer.

### Candidate key
A **candidate key** is a key that could potentially be chosen as the primary key of a table. In other words, a candidate key is a set of attributes that could be used to uniquely identify each record, but it hasn't been chosen as the primary key yet. In the customer information table, for example, the customer's email address is a candidate key, as is the customer's phone number.

### Primary Key 
A **primary key** is the chosen key that uniquely identifies each record in a table. In other words, it's the candidate key that has been selected as the primary way to identify records. In most cases, a primary key is a single column, but it can also be a combination of columns. For example, in the customer information table, the primary key might be the customer's email address.

### Foreign Key
A **foreign key** is a column in one table that refers to the primary key of another table. It's used to establish a relationship between the two tables. For example, in a database for an online store, the customer information table might have a foreign key column that refers to the primary key of the order information table. This would allow the store to link each customer to their orders.

