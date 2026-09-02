# EXPERIMENT 2: DDL Commands
## NAME : NISHANTH J
## REGISTRATION  NUMBER : 212223100040
## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
```sql
INSERT INTO Books(ISBN,Title,Author)
VALUES('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**

<img width="1288" height="885" alt="image" src="https://github.com/user-attachments/assets/30df37fb-49a4-4842-a7da-43c804e057e5" />



**Question 2**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'
For example:

Test	Result
pragma table_info('books');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           book_id     INT         0                       1
1           title       VARCHAR(15  0                       0
2           author      VARCHAR(10  0                       0
3           genre       VARCHAR(50  0                       0
4           publicatio  INT         0                       0
5           ISBN        varchar(30  0                       0
6           domain_dep  varchar(30  0                       0

```sql
ALTER TABLE books
ADD  ISBN varchar(30) ;
ALTER TABLE books
ADD domain_dept  varchar(30);
```

**Output:**

<img width="1294" height="909" alt="image" src="https://github.com/user-attachments/assets/3d65bd4e-4651-4a32-afbd-673a3b95b49a" />



**Question 3**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT
For example:

Test	Result
pragma table_info('Locations');
cid       name             type        notnull     dflt_value  pk
--------  ---------------  ----------  ----------  ----------  ----------
0         LocationID       INTEGER     0                       0
1         LocationName     TEXT        0                       0
2         Address          TEXT        0                       0

```sql
CREATE TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT);
```

**Output:**

<img width="1308" height="887" alt="image" src="https://github.com/user-attachments/assets/29c3121e-80cd-4995-b831-b01e2780cec3" />


**Question 4**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
For example:

Test	Result
INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;
BonusID     EmployeeID  BonusAmount  BonusDate   Reason
----------  ----------  -----------  ----------  -----------------------
1           6           1000.0       2024-08-01  Outstanding performance

```sql
CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
BonusAmount REAL  CHECK(BonusAmount>0),
BonusDate DATE,
Reason TEXT NOT NULL
);
```

**Output:**

<img width="1298" height="920" alt="image" src="https://github.com/user-attachments/assets/49e4be8b-a2be-4c28-8458-a95bae066e70" />


**Question 5**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0
```sql
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL CHECK((list_price>=discount) and (list_price>=0)),
discount DECIMAL(10,2) DEFAULT 0 NOT NULL CHECK(discount>=0));
```

**Output:**

<img width="1329" height="855" alt="image" src="https://github.com/user-attachments/assets/686e759d-f42c-43d4-820f-d6f09675f9a0" />


**Question 6**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'
For example:

Test	Result
INSERT INTO Student_details (RollNo, Name, Gender, Subject, email) 
VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');
select * from Student_details;
RollN  Name   Gen  Subject     email
-----  -----  ---  ----------  ----------------
1      John   M    Math        john@example.com

```sql
ALTER TABLE Student_details
ADD email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**

<img width="1265" height="824" alt="image" src="https://github.com/user-attachments/assets/4c0dd3e5-95ed-4961-b95b-880bd24fe06c" />


**Question 7**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

For example:

Test	Result
SELECT * FROM Products WHERE ProductID = 101;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
101         Laptop      Electronics  1500        50
```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)VALUES(101,'Laptop','Electronics','1500','50');
```

**Output:**

<img width="1295" height="817" alt="image" src="https://github.com/user-attachments/assets/e67f28cb-7b4c-41a3-b67d-6a84c06528bc" />


**Question 8**
---
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.

```sql
insert into Employee(EmployeeID,Name,Position)
values(4,"Emily White","Analyst");
```

**Output:**

<img width="1000" height="800" alt="Screenshot 2026-02-02 133335" src="https://github.com/user-attachments/assets/f38ab02a-cca3-4d70-8a78-1b6683cf4afb" />


**Question 9**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Invoices(
InvoiceID integer primary key,
InvoiceDate fate,
Amount real check(Amount>0),
DueDate date check(DueDate>InvoiceDate),
OrderID integer,
foreign key (OrderID) references Orders(OrderID));
```

**Output:**

<img width="1000" height="800" alt="Screenshot 2026-02-02 133352" src="https://github.com/user-attachments/assets/07bd96b8-74af-472d-a046-d4f116892683" />


**Question 10**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
insert into Books select * from Out_of_print_books
```

**Output:**

<img width="1000" height="800" alt="Screenshot 2026-02-02 133405" src="https://github.com/user-attachments/assets/ae821cc6-4f05-4959-98a2-9025fca057c6" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

