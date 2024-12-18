# Introduction to Database Systems

### Transactional data:
- **Structured data** created with an organization, with sizes ranging from gigabytes to terabytes. 
- **Transactional data** refers to structured data generated by day-to-day operations within an organization. This type of data typically involves records of transactions such as purchases, bookings, or customer interactions.

### Big data
Data generated by **multimedia applications** and internet of things.
Big data differs from transactional data in the following four ways:
- Volume: How much data at rest terabytes to exabytes
- Velocity: Data in motion / streaming data, milliseconds to seconds to respond
- Variety: Data in many forms, structured unstructed, text, multimedia 
- Veracity: Data in doubt or uncertainty due to data inconsistency  

### Examples of transactional data

The Ohio department of motor vehicles processes vehicle registrations, drivers licenses, and traffic violations for 26 million drivers. Assume each driver creates 4 transactions per year at 1000 bytes per transaction, on average, and 5 years of data are stored in a database.

**Bank Transactions**:
- A customer makes a payment or withdrawal from a bank account.
- Fields recorded might include:
    - Account Number
    - Transaction Date and Time
    - Transaction Amount
    - Transaction Type (Deposit, Withdrawal, Transfer)
    - Balance after Transaction
    
**Retail Sales**:
- When a customer buys products in a store, transactional data would include:
    - Purchase ID
    - Customer ID
    - Product ID
    - Quantity purchased
    - Price
    - Date and Time of Purchase
### Examples of big data 

Youtube users view approximately 4 million videos per minutes worldwide. Youtube tracks all views and information about video content to optimize advertising shown to each user. Assume youtube stores approximately 10,000 bytes per view annually.

**Social Media Data**
- **Description**: Platforms like Facebook, Twitter, Instagram, and LinkedIn generate vast amounts of data every second.
- **Components**:
    - **User Posts and Comments**: Text, images, videos, and other multimedia content.
    - **User Interactions**: Likes, shares, retweets, and reactions.
    - **Metadata**: Timestamps, geolocation data, and device information.
- **Use Cases**:
    - Sentiment analysis to gauge public opinion.
    - Targeted advertising based on user behavior and preferences.
    - Trend analysis to identify popular topics.
    
**Internet of Things (IoT) Data**
- **Description**: Devices connected to the internet, such as smart thermostats, wearable fitness trackers, and industrial sensors, continuously generate data.
- **Components**:
    - **Sensor Readings**: Temperature, humidity, motion, and other environmental metrics.
    - **Device Logs**: Operational data from machinery and equipment.
    - **User Interactions**: Data from smart home devices controlled by users.
- **Use Cases**:
    - Predictive maintenance in manufacturing to prevent equipment failures.
    - Smart city applications like traffic management and energy consumption optimization.
    - Health monitoring through wearable devices.

### Database systems
**Database**: A very large collection of interrelated data
Models a real-world enterprise:
- Entities/Objects
- Relationships
A **database management system** is a software system designed to store, manage, and facilitate access to databases.

### Why use databases
In the early days file systems were used but that have some drawbacks:
- Data redundancy
- Difficulty sorting and accessing data ( no api)
- Data isolation( no standard format) and lack of security 
- Integrity problems ( cannot control input data such as account > 0)
- Concurrency problems

So we use databases to solve some of those problems here are some advantages behind them:
- Data independence ( primary key / unique)
- Efficient data access
- Data integrity and security 
- Concurrent access, and crash recovery

But databases did also have some drawbacks such as:
- Expensive and complicated to maintain 
- They are not suited for special purpose tasks ( keyword search)

### Schemas 

A **schema** is the logical structure of the database
An **instance** is the actual content of the database

**Database** = collection of relationships / tables
**Relation schema** = relation name and attribute list. (Optionally data types)
**Database schema** = set of all relation relation schema in the database 

# SQL - Structured Query Language
SQL is designed for managing data held in a relational database management system. SQL consists of a **data definition language** and a **data manipulation language**.

**Two main components of SQL**:
1. Data Definition Language
	- This is for tables such as creating, altering or dropping
2. Data Manipulation Language 
	- This is for data such as insert, update, delete, and select

**Creating, Dropping, and adding a column to  a table**:
```
//Create table
CREATE TABLE <table_name> (<List of elements>);

//Delete table
DROP TABLE <table_name>;

//Add a column but not changing data
ALTER TABLE <table_name> ADD <column_name> datatype;
```

### Elements of table declarations

**Data types**
- INT or INTEGER
- REAL or FLOAT
- CHAR(n) - fixed length n
- VARCHAR(n) - variable length string up to n

**Any** value can be **NULL** 

**Declaring Keys** 
- Tables can have at most one primary key
- Can have more than one unique key
- No attribute of PRIMARY KEY can ever be NULL
- UNIQUE keys can have a NULL value

