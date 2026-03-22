# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

```sql
SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```
**Output:**

<img width="459" height="291" alt="image" src="https://github.com/user-attachments/assets/25470ac3-dfa7-41b4-a5b3-bac20033a5e6" />

**Question 2**
---
Write a SQL query to find  how many employees work in California?

```sql
SELECT COUNT(*) AS employees_in_california
FROM employee
WHERE city='California';
```
**Output:**

<img width="645" height="294" alt="image" src="https://github.com/user-attachments/assets/fe28d9e1-2d2d-4ed9-a9ec-01d09fec44a8" />

**Question 3**
---
Write a SQL query to find the customer with longest name?

```sql
SELECT name, LENGTH(name) AS length
FROM Customer
ORDER BY LENGTH(name) DESC
LIMIT 1;
```
**Output:**

<img width="660" height="296" alt="image" src="https://github.com/user-attachments/assets/37ae4003-7576-45d0-bcb6-398ee2e2b1e0" />

**Question 4**
---
How many medical records were created in each month?

```sql
SELECT
  strftime('%Y-%m', date) AS Month,
  COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY strftime('%Y-%m', date)
ORDER BY Month;
```
**Output:**

<img width="642" height="421" alt="image" src="https://github.com/user-attachments/assets/3d1e7840-7001-4467-a487-628b0b0c43ee" />

**Question 5**
---
How many doctors specialize in each medical specialty?

```sql
SELECT
   specialty AS Specialty,
   COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY specialty
ORDER BY specialty;
```
**Output:**

<img width="810" height="658" alt="image" src="https://github.com/user-attachments/assets/d1b337ed-abaf-4267-9522-849ca42f09d1" />

**Question 6**
---
What is the total number of appointments scheduled for each day?

```sql
SELECT 
   DATE(AppointmentDateTime) AS AppointmentDate,
   COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY AppointmentDate;
```
**Output:**

<img width="874" height="637" alt="image" src="https://github.com/user-attachments/assets/a85d726c-7ad7-4414-9889-de759dd3782e" />

**Question 7**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

```sql
SELECT 
  (age / 5) * 5 AS age_group,
  MAX(salary)
FROM customer1
GROUP BY (age / 5) * 5
HAVING MAX(salary) > 8000
ORDER BY age_group;
```
**Output:**

<img width="677" height="343" alt="image" src="https://github.com/user-attachments/assets/e12787c6-363c-4d24-8a00-4686bd3f2697" />

**Question 8**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

```sql
SELECT
  category_id,
  count(product_name)
FROM products
GROUP BY category_id
HAVING MIN(category_id) < 3
ORDER BY category_id;
```
**Output:**

<img width="787" height="344" alt="image" src="https://github.com/user-attachments/assets/0e01066a-31a6-4700-a81c-cc88d563b551" />

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

```sql
SELECT
   (age/5)*5 AS age_group,
   MIN(age)
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(age) < 25
ORDER BY age_group;
```
**Output:**

<img width="633" height="288" alt="image" src="https://github.com/user-attachments/assets/2f004268-7e96-413f-bf67-5bb775718971" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

```sql
SELECT 
  age,
  MAX(income)
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000
ORDER BY age;
```
**Output:**

<img width="685" height="347" alt="image" src="https://github.com/user-attachments/assets/63fbb030-c5d9-4af3-9730-71e1fad0d076" />

## MODULE 3 GRADE 

<img width="1393" height="152" alt="image" src="https://github.com/user-attachments/assets/46917cfb-b674-4d0d-bbb0-a35d76158aae" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
