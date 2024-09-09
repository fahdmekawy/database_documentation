In SQL, **Primary Keys** and **Foreign Keys** are crucial concepts that help maintain data integrity and define relationships between tables in a database. This document provides an overview of these keys, their importance, and examples of how to use them effectively.

## Primary Key

### What is a Primary Key?
A **Primary Key** is a unique identifier for each record in a table. It ensures that no two rows in the table have the same value in the primary key column(s). Additionally, a primary key column cannot contain `NULL` values, ensuring that every record has a valid and unique identifier.

### Key Characteristics:
- **Uniqueness:** Each value in the primary key column(s) must be unique.
- **Non-NULL:** Primary key columns cannot contain `NULL` values.

### Example: Creating a Primary Key
Below is an example of how to create a table with a primary key in SQL:
```sql
CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    amount DECIMAL(5,2)
);
```
In this example, the `transaction_id` column is defined as the primary key, ensuring that each transaction has a unique identifier.

### Example: Adding a Primary Key to an Existing Table
If you already have a table and need to add a primary key, you can do so using the following SQL statement:
```sql
ALTER TABLE transactions
ADD CONSTRAINT PRIMARY KEY(transaction_id);
```

### Example: Inserting and Querying Data Using a Primary Key
Here's how you can insert data into a table with a primary key and query it:
```sql
INSERT INTO transactions (transaction_id, amount) 
VALUES (1000, 4.99);

SELECT amount FROM transactions WHERE transaction_id = 1000;
```
This ensures that you can uniquely identify and retrieve records based on the primary key.

## Foreign Key

### What is a Foreign Key?
A **Foreign Key** is a field (or collection of fields) in one table that refers to the primary key in another table. It establishes a link between the data in the two tables, enforcing referential integrity. This means that a record in the child table cannot exist unless it is associated with a valid record in the parent table.

### Key Characteristics:
- **Referential Integrity:** Ensures that foreign key values in the child table correspond to existing primary key values in the parent table.
- **Relationships:** Used to define and enforce relationships between tables, such as one-to-many or many-to-one relationships.

### Example: Creating a Table with a Foreign Key
Below is an example of how to create two related tables with a foreign key:
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY AUTO_INCREMENT,
    amount DECIMAL(5,2),
    customer_id INT,
    FOREIGN KEY(customer_id) REFERENCES customers(customer_id)
);
```
In this example, the `customer_id` column in the `transactions` table is a foreign key that references the `customer_id` column in the `customers` table. This ensures that each transaction is linked to a valid customer.

### Example: Adding a Foreign Key to an Existing Table
You can add a foreign key to an existing table using the following SQL statement:
```sql
ALTER TABLE transactions
ADD CONSTRAINT fk_customer_id
FOREIGN KEY(customer_id) REFERENCES customers(customer_id);
```

### Example: Inserting and Querying Data Using a Foreign Key
Here's how you can insert data into a table with a foreign key and query it:
```sql
INSERT INTO transactions (amount, customer_id)
VALUES (4.99, 3), (9.99, 1);

SELECT * FROM transactions;
```
This ensures that the `customer_id` in the `transactions` table corresponds to a valid `customer_id` in the `customers` table.

Sure! Below is a `README.md` file that explains the concept of SQL JOINs, including examples of different types of joins.

```


## SQL JOINs

In SQL, a **JOIN** is used to combine rows from two or more tables based on a related column between them. By using JOINs, you can retrieve data from multiple tables in a single query, making it easier to work with related data.

### Types of JOINs

### 1. INNER JOIN
**INNER JOIN** returns only the rows that have matching values in both tables. If there is no match, the rows are excluded from the result set.

#### Example:
```sql
SELECT customers.first_name, customers.last_name, transactions.amount
FROM customers
INNER JOIN transactions
ON customers.customer_id = transactions.customer_id;
```
This query retrieves the `first_name`, `last_name` from the `customers` table and the `amount` from the `transactions` table where the `customer_id` matches in both tables.

### 2. LEFT JOIN (or LEFT OUTER JOIN)
**LEFT JOIN** returns all the rows from the left table (table1), and the matched rows from the right table (table2). If there is no match, NULL values are returned for columns from the right table.

#### Example:
```sql
SELECT customers.first_name, customers.last_name, transactions.amount
FROM customers
LEFT JOIN transactions
ON customers.customer_id = transactions.customer_id;
```
This query retrieves all customers, including those who haven't made any transactions. For those without transactions, the `amount` field will contain `NULL`.

### 3. RIGHT JOIN (or RIGHT OUTER JOIN)
**RIGHT JOIN** returns all the rows from the right table (table2), and the matched rows from the left table (table1). If there is no match, NULL values are returned for columns from the left table.

#### Example:
```sql
SELECT customers.first_name, customers.last_name, transactions.amount
FROM customers
RIGHT JOIN transactions
ON customers.customer_id = transactions.customer_id;
```
This query retrieves all transactions, including those not associated with any customer (if there are any). For those without customers, the `first_name` and `last_name` fields will contain `NULL`.

### 4. FULL JOIN (or FULL OUTER JOIN)
**FULL JOIN** returns all the rows when there is a match in either the left table or the right table. If there is no match, NULL values are returned for columns where there is no match.

#### Example:
```sql
SELECT customers.first_name, customers.last_name, transactions.amount
FROM customers
FULL OUTER JOIN transactions
ON customers.customer_id = transactions.customer_id;
```
This query retrieves all customers and all transactions. If a customer has no corresponding transaction, or if a transaction has no corresponding customer, `NULL` values will be displayed for the missing columns.

### 5. CROSS JOIN
**CROSS JOIN** returns the Cartesian product of the two tables, i.e., it combines every row of the first table with every row of the second table. This JOIN does not require a matching condition.

#### Example:
```sql
SELECT customers.first_name, transactions.amount
FROM customers
CROSS JOIN transactions;
```
This query retrieves every possible combination of `customers` and `transactions`, regardless of whether they are related.

### 6. SELF JOIN
A **SELF JOIN** is a regular join, but the table is joined with itself. It is useful when you need to compare rows within the same table.

#### Example:
```sql
SELECT A.first_name AS Employee1, B.first_name AS Employee2
FROM employees A, employees B
WHERE A.manager_id = B.employee_id;
```
In this query, the `employees` table is joined with itself to find all employees who report to the same manager.