**Example of creating a table with a primary key** 
```
CREATE TABLE Beers (
	name CHAR(20) PRIMARY KEY,
	manf CHAR(20)
)
```

**Example of Multi-attribute Key**
```
CREATE TABLE Sells (
	bar CHAR(20),
	beer VARCHAR(20),
	price REAL,
	PRIMARY KEY (bar, beer)
)
```



# Relational Algebra

**Core Relational Algebra**
- **Selection**: Picking certain rows
- **Projection**: Picking certain columns
- **Products and joins**: Composition of relations
- **Renaming**: of relations and attributes
- **Union, intersection and difference**: Usual set operations, but both operands must have the same relational schema.


**Selection**:
- Picks certain rows

Example of selection:

| bar   | beer   | price |
|-------|--------|-------|
| Joe's | Bud    | 2.50  |
| Joe's | Miller | 2.75  |
| Sue's | Bud    | 2.50  |
| Sue's | Miller | 3.00  |

JoeMenue := σ_bar="Joe's"(Sells)

| bar   | beer   | price |
|-------|--------|-------|
| Joe's | Bud    | 2.50  |
| Joe's | Miller | 2.75  |


**Projection**:
- Projects the current query to pick out certain columns
- Eliminate duplicate tuples

Example of projection

| bar   | beer   | price |
|-------|--------|-------|
| Joe's | Bud    | 2.50  |
| Joe's | Miller | 2.75  |
| Sue's | Bud    | 2.50  |
| Sue's | Miller | 3.00  |

Prices := π_beer, price(Sells)

| beer   | price |
|--------|-------|
| Bud    | 2.50  |
| Miller | 2.75  |
| Miller | 3.00  |

**Product**:
- Not often used
- Pair each tuple from T1 with each tuple of T2

Example of product 
R1:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

R2:

| B | C  |
|---|----|
| 5 | 6  |
| 7 | 8  |
| 9 | 10 |

R3: (Result of R1 ⨯ R2)

| A | R1.B | R2.B | C  |
|---|------|------|----|
| 1 | 2    | 5    | 6  |
| 1 | 2    | 7    | 8  |
| 1 | 2    | 9    | 10 |
| 3 | 4    | 5    | 6  |
| 3 | 4    | 7    | 8  |
| 3 | 4    | 9    | 10 |

**Theta-join** 
- Take the product of R1 X R2 then apply selection to result
- Often natural join would be a better choice 

Example of Theta-join
Sells:

| bar   | beer   | price |
|-------|--------|-------|
| Joe's | Bud    | 2.50  |
| Joe's | Miller | 2.75  |
| Sue's | Bud    | 2.50  |
| Sue's | Coors  | 3.00  |

Bars:

| name   | addr        |
|--------|-------------|
| Joe's  | Maple St.   |
| Sue's  | River Rd.   |

BarInfo := Sells ⨝ Bars
*Join on Sells.bar = Bars.name*

BarInfo:

| bar   | beer   | price | name   | addr        |
|-------|--------|-------|--------|-------------|
| Joe's | Bud    | 2.50  | Joe's  | Maple St.   |
| Joe's | Miller | 2.75  | Joe's  | Maple St.   |
| Sue's | Bud    | 2.50  | Sue's  | River Rd.   |
| Sue's | Coors  | 3.00  | Sue's  | River Rd.   |

**Natural Join**:
- Equating attributes of the same name
- Projecting out one copy of each pair of equated attributes

Example of natural join:
Sells:

| bar   | beer    | price |
|-------|---------|-------|
| Joe's | Bud     | 2.50  |
| Joe's | Miller  | 2.75  |
| Sue's | Bud     | 2.50  |
| Sue's | Coors   | 3.00  |

Bars:

| bar    | addr        |
|--------|-------------|
| Joe's  | Maple St.   |
| Sue's  | River Rd.   |

BarInfo := Sells ⟕ Bars
*Left outer join (⟕) between Sells and Bars*

BarInfo:

| bar   | beer    | price | addr        |
|-------|---------|-------|-------------|
| Joe's | Bud     | 2.50  | Maple St.   |
| Joe's | Miller  | 2.75  | Maple St.   |
| Sue's | Bud     | 2.50  | River Rd.   |
| Sue's | Coors   | 3.00  | River Rd.   |

**Theta join vs natural join** 
The **natural join** (`R ⨝ S`) automatically joins two relations `R` and `S` by equating all attributes with the same name in both relations. It implicitly uses equality conditions for every pair of attributes with the same name, and it removes one copy of the duplicate attributes in the result.

