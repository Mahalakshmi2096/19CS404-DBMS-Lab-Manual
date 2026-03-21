 # Experiment 2: DDL Commands

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
--
Create a table named Attendance with the following constraints:
1. AttendanceID as INTEGER should be the primary key.
2. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
3. AttendanceDate as DATE.
4. Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK(Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```
**Output:**
<img width="1808" height="217" alt="image" src="https://github.com/user-attachments/assets/d0eed6f7-0fb6-4f5d-a1a8-42a971dacf99" />

**Question 2**
---
Create a table named Tasks with the following columns:
1. TaskID as INTEGER
2. TaskName as TEXT
3. DueDate as DATE

```sql
CREATE TABLE Tasks (
    TaskID INTEGER,
    TaskName TEXT,
    DueDate DATE
);
```
**Output:**
<img width="1844" height="342" alt="image" src="https://github.com/user-attachments/assets/b36bd59c-b09a-4b7e-9e56-5dd5fdb2fc6d" />

**Question 3**
---
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY  

1                Ramesh           32   Ahmedabad   2000

2                Khilan           25   Delhi       1500

3                Kaushik          23   Kota        2000

```sql
INSERT INTO Customers (ID, NAME, AGE, ADDRESS, SALARY) VALUES
(1, 'Ramesh', 32, 'Ahmedabad', 2000),
(2, 'Khilan', 25, 'Delhi', 1500),
(3, 'Kaushik', 23, 'Kota', 2000);
```
**Output:**
<img width="1335" height="231" alt="image" src="https://github.com/user-attachments/assets/44b7c3dc-35b3-4fc8-b740-dd9d2cdeda94" />

**Question 4**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS

205         Olivia Green    F

207         Liam Smith      M           Mathematics  85

208         Sophia Johnson  F           Science

```sql
INSERT INTO student_details (RollNo, Name, Gender, Subject, Marks) VALUES
(205, 'Olivia Green', 'F', NULL, NULL),
(207, 'Liam Smith', 'M', 'Mathematics', 85),
(208, 'Sophia Johnson', 'F', 'Science', NULL);
```
**Output:**
<img width="1567" height="256" alt="image" src="https://github.com/user-attachments/assets/84e17e99-8171-487d-9d96-642b7267d5ff" />

**Question 5**
---
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

```sql
ALTER TABLE student_details
ADD COLUMN Mobilenumber number;
```
**Output:**
<img width="1627" height="334" alt="image" src="https://github.com/user-attachments/assets/5e8d3739-44a3-4628-a933-226ccc2c263d" />

**Question 6**
---
Write a SQL query to Add a new column State as text in the Student_details table.

```sql
ALTER TABLE student_details
ADD COLUMN State TEXT;
```
**Output:**
<img width="1623" height="343" alt="image" src="https://github.com/user-attachments/assets/4774378d-1fe1-445f-91f1-a55350b1257f" />

**Question 7**
---
Create a table named Orders with the following constraints:
1. OrderID as INTEGER should be the primary key.
2. OrderDate as DATE should be not NULL.
3. CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders(
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
**Output:**
<img width="1823" height="236" alt="image" src="https://github.com/user-attachments/assets/7574f79a-ce87-4c1c-b406-4a8a110b62ff" />

**Question 8**
---
Create a table named Products with the following constraints:
1. ProductID should be the primary key.
2. ProductName should be NOT NULL.
3. Price is of real datatype and should be greater than 0.
4. Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products(
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT NOT NULL,
    Price REAL CHECK (Price>0),
    Stock INTEGER CHECK (Stock>=0)
);
```
**Output:**
<img width="1590" height="270" alt="image" src="https://github.com/user-attachments/assets/e0127d4e-ea82-46fd-bc6d-0496c6b0ee6c" />

**Question 9**
---
Create a table named Employees with the following columns:
1. EmployeeID as INTEGER
2. FirstName as TEXT
3. LastName as TEXT
4. HireDate as DATE

```sql
CREATE TABLE Employees (
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);
```
**Output:**
<img width="1622" height="319" alt="image" src="https://github.com/user-attachments/assets/4385bbc6-0777-4245-8383-2080ebffe95a" />

**Question 10**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers
SELECT CustomerID, Name, Address, Email
FROM Old_Customers;
```
**Output:**
<img width="1722" height="308" alt="image" src="https://github.com/user-attachments/assets/c8388042-e3f6-4207-8b6c-8032fbc2316b" />

## MODULE 1 GRADE
<img width="1407" height="137" alt="image" src="https://github.com/user-attachments/assets/f960c194-3719-4e61-9405-72803ade0e41" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
