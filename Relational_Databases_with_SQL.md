
```md
# SQL Notes

## Data Definition Language (DDL)

Learn SQL commands to define the structure of a database table and how to apply data types and constraints to columns.

```sql
CREATE TABLE employees (
	employee_id INT,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	hourly_pay DECIMAL(5,2),
	hire_date DATE
);
```
- Create a new table.

```sql
SELECT * FROM employees;
```
- Retrieve all data from the `employees` table.

```sql
RENAME TABLE employees TO workers;
```
- Rename the table from `employees` to `workers`.

```sql
DROP TABLE employees;
```
- Drop the `employees` table.

```sql
ALTER TABLE employees 
ADD phone_number VARCHAR(15);
```
- Add a `phone_number` column to the `employees` table.

```sql
RENAME COLUMN phone_number TO email;
```
- Rename the column `phone_number` to `email`.

```sql
MODIFY COLUMN email VARCHAR(100)  
AFTER last_name;
```
- Modify the `email` column to appear after the `last_name` column.

```sql
FIRST; 
```
- Move the column to be the first in the table.

```sql
DROP COLUMN email;
```
- Drop the `email` column from the table.

```sql
TRUNCATE TABLE employees;
```
- Truncate the `employees` table (delete all data, but keep the structure).

---

## Data Manipulation Language (DML)

Learn how to use SQL commands `INSERT`, `UPDATE`, and `DELETE` to manipulate data in a database.

```sql
INSERT INTO employees 
VALUES (1, 'Fahd', 'Mekawy', 50.0, '2022-07-19');
```
- Insert a new row into the `employees` table.

```sql
INSERT INTO employees 
VALUES (1, 'Fahd', 'Mekawy', 50.0, '2022-07-19'), 
       (2, 'Mohamed', 'Ahmed', 50.0, '2020-07-19');
```
- Insert multiple rows into the `employees` table.

```sql
INSERT INTO employees (employee_id, first_name, last_name) 
VALUES (1, 'Fahd', 'Mekawy');
```
- Insert specific columns in the `employees` table.

```sql
UPDATE employees
SET hourly_pay = 10.25;
```
- Update all rows in the `employees` table.

```sql
UPDATE employees
SET hourly_pay = 10.25, hire_date = '2020-02-12' 
WHERE employee_id = 6;
```
- Update specific rows in the `employees` table.

```sql
DELETE FROM employees 
WHERE employee_id = 6;
```
- Delete specific rows in the `employees` table.

---

## Data Query Language (DQL)

Introduction to data query language (DQL) for retrieving and viewing data from one, or multiple, tables. Learn how to filter data using the `WHERE` clause and how to apply conditions using operators in SQL.

```sql
SELECT first_name, last_name FROM employees;
```
- Select specific columns from the `employees` table.

```sql
SELECT DISTINCT hire_date FROM employees;
```
- Select distinct hire dates from the `employees` table.

```sql
SELECT email AS email_address, phone_number AS mobile_number FROM employees;
```
- Rename columns in the result set.

```sql
SELECT hourly_pay * 3 AS per FROM employees;
```
- Perform arithmetic operations in the `SELECT` statement.

```sql
SELECT first_name FROM employees ORDER BY first_name;
```
- Order the result set by `first_name`.

```sql
SELECT DISTINCT first_name FROM employees ORDER BY first_name;
```
- Select distinct first names and order them.

```sql
SELECT first_name FROM employees GROUP BY first_name ORDER BY first_name;
```
- Group by and order the result set.

```sql
SELECT COUNT(employee_id) AS "# of people",
       COUNT(DISTINCT employee_id) AS "# of district primary key values",
       COUNT(first_name) AS "# of people with non-NULL first names",
       COUNT(DISTINCT first_name) AS "# of distinct first names"
FROM employees;
```
- Use `COUNT` with different conditions.

---

### Comparison Operators

```sql
SELECT * FROM employees WHERE hourly_pay = 50;
SELECT * FROM employees WHERE hourly_pay > 60;
SELECT * FROM employees WHERE hourly_pay < 40;
SELECT * FROM employees WHERE hourly_pay >= 80;
SELECT * FROM employees WHERE hourly_pay <= 30;
SELECT * FROM employees WHERE hourly_pay <> 70;
```
- Comparison operations in SQL.

---

### Arithmetic Operators

```sql
SELECT employee_id, first_name, hourly_pay, hourly_pay + 100 AS "hourly_pay + 100" 
FROM employees;
```
- Perform arithmetic operations on columns.

---

### Logical Operators

```sql
SELECT * FROM employees WHERE first_name = 'Fahd' AND hourly_pay > 50;
SELECT * FROM employees WHERE first_name = 'Fahd' OR hourly_pay > 50;
SELECT * FROM employees WHERE NOT hourly_pay > 50;
```
- Logical operators: `AND`, `OR`, `NOT`.

---

### BETWEEN Operator

```sql
SELECT * FROM employees WHERE hourly_pay BETWEEN 50 AND 60;
```
- Use `BETWEEN` to filter rows within a range.

---

### IN, NOT IN Operators

```sql
SELECT first_name FROM employees WHERE first_name IN ('Fahd', 'Mekawy', 'Mohamed');
SELECT first_name FROM employees WHERE first_name NOT IN ('Fahd', 'Mekawy', 'Mohamed');
```
- Use `IN` and `NOT IN` to filter rows.

---

### LIKE Operator

```sql
SELECT * FROM employees WHERE first_name LIKE 'F%';
SELECT * FROM employees WHERE first_name LIKE 'F%D';
SELECT * FROM employees WHERE first_name LIKE '%AH%';
SELECT * FROM employees WHERE first_name LIKE '_ahd';
SELECT * FROM employees WHERE first_name LIKE '__hd';
```
- Use `LIKE` for pattern matching in SQL.

---

### ORDER BY and LIMIT

```sql
SELECT * FROM employees ORDER BY first_name DESC;
SELECT * FROM employees ORDER BY first_name DESC, last_name;
SELECT * FROM employees LIMIT 5;
SELECT * FROM employees ORDER BY first_name LIMIT 5;
```
- Order the result set and limit the number of rows returned.

---

### GROUP BY

```sql
SELECT SUM(hourly_pay), hire_date FROM employees GROUP BY hire_date;
SELECT MIN(hourly_pay), hire_date FROM employees GROUP BY hire_date;
SELECT MAX(hourly_pay), hire_date FROM employees GROUP BY hire_date;
SELECT AVG(hourly_pay), hire_date FROM employees GROUP BY hire_date;
SELECT COUNT(hourly_pay), hire_date FROM employees GROUP BY hire_date;
SELECT COUNT(hourly_pay), hire_date FROM employees GROUP BY hire_date HAVING COUNT(hourly_pay) > 1;
SELECT COUNT(hourly_pay), hire_date FROM employees GROUP BY hire_date HAVING COUNT(hourly_pay) > 1 AND employee_id IS NOT NULL;
```
- Group the result set by columns and apply aggregate functions.

---

### UNION and UNION ALL

```sql
SELECT * FROM employees UNION SELECT * FROM students;
SELECT * FROM employees UNION ALL SELECT * FROM students;
```
- Combine the result sets of two `SELECT` queries using `UNION` and `UNION ALL`.
```