On the other hand, the **theta-join** (`R ⨝_C S`) allows for an explicit join condition `C` to be specified. In this case, the condition is `R.A = S.A` for each attribute `A` that appears in both `R` and `S`. While this might seem the same as a natural join, the key difference is that the theta-join does not automatically remove duplicate attributes. Both attributes `R.A` and `S.A` will appear in the result unless explicitly projected away.

Summary of Differences:
- **Natural Join (`R ⨝ S`)**: Implicitly joins on attributes with the same name, removes duplicates.
- **Theta-Join (`R ⨝_C S`)**: Requires an explicit condition and does not remove duplicates unless specified.

**Renaming**
- Renames a table and attribute 

Example of Renaming
Bars:

| name   | addr        |
|--------|-------------|
| Joe's  | Maple St.   |
| Sue's  | River Rd.   |

R(bar, addr) := Bars

R:

| bar    | addr        |
|--------|-------------|
| Joe's  | Maple St.   |
| Sue's  | River Rd.   |


For **Union**, **Intersection**, and **difference** the schema of both sets must be the same

**Precedence of relational operators:**
1. [σ, π, ρ] (highest).
2. [⨯, ⨝].
3. ∩.
4. [∪, −].

### Relational Algebra vs SQL
 - Relational Algebra treats relations as sets (ie duplicates will never occur)
 - Duplicate elimination is explicit in SQL(Select Distinct)


# SQL 

**SQL** is a very-high-level language. In SQL you say how to do something rather then how to do it.

**Two main components of SQL**:
1. Data Definition Language
	- This is for tables such as creating, altering or dropping
2. Data Manipulation Language 
	- This is for data such as insert, update, delete, and select

### Table Creation and Manipulation 

- You can use the `CREATE` Keyword to make new tables
- You can **not** start table names with numbers and **can't** have spaces in names
- **Valid Table names** should be any alphanumeric combination that doesn't start with a digit

**Examples of valid table names**
- abc123
- _123abc
- abc-abc
- abc.abc

**You can create a table using**:
```
CREATE TABLE <tablename> 
( column_name     datatype,
	...,
)
```


**Common datatypes**
- Text
	- char(n) //fixed length n characters
	- varchar(n) //variable length up to n
	- clob
- Number
	- integer
	- float
	- numeric(n,m)
- Date
	- date
	- datetime
	- timestamp
- binary
	- varbinary(n) raw(n)
	- blob

**Common Constraints**
- `NOT NULL` - indicates that a column cannot store a NULL value
- `UNIQUE` - Ensure that each row for a column must have a unique value
- `PRIMARY KEY` - A combination of a NOT NULL and UNIQUE.
- `FOREIGN KEY` - Ensure that referential integrity of the data in one table to match values in another table.
- `CHECK` - Ensure that the value in a column meets a specific condition

**Example table with constraints**:
```
CREATE TABLE people (
	peopleid int PRIMARY KEY,
	first_name varchar(30) NOT NULL,
	surname varchar(30) NOT NULL,
	born numeric(4) NOT NULL,
	died numeric(4),
	country varchar(30),
	CHECK (born > 1950),
	foreign key (country) References countries(country_code)
)
```

**How to modify and alter tables**
- Tables can be changed using the keyword `ALTER`
	- Using `ALTER` you can `ADD` or `DROP` attributes of a table
- You can delete an entire table with the `DROP` keyword

**Examples of altering/deleting a table**
```
ALTER TABLE table_name  
	ADD CONSTRAINT MyPrimaryKey  
	PRIMARY KEY (column1, column2...);  
	
ALTER TABLE table_name  
	DROP CONSTRAINT MyPrimaryKey;  
	
ALTER TABLE table_name  
	ADD PRIMARY KEY (column1, column2...);
```


### Data Manipulation with a table 

- Three kinds of modifications
	- `INSERT` a tuple or tuples
	- `DELETE` a tuple or tuples
	- `UPDATE` the value(s) of an existing tuple or tuples

**Example of `INSERT`**
```
INSERT INTO Orders (order_id, order_date, customer_id, amount) VALUES (101, '2024-10-07', 1, 99.99);

INSERT INTO Customers (customer_id, customer_name, email)
VALUES 
(2, 'Jane Smith', 'janesmith@example.com'),
(3, 'Robert Brown', 'robertbrown@example.com');

```

If we don’t have values for all attributes, and then we want the system to fill in missing components with `NULL`

**Example of `UPDATE`**
```
UPDATE table_name SET <list of attribute assignments> WHERE <condition on tuples>;

UPDATE Students SET Major = ‘CS’ WHERE ID = ‘ab123’;

UPDATE Customers SET email = 'john.doe@newmail.com' WHERE customer_id = 1;

```


**Example of `Deletion`**
```
DELETE FROM table_name WHERE <condition>;

DELETE FROM Students WHERE Major = ‘CS’;

//deletes all rows in a table
DELETE FROM table_name;
```

