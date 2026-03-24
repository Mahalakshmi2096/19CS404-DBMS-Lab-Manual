# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Program:**
```
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);
```
```
CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY,
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_date DATE
);
```
```
CREATE OR REPLACE TRIGGER trg_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log(emp_id, emp_name, salary, log_date)
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/
```
```
INSERT INTO employees VALUES (1, 'Arun', 5000);
COMMIT;

SELECT * FROM employee_log;
```
**Expected Output:** 

<img width="1183" height="714" alt="image" src="https://github.com/user-attachments/assets/d14fb5ba-04c7-4db6-8c8b-758e58c7c8b9" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program:**
```
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    data VARCHAR2(100)
);
```
```
INSERT INTO sensitive_data VALUES (1, 'Confidential Record 1');
INSERT INTO sensitive_data VALUES (2, 'Confidential Record 2');

COMMIT;
```
```
CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'Deletion is not allowed on sensitive_data table!');
END;
/
```
```
DELETE FROM sensitive_data WHERE id = 1;
```
**Expected Output:**

<img width="1081" height="740" alt="image" src="https://github.com/user-attachments/assets/b043ecea-976b-4ef1-addd-d228d3187205" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program:**
```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);
```
```
INSERT INTO products VALUES (1, 'Laptop', 50000, NULL);
INSERT INTO products VALUES (2, 'Mobile', 20000, NULL);

COMMIT;
```
```
CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
```
```
UPDATE products
SET price = 55000
WHERE product_id = 1;
```
```
SELECT * FROM products;
```
**Expected Output:**

<img width="1069" height="727" alt="image" src="https://github.com/user-attachments/assets/78734199-4cff-4446-a74e-3793d161a975" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program:**
```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    amount NUMBER
);
```
```
CREATE TABLE audit_log (
    update_count NUMBER
);
INSERT INTO audit_log VALUES (0);
COMMIT;
```
```
CREATE OR REPLACE TRIGGER trg_update_counter
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/
```
```
-- Insert sample data
INSERT INTO customer_orders VALUES (1, 'Arun', 5000);
INSERT INTO customer_orders VALUES (2, 'Ramya', 7000);
COMMIT;

-- Perform updates
UPDATE customer_orders SET amount = 6000 WHERE order_id = 1;
UPDATE customer_orders SET amount = 8000 WHERE order_id = 2;
COMMIT;
```
```
SELECT * FROM audit_log;
```
**Expected Output:**

<img width="1035" height="736" alt="image" src="https://github.com/user-attachments/assets/a74fd873-d78f-442a-a877-8e00764742fd" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program:**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);
```
```
CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary <= 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'Salary must be greater than 3000!'
        );
    END IF;
END;
/
```
```
INSERT INTO employees VALUES (1, 'Arun','Manager', 5000,04);
```
```
INSERT INTO employees VALUES (2, 'Ramya','Analyst', 2000,05);
```
**Expected Output:**

<img width="1059" height="731" alt="image" src="https://github.com/user-attachments/assets/303e2cf6-47ef-48f6-941d-8cf7dd02b1fb" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
