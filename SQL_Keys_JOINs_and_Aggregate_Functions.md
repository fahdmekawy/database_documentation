## Primary Keys

A **Primary Key** is a unique identifier for a record in a table. Each table should have one primary key, which must contain unique values that cannot contain NULL values.

### Example

```sql
CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    amount DECIMAL(5,2)
);

ALTER TABLE transactions
ADD CONSTRAINT PRIMARY KEY(transaction_id);

INSERT INTO transactions VALUES (1000, 4.99);

SELECT amount FROM transactions WHERE transaction_id = 1000;
```

- **Primary Key Definition:** The `transaction_id` column is defined as the primary key, ensuring unique and non-null values.

## Foreign Keys

A **Foreign Key** is a field (or collection of fields) in one table that refers to the primary key in another table. Foreign keys establish relationships between tables, ensuring referential integrity.

### Example

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

SELECT * FROM customers;

INSERT INTO customers (first_name, last_name) 
VALUES ("Fahd", "Mekawy"), ("Mohamed", "Ahmed"), ("Ahmed", "Mohamed");

CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY AUTO_INCREMENT,
    amount DECIMAL(5,2),
    customer_id INT,
    FOREIGN KEY(customer_id) REFERENCES customers(customer_id)
);

DROP FOREIGN KEY transactions_ibfk_1;

ALTER TABLE transactions
ADD CONSTRAINT fk_customer_id
FOREIGN KEY(customer_id) REFERENCES customers(customer_id);

ALTER TABLE transactions
AUTO_INCREMENT = 1000;

INSERT INTO transactions (amount, customer_id)
VALUES (4.99, 3), (4.99, 3), (4.99, 3);

SELECT * FROM transactions;
```

- **Foreign Key Definition:** The `customer_id` column in the `transactions` table is a foreign key that references the `customer_id` column in the `customers` table, establishing a relationship between the two tables.