### Select-From-Where statements
- `SELECT` desired attributes
- `FROM` one or more tables
- `WHERE` condition about tuples of the tables

**Steps to use**
- Begin with the relation in the FROM clause.  
- Apply the selection condition indicated by the WHERE clause.  
- Apply the extended projection indicated by the SELECT clause.

**Examples**
```
SELECT name FROM Beers WHERE manf = ’Anheuser-Busch’;

//you can also select the whole row
SELECT * FROM Beers WHERE manf = ’Anheuser-Busch’;

//renames the attribute name as beer in result
SELECT name AS beer, manf FROM Beers WHERE manf = ’Anheuser-Busch’;
```


**There are also more complex conditions for `WHERE` Clauses**
- Boolean operators AND, OR, NOT.  
- Comparisons =, <>, <, >, <=, >=.

**Example**
```
SELECT price FROM Sells WHERE bar = ’Joe’’s’ AND beer = ’Bud’;
```

### Other SQL Query keywords
##### **Like Keyword**
- Attribute LIKE pattern 
- Attribute NOT LIKE pattern
- **Pattern** is a quoted string with `%` which means "any string" and `_` means "any character" 

**Example of LIKE keyword**
```
SELECT name FROM Drinkers WHERE phone LIKE ’330 % ’;
```

##### **NULL Values**
- Tuples in SQL relations can have NULL as a value for one or more components
- Two main reasons
	- Missing value : e.g., we know Joe’s Bar has some address, but we don’t know what it is.  
	- Inapplicable : e.g., the value of attribute died for an alive person.
- `NULL` in SQL is not a value

**You cannot do** `where column_name = null`;, but you can `where column_name is null;` or `where column_name is not null;`

##### **Distinct keyword**
- Does not allow for duplicate results

**Example of Distinct**
```
/* Without DISTINCT, each price would be listed as many times as there were bar/beer pairs at that price */
SELECT DISTINCT price FROM Sells;
```

##### **Group by keyword**

- You can follow a select-from-where expression by a `GROUP BY` and a list of attributes
- The relation that results from the SELECT-FROM-WHERE  is grouped according to the values of all those attributes, and any aggregation is applied only within each group

**Example of `Group by`**
```
SELECT beer, AVG(price) AS average FROM Sells GROUP BY beer;
```

**Explanation of example**

Data from the `Sells` table:

|bar|beer|price|
|---|---|---|
|Joe's|Bud|5.00|
|Joe's|Heineken|7.00|
|Manny's|Bud|6.00|
|Manny's|Heineken|8.00|
|Manny's|Miller|7.00|
**Group 1 (Bud)**

|bar|beer|price|
|---|---|---|
|Joe's|Bud|5.00|
|Manny's|Bud|6.00|
 **Group 2 (Heineken)**

|bar|beer|price|
|---|---|---|
|Joe's|Heineken|7.00|
|Manny's|Heineken|8.00|
 **Group 3 (Miller)**

|bar|beer|price|
|---|---|---|
|Manny's|Miller|7.00|


#### Aggregations

- `SUM`: Returns the total sum of a numeric column. It adds all the values together.
- `AVG`: Calculates the average of a numeric column by dividing the sum by the number of values.
- `COUNT`: Counts the number of rows that match a specified condition or the total number of non-null entries in a column.
- `MIN`: Returns the smallest value from a specified column.
- `MAX`: Returns the largest value from a specified column.

**NULL’s Ignored in Aggregation** 
-  `NULL` never contributes to a sum, average, or count, and can never be the minimum or maximum of a column
- If there are no non-NULL values in a column, then the result of the aggregation is `NULL`

### Multi-Relational Queries
- Distinguish attributes of the same name by `table_name.attribute_name`

#### Joining two tables for a Query

##### 1. Inner Join

An **inner join** returns only those records that have matching values in both tables. It discards rows that do not meet the join condition.

**Syntax** 
`SELECT columns FROM table1 INNER JOIN table2 ON table1.column = table2.column;`

##### 2. Natural Join

A **natural join** is a type of inner join that automatically joins tables based on columns with the same name and data type in both tables. It eliminates the need to explicitly specify the condition.

**Syntax** 
`SELECT columns FROM table1 NATURAL JOIN table2;`

##### 4. Theta Join

A **theta join** is a join that uses a condition, typically with a comparison operator such as `=`, `<`, `>`, etc.

**Syntax**
`SELECT columns FROM table1 JOIN table2 ON condition;`

##### 6. Self Join

A **self join** is used to join a table with itself. This is useful for hierarchical data or finding relationships within the same table.

**Syntax** 
`SELECT A.columns, B.columns FROM table A JOIN table B ON A.column = B.column;`

##### 7. Outer left/right  Join
**information not filled in** 

#### Subqueries

