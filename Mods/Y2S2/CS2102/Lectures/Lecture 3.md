# SQL 01
## Structured Query Language
- Domain-specific language
- Declarative language
	- What to compute, instead of how to compute


#### Non-Interractive SQL
##### Statement Level Interface (SLI)
-   Application is a _mixture_ of host language (e.g., C, Java, Python) and SQL statements
    -   **_Example:_** Embedded SQL, Dynamic SQL

##### Call Level Interface (CLI)
-   Application is _entirely_ written in the host language (e.g., C, Java, Python)
    -   **_Example:_** ODBC (Open DataBase Connectivity), JDBC (Java DataBase Connectivity)


#### Interactive SQL
- Directly writing SQL statements to an interface


## SQL Commands
### Create Table
```sql
CREATE TABLE <table_name> (
	<attr1> <type1> [<column_constraint>],
	<attr2> <type2> [<column_constraint>],
	⁝
	<attrn> <typen> [<column_constraint>],
	[<table_constraint>], -- comment
	[<table_constraint>], /* comment */
	⁝
	[<table_constraint>] -- no comma
);


/*For Example*/
CREATE TABLE Employees (
	id INTEGER,
	name VARCHAR(50),
	age INTEGER,
	role VARCHAR(50)
);
```
SQL is case-insensitive

#### Data Types
| Type           | Description                             |
| -------------- | --------------------------------------- |
| BOOLEAN        | Logical Boolean                         |
| INTEGER(int)   | Signed 4-bytes integer                  |
| FLOAT8         | Double precision 8-bytes floating point |
| NUMERIC[(p,s)] | Exact numeric of selectable precision   |
| CHAR(n)        | Fixed-length character string           |
| VARCHAR(n)     | Variable-length character string        |
| TEXT           | Variable-length character string        |
| DATE           | Calendar date (year,month,day)          |
| TIMESTAMP      | Date and time                                        |

#### Extended Data Types
| Kinds    | Types          |
| -------- | -------------- |
| Document | XML            |
|          | JSON           |
| Spatial  | Point          |
|          | Line           |
|          | Polygon        |
|          | Circle         |
|          | Box            |
|          | Path           |
| Special  | Money/Currency |
|          | MAC/IP Address |



### Insert
```sql
INSERT INTO <table_name> [(attr_1, attr_2, ..., attr_n)]
	VALUES
		(<val_1_1>, <val_2_1>, ..., <val_n_1>),
		(<val_1_2>, <val_2_2>, ..., <val_n_2>),
		⁝
		(<val_1_m>, <val_2_m>, ..., <val_n_m>);

/*For Example*/
INSERT INTO Employees
	VALUES (101, 'Sarah', 25, 'dev');
```

- Either all or none inserted
- Attributes can be specified out of order


### Default
```sql
CREATE TABLE Employees (
	id INTEGER,
	name VARCHAR(50),
	age INTEGER,
	role VARCHAR(50) DEFAULT 'sales' /*defaults to sales if var not provided*/
);
```


### Delete
```sql
DELETE FROM <table_name>
	[ WHERE <condition> ];

DELETE FROM Employees;
-- delete all!

DELETE FROM Employees
	WHERE role <> 'dev';
```


##### Principle of Rejection
**Reject** the insertion if the condition **_evaluates to False_**.
-   Used in integrity constraints


### Three Valued Logic
#### IS [NOT] NULL
| x        | x is NULL | x is not NULL |
| -------- | --------- | ------------- |
| not-NULL | False     | True          |
| NULL     | True      | False         |

#### IS [NOT] DISTINCT FROM
| x        | y        | x is distinct from y | x is not distinct from y |
| -------- | -------- | -------------------- | ------------------------ |
| not-NULL | not-NULL | x <> y               | x = y                    |
| not_NULL | NULL     | True                 | False                    |
| NULL     | not-NULL | True                 | False                    |
| NULL     | NULL     | False                | True                     |

