## Introduction
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

## Conclusion
Understanding and using **Primary Keys** and **Foreign Keys** effectively is essential for creating robust and relational databases. Primary keys uniquely identify records within a table, while foreign keys establish and enforce relationships between tables. Together, they play a critical role in maintaining data integrity and supporting complex queries across related tables.

For more detailed information and advanced usage, consider exploring topics such as indexing, normalization, and SQL join operations.
```

You can copy and paste this content into your `README.md` file in your GitHub repository to describe the concepts of Primary Keys and Foreign Keys in SQL. This document is structured to be informative and provides examples to help readers understand how to implement these concepts in their own databases.
