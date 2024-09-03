```markdown
# SQL Notes

## Data Definition Language (DDL)

Learn SQL commands to define the structure of a database table, apply data types, and set constraints on columns.

### Create a New Table
```sql
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hourly_pay DECIMAL(5,2),
    hire_date DATE
);
```

### View All Data in a Table
```sql
SELECT * FROM employees;
```

### Rename a Table
```sql
RENAME TABLE employees TO workers;
```

### Drop a Table (Delete the Table Completely)
```sql
DROP TABLE employees;
```

### Alter a Table Structure
```sql
ALTER TABLE employees
ADD phone_number VARCHAR(15);  -- Add a new column
```

### Rename a Column
```sql
RENAME COLUMN phone_number TO email;
```

### Modify a Column’s Data Type
```sql
ALTER TABLE employees
MODIFY COLUMN email VARCHAR(100);
```

### Reallocate Column Position
```sql
ALTER TABLE employees
MODIFY COLUMN email VARCHAR(100) AFTER last_name;  -- Move after last_name
ALTER TABLE employees
MODIFY COLUMN email VARCHAR(100) FIRST;  -- Move to the first position
```

### Drop a Column
```sql
ALTER TABLE employees
DROP COLUMN email;
```

### Truncate a Table (Delete Data, Keep Structure)
```sql
TRUNCATE TABLE employees;
```

## Data Manipulation Language (DML)

Learn how to use SQL commands to manipulate data in a database.

### Insert Data into a Table
```sql
INSERT INTO employees 
VALUES (1, 'Fahd', 'Mekawy', 50.0, '2022-07-19');
```

### Insert Multiple Rows into a Table
```sql
INSERT INTO employees 
VALUES (1, 'Fahd', 'Mekawy', 50.0, '2022-07-19'),
       (2, 'Mohamed', 'Ahmed', 50.0, '2020-07-19');
```

### Insert Data into Specific Columns
```sql
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (1, 'Fahd', 'Mekawy');
```

---

This documentation covers basic SQL commands for data definition and manipulation. You can expand on these examples as you delve deeper into SQL.
```