### Types of Integrity Constraints
1.  [Not-`NULL`](https://www.comp.nus.edu.sg/~cs2102/03_SQL_01.html#NotNull) Constraints
2.  [Unique](https://www.comp.nus.edu.sg/~cs2102/03_SQL_01.html#Unique) Constraints
3.  [Primary Key](https://www.comp.nus.edu.sg/~cs2102/03_SQL_01.html#PK) Constraints
4.  [Foreign Key](https://www.comp.nus.edu.sg/~cs2102/03_SQL_01.html#FK) Constraints
5.  [General](https://www.comp.nus.edu.sg/~cs2102/03_SQL_01.html#Check) Constraints

#### Not-NULL Constraint
```sql
-- Unnamed
CREATE TABLE Employees (
	id INT NOT NULL,
	name TEXT NOT NULL,
	age INT,
	role TEXT
);

-- Named
CREATE TABLE Employees (
	id INT CONSTRAINT nn_id NOT NULL,
	name TEXT CONSTRAINT nn_name NOT NULL,
	age INT,
	role TEXT
);
```


#### Unique Constraint
```sql
-- Column Constraints
-- Unnamed
CREATE TABLE Employees (
  id    INT  UNIQUE,
  name  TEXT,
  age   INT,
  role  TEXT
);

-- Named
CREATE TABLE Employees (
  id    INT  CONSTRAINT emp_id UNIQUE,
  name  TEXT ,
  age   INT,
  role  TEXT
);

-- Table Constraints
-- Unnamed
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  UNIQUE (eid, pname)
);

-- Named
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  CONSTRAINT team_id UNIQUE (eid, pname)
);
```


### Primary Key Constraint
##### Definition
A **primary key** is a _selected **candidate keys**_.
-   Uniquely identifies a tuple in a relation
-   Cannot be `NULL`

In other words, `UNIQUE` and `NOT NULL`

```sql
-- Column Constraint
-- Unnamed
CREATE TABLE Employees (
  id    INT  PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);

-- Named
CREATE TABLE Employees (
  id    INT  CONSTRAINT emp_pk PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);

-- Table Constraint
-- Unnamed
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  PRIMARY KEY (eid, pname)
);

-- Named
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  CONSTRAINT team_pk PRIMARY KEY (eid, pname)
);

```


#### Constraint on Referencing Relation
```sql
CREATE TABLE Teams (
  eid     INT,
  pname   TEXT REFERENCES Projects,
  hours   INT,
  PRIMARY KEY (eid, pname),
  FOREIGN KEY (eid) REFERENCES Employees (id)
);

-- Referenced Relations
CREATE TABLE Employees (
  id    INT  PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);

CREATE TABLE Projects (
  name        TEXT,
  start_year  INT,
  end_year    INT,
  PRIMARY KEY (name)
);


```


### Delete Actions
`NO ACTION`
_Reject_ delete/update if it violates constraint (default value)

`RESTRICT`
Similar to "`NO ACTION`" except that check of constraint _cannot be deferred_ (deferrable constraints are discussed in a bit)

`CASCADE`
_Propagates_ delete/update to the referencing tuples

`SET DEFAULT`
_Updates_ the foreign key of the referencing tuples to some default value (**Important:** default value must be a primary key in the referenced table)

`SET NULL`
_Updates_ the foreign key of the referencing tuples to `NULL` value (**Important:** corresponding column must be allowed to contain `NULL` values)

```sql
CREATE TABLE Teams (
  eid    INT,
  pname  TEXT DEFAULT 'FastCash',
  hours  INT,
  PRIMARY KEY (eid, pname),
  FOREIGN KEY (eid) REFERENCES Employees (id) ON DELETE NO ACTION ON UPDATE CASCADE,
  FOREIGN KEY (pname) REFERENCES Projects (name) ON DELETE SET DEFAULT ON UPDATE CASCADE
);
```

- Updates on _Employees.id_ and _Projects.name_ are _propagated_
- Deleting a project will set _Teams.pname_ to _default value_ (i.e., FastCash)
- Deleting an employee will _raise an error_ if that employee is still assigned to a team

```sql
-- Updates
UPDATE Projects
SET    name = 'SmartAI'
WHERE  name = 'BigAI';

-- Deletes
DELETE FROM Projects
WHERE  name = 'BigAI';
```


#### Check Constraint
```sql
CREATE TABLE Projects (
  eid    INT,
  pname  TEXT,
  hours  INT CHECK (hours > 0),
  PRIMARY KEY (eid, pname)
);

-- Multiple Columns
CREATE TABLE Teams (
  name        TEXT PRIMARY KEY,
  start_year  INT,
  end_year    INT,
  CHECK (start_year <= end_year)
);


-- Complex Constraint
/* Create the Table "Teams" where the minimum hours for 'CoreOS' is at least 30 hours but there are no such restrictions for other projects. */

CREATE TABLE Projects (
  eid    INT,
  pname  TEXT,
  hours  INT CHECK (hours > 0),
  PRIMARY KEY (eid, pname),
  CHECK (
    (pname = 'CoreOS' AND hours >= 30)
    OR
    (pname <> 'CoreOS' AND hours > 0)
  )
);
```


## Summary
![[Pasted image 20230221175729.png]]


### Alter Table
```sql
ALTER TABLE <table_name>
	[ALTER / ADD / DROP] [COLUMN / CONSTRAINT] <name>
	<changes>;

--example
ALTER TABLE Projects ALTER COLUMN name TYPE VARCHAR(200);
ALTER TABLE Projects ALTER COLUMN start_year SET DEFAULT 2021;
ALTER TABLE Projects ALTER COLUMN name DROP DEFAULT;
```



