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
	emp_id INTEGER,
	name TEXT NOT NULL,
	office_id INTEGER NOT NULL,
	manager_id INTEGER,
	PRIMARY KEY (emp_id),
	FOREIGN KEY (office_id) REFERENCES Offices (office_id) ON UPDATE CASCADE,
	FOREIGN KEY (manager_id) REFERENCES Employees (emp_id) ON UPDATE CASCADE
);
```


### SQL DDL
```sql
DROP TABLE IF EXISTS 
	Books , Customers , Carts , Purchase , Purchased_items CASCADE;

CREATE TABLE Books (
	isbn INTEGER
	title TEXT NOT NULL,
	authors TEXT NOT NULL,
	year INTEGER,
	edition TEXT NOT NULL
		CHECK (edition in ('hardcopy', 'paperback', 'ebook')),
	publisher TEXT,
	number_pages INTEGER CHECK (number_pages > 0,
	price INTEGER NOT NULL CHECK (price > 0),
	PRIMARY KEY (isbn)
	
);

CREATE TABLE Customers (
	cust_id INTEGER,
	name TEXT NOT NULL,
	email TEXT,
	PRIMARY KEY (cust_id)
);

CREATE TABLE Carts (
	cust_id INTEGER,
	isbn INTEGER,
	PRIMARY KEY (cust_id, isbn),
	FOREGIN KEY (cust_id) REFERENCES Customers,
	FOREIGN KEY (isbn) REFERENCES Books
);

CREATE TABLE Purchase (
	pid INTEGER,
	purchase_date DATE NOT NULL,
	cust_id INTEGER NOT NULL,
	PRIMARY KEY (pid),
	FOREIGN KEY (cust_id) REFERENCES CUSTOMERS
);

CREATE TABLE Purchased_items (
	pid INTEGER,
	isbn INTEGER,
	PRIMARY KEY (pid, isbn),
	FOREIGN KEY (pid) REFERENCES Purchase,
	FOREIGN KEY (isbn) REFERENCES Books
);

-- b)
CREATE TABLE Purchase (
	pid INTEGER,
	purchase_timestamp DATE NOT NULL,
	cust_id INTEGER NOT NULL,
	PRIMARY KEY (pid),
	FOREIGN KEY (cust_id) REFERENCES CUSTOMERS,
	UNIQUE (purchase_timestamp, cust_id)
);
```

#### c) 
1. Can be expressed using a table constraint
- `CHECK ((edition <> 'hardcover') OR (price >= 30))`
2. Cannot be expressed
3. Can be expressed
- `CHECK ((number_pages > 1000) OR (edition = 'ebook') OR (price >= 100))`
4. Can be expressed
- `CHECK ((publisher <> ’Acme’) OR (year < 2010) OR (edition = ’ebook’))`

