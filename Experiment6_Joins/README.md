# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

```sql
select p.first_name
from patients p
inner join surgeries s on p.patient_id=s.patient_id
where s.surgery_date='2024-01-15';
```
**Output:**

<img width="507" height="382" alt="image" src="https://github.com/user-attachments/assets/717cb963-5d07-41bf-8cf5-37c99916b4e3" />

**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers with the name 'Fabian Johns'.

```sql
SELECT s.*
FROM salesman s
LEFT JOIN customer c ON s.salesman_id= c.salesman_id
WHERE c.cust_name = 'Fabian Johns';
```
**Output:**

<img width="1205" height="348" alt="image" src="https://github.com/user-attachments/assets/1fc464aa-4d4c-4165-9011-9dda4de66e75" />

**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

```sql
SELECT 
    p.first_name,
    s.*
FROM 
    patients p
INNER JOIN 
    surgeries s ON p.patient_id = s.patient_id
WHERE 
    p.date_of_birth > '1990-01-01';
```
**Output:**

<img width="1254" height="328" alt="image" src="https://github.com/user-attachments/assets/09df564a-7175-43ac-a5c5-79ef630ea88f" />

**Question 4**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman_id values that have more than one associated customer.

```sql
SELECT s.name, c.cust_name, c.city, c.grade, c.salesman_id
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE s.salesman_id IN (
SELECT salesman_id
FROM customer
GROUP BY salesman_id
HAVING COUNT(*)>1
);
```
**Output:**

<img width="1248" height="505" alt="image" src="https://github.com/user-attachments/assets/a6905578-86b5-4193-b71b-3e342d2968c3" />

**Question 5**
---
Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.

```sql
SELECT c.cust_name,
       c.city,
       o.ord_no,
       o.ord_date,
       o.purch_amt
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE c.city = 'London';
```
**Output:**

<img width="1331" height="391" alt="image" src="https://github.com/user-attachments/assets/9a6a8b1e-5f54-4d9f-aa34-921d9e97d1b6" />

**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

```sql
SELECT n.*, d.department_name
FROM nurses n
INNER JOIN departments d ON n.department_id = d.department_id;
```
**Output:**

<img width="1393" height="450" alt="image" src="https://github.com/user-attachments/assets/27def990-94bd-4db6-b014-68977183fb38" />

**Question 7**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

```sql
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM 
    patients AS p
INNER JOIN 
    doctors AS d ON p.doctor_id = d.doctor_id
WHERE 
    p.discharge_date IS NULL;
```
**Output:**

<img width="746" height="413" alt="image" src="https://github.com/user-attachments/assets/24fc80d5-439b-4578-841d-25b758a4ab3d" />

**Question 8**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

```sql
SELECT p.first_name AS patient_name,
t.test_name
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id;
```
**Output:**

<img width="736" height="477" alt="image" src="https://github.com/user-attachments/assets/1236261e-8e7b-4e34-b5c4-0da070362301" />

**Question 9**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

```sql
SELECT c.cust_name, s.commission
FROM customer c
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id;
```
**Output:**

<img width="773" height="802" alt="image" src="https://github.com/user-attachments/assets/b75ab3d4-0d71-43c0-bd44-c5bf695d40fc" />

**Question 10**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

```sql
select p.date_of_birth, a.appointment_id, p.patient_id, p.doctor_id, a.appointment_date
from patients p
inner join appointments as a on p.patient_id= a.patient_id
where p.first_name='Alice';
```
**Output:**

<img width="1609" height="378" alt="image" src="https://github.com/user-attachments/assets/05d313a8-22db-4843-86a1-2f71d8efa18f" />

## MODULE 5 GRADE
<img width="1333" height="125" alt="image" src="https://github.com/user-attachments/assets/ad2c9cd6-faf8-45e6-b03f-1ad8d88fba67" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
