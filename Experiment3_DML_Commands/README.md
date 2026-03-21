# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a query to find the names of employees that begin with ‘S’ from EmployeeInfo table.

```sql
SELECT *
FROM EmployeeInfo
WHERE EmpFname LIKE 'S%';
```
**Output:**
<img width="1801" height="220" alt="image" src="https://github.com/user-attachments/assets/0b8cc685-6274-4d2e-bf97-fcb6ba654d25" />

**Question 2**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3 or surgeon ID is 4.

```sql
DELETE FROM Surgeries
WHERE surgery_id=3
OR surgery_id=4;
```
**Output:**
<img width="1189" height="808" alt="image" src="https://github.com/user-attachments/assets/5a9d5e78-9047-435f-8fe1-377fcd6005b6" />

**Question 3**
---
Write a SQL query to find all those customers who does not have any grade. Return customer_id, cust_name, city, grade, salesman_id.

```sql
SELECT customer_id,
       cust_name,
       city,
       grade,
       salesman_id
FROM customer
WHERE grade IS NULL;
```
**Output:**
<img width="1348" height="404" alt="image" src="https://github.com/user-attachments/assets/3ef3ae5c-65fc-4451-bb21-0bb16f3927fd" />

**Question 4**
---
Write a SQL query to calculate the discounted price for products where the discount percentage is greater than 0, and order the results by discounted_price in ascending order. Return product_id, original_price, discount_percentage, and discounted_price.

```sql
SELECT product_id,
original_price,
discount_percentage,
original_price - (original_price * discount_percentage) AS discounted_price
FROM Products
WHERE discount_percentage > 0
ORDER BY discounted_price ASC;
```
**Output:**
<img width="1381" height="271" alt="image" src="https://github.com/user-attachments/assets/cb6f5d3d-bacf-48cb-a072-2e0929cf1df2" />

**Question 5**
---
Write a SQL query to retrieve the details of all customers whose ID belongs to any of the values 3007, 3008 or 3009. Return customer_id, cust_name, city, grade, and salesman_id.

```sql
SELECT customer_id,
cust_name,
city,
grade,
salesman_id
FROM customer
WHERE customer_id IN (3007, 3008, 3009);
```
**Output:**
<img width="1316" height="371" alt="image" src="https://github.com/user-attachments/assets/919659f1-1d9d-4f83-b6d8-402da11e8260" />

**Question 6**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

```sql
DELETE FROM surgeries
WHERE surgery_id = 3;
```
**Output:**
<img width="1287" height="354" alt="image" src="https://github.com/user-attachments/assets/b8755380-c22d-48eb-bf00-46baf7716ca3" />

**Question 7**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

```sql
UPDATE products 
SET reorder_lvl=40
WHERE category='Grocery';
```
**Output:**
<img width="1828" height="377" alt="image" src="https://github.com/user-attachments/assets/f7d2124d-b778-4e88-9aba-cf275ef57739" />

**Question 8**
---
Write a SQL statement to display name and commission of first 5 salesmen.

```sql
SELECT name, commission
FROM salesman 
LIMIT 5;
```
**Output:**

<img width="810" height="559" alt="image" src="https://github.com/user-attachments/assets/29450019-0104-4858-b3b4-607e2491243d" />

**Question 9**
---
Write a SQL query to identify products where the discount amount is greater than $50. Return product_id, original_price, discount_percentage, and discount_amount.

```sql
SELECT product_id,
original_price,
discount_percentage,
original_price * discount_percentage AS discount_amount
FROM products
WHERE original_price  * discount_percentage > 50;
```
**Output:**
<img width="1337" height="230" alt="image" src="https://github.com/user-attachments/assets/aeb22600-169a-424e-b916-e4e12ce66c4f" />

**Question 10**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.

```sql
DELETE FROM customer
WHERE grade >= 2;
```
**Output:**

<img width="748" height="544" alt="image" src="https://github.com/user-attachments/assets/facf3b0a-a09b-4702-abc9-148a5c656d47" />

## MODULE 2 GRADE
<img width="1375" height="134" alt="image" src="https://github.com/user-attachments/assets/176906b1-d253-426c-9975-26ec0e8f8a87" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
