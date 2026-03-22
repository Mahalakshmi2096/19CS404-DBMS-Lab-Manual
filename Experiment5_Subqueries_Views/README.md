# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

```sql
SELECT *
FROM Employee
WHERE age < (
  SELECT AVG(age)
  FROM Employee
  WHERE income > 1000000
);
```
**Output:**

<img width="1219" height="368" alt="image" src="https://github.com/user-attachments/assets/5ad654ce-2d94-4d80-a04c-922b8defbc22" />

**Question 2**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

```sql
SELECT *
FROM Medications
WHERE dosage = (
SELECT MAX(dosage)
FROM Medications
);
```
**Output:**

<img width="931" height="380" alt="image" src="https://github.com/user-attachments/assets/4a1a95ff-d690-44f0-b207-ba3cefa17053" />

**Question 3**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

```sql
SELECT  ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
SELECT AVG(purch_amt)
FROM orders
WHERE ord_date='2012-10-10'
);
```
**Output:**

<img width="1207" height="399" alt="image" src="https://github.com/user-attachments/assets/bf7ae5f7-79c5-484a-be7a-c911a8d556c2" />

**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

```sql
SELECT ID, NAME, AGE, ADDRESS, SALARY
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi' 
AND AGE < 30
ORDER BY ID ASC;
```
**Output:**

<img width="1144" height="299" alt="image" src="https://github.com/user-attachments/assets/9f19c6f9-b248-41f8-8afa-d20d3a3d535c" />

**Question 5**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

```sql
SELECT name, city
FROM customer
WHERE city IN (SELECT city FROM customer WHERE id IN (3,7));
```
**Output:**

<img width="622" height="388" alt="image" src="https://github.com/user-attachments/assets/67c45af3-5806-4a6c-b232-252d69cb0351" />

**Question 6**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

```sql
SELECT *
FROM GRADES 
WHERE (subject,grade) IN (
   SELECT subject, MIN(grade)
   FROM GRADES
   GROUP BY subject
);
```
**Output:**

<img width="1239" height="371" alt="image" src="https://github.com/user-attachments/assets/7d505a7b-b6d1-4a15-97c1-c7f7ff4c0b6e" />

**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```
**Output:**

<img width="1146" height="522" alt="image" src="https://github.com/user-attachments/assets/fc1c637c-ee83-4291-9055-0b2b2d15b6bd" />

**Question 8**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

```sql
SELECT grade, COUNT(*)
FROM customer
WHERE grade > (
SELECT AVG(grade)
FROM customer
WHERE city ='New York'
)
GROUP BY grade;
```
**Output:**

<img width="646" height="282" alt="image" src="https://github.com/user-attachments/assets/ee849ff7-f4b3-42ca-ab53-c8e8e59f7f80" />

**Question 9**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

```sql
SELECT student_name, grade
FROM GRADES
WHERE (subject,grade) IN (
SELECT subject, MIN(grade)
FROM GRADES
GROUP BY subject
);
```
**Output:**

<img width="748" height="374" alt="image" src="https://github.com/user-attachments/assets/b01a89e2-5078-48ec-8316-f210eea4056c" />

**Question 10**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

```sql
SELECT o.ord_no,
       o.purch_amt,
       o.ord_date,
       o.customer_id,
       o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```
**Output:**

<img width="1150" height="411" alt="image" src="https://github.com/user-attachments/assets/a856defb-fd2f-4a68-8bbc-8c487271b499" />

## MODULE 4 GRADE

<img width="1341" height="132" alt="image" src="https://github.com/user-attachments/assets/071f75dd-86da-4a9c-aacb-16351231b8c4" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
