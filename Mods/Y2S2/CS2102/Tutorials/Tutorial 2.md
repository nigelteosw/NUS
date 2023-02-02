# Relational Algebra & SQL (Part 1)

## RA Operator

## SQL DDL
```sql
CREATE TABLE Offices {
office_id INTEGER PRIMARY KEY,
building TEXT,
floor INTEGER,
room_number INTEGER,
area INTEGER,
}

CREATE TABLE Employees {
	emp_id INTEGER PRIMARY KEY,
	name TEXT NOT NULL
	office_id INTEGER NOT NULL
		References offices ON UPDATE CASCADE
	manager_id INTEGER
		refferences manager_id ON UPDATE CASADE
}
```

## SQL DDL
### (a)
```sql
CREATE TABLE Books {
	isbn TEXT
	title TEXT NOT NULL
	authors TEXT NOT NULL
	
	PRIMARY KEY (isbn)
}

CREATE TABLE Customers {
	cust_id INTEGER
	name TEXT NOT NULL
	email TEXT NOT NULL
	PRIMARY KEY (cust_id)
}

CREATE TABLE Carts {

}

CREATE TABLE Purchase {


	FOREGING KEY (cust_id) REFERENCES 
}

CREATE TABLE Purchased_items {
	pid
	isbn TEXT
	PRIMARY KEY (pid, isbn)
}
```

### (b)
```sql

```

### (c)
1. Can be encoded 
2. Can be encoded (can only be done with `CHECK`)
3. Can be encoded (can only be done with `CHECK`)
4. Can be encoded (can only be done with `CHECK`)
	1. Check the publisher name, year then check the ebook