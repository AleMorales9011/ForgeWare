![Banner](images/futurism-perspective-digital-nomads-lifestyle.jpg)
# DBMS: Data base Management System

120 minutes

SGBD (Database Management Databases are one of the core pillars of every `system architecture`. They are essential for managing data. 

# Table of Contents

1. Prerequisites
2. Connecting to a MySQL Database Via CLI
3. Modeling And Designing A Database With MySql Workbench
4. Deploying A Database Via Script
5. Inserting Data Via Script
6. Creating A View For Easy Acces.
7. Conclusion

# Prerequisites

1. MySQL Community Server
2. MySQL Workbench

# Connecting Via CLI

The CLI(command line interface) provides a direct way to interact with the `database server`. 

```ruby
mysql -u root -p
```

# Modeling With MySql Workbench

MySQL Workbench offers a set of tools for modeling and `designing databases`. 

![DER_Loja](images/der_database_loja.png)

# SQL Categories

In SQL, there are five main categories of commands, each serving a specific purpose in managing and interacting with databases. By understanding these different categories of SQL commands, you can effectively manage your database, ensuring proper `data structure`, manipulation, `security`, and retrieval capabilities.

![SQL_101](images/SQL_101.jpeg)

| DML(Data Manipulation)                                         | DDL(Data Definition Language)                                                                          |   
|--------------------------------------------------------------- |--------------------------------------------------------------------------------------------------------|
| `SELECT` column1 `FROM` table;                                 | `CREATE VIEW` view_name `AS SELECT` column1, column2, `FROM` table_name `WHERE` condition;             |     
| `INSERT INTO` table_name `VALUES` value1;                      | `CREATE DATABASE` my_database; `CREATE TABLE` employees (id INT PRIMARY KEY, name VARCHAR(100));       |
| `UPDATE` table_name `SET` column1 = value1, `WHERE` condition; | `ALTER TABLE` employees `ADD`/`MODIFY` email VARCHAR(100); `ALTER TABLE` employees `DROP COLUMN` email;|             
| `DELETE FROM` table_name `WHERE` condition;                    | `TRUNCATE` TABLE employees;                                                                            |
|                                                                | `DROP DATABASE` my_database; `DROP TABLE` employees; `DROP VIEW` employee_view;                        |
|                                                                | `ALTER TABLE` orders `ADD CONSTRAINT` fk_employee `FOREIGN KEY` (emp_id) `REFERENCES` employees(id);   |
|                                                                | `ALTER TABLE` employees `ADD CONSTRAINT` unique_name `UNIQUE` (name);                                  |                |                                                                | `ALTER TABLE` employees `ADD CONSTRAINT` check_age `CHECK` (age > 18);                                |
|                                                                | `ALTER TABLE` employees `ALTER COLUMN` status `SET DEFAULT` 'active';                                  |


# Transactions
Here’s an example of a transaction in SQL that includes all possible scenarios: `COMMIT`, `ROLLBACK`, `SAVEPOINT`, and `ROLLBACK TO SAVEPOINT`. This transaction simulates a banking system where we perform a few account updates, use a savepoint, and handle an error that requires a rollback to a specific point.

```SQL
-- Start the transaction
BEGIN TRANSACTION;

-- Step 1: Deduct $500 from Account A
UPDATE accounts
SET balance = balance - 500
WHERE account_id = 'A';

-- Step 2: Set a SAVEPOINT after deducting from Account A
SAVEPOINT deduct_from_A;

-- Step 3: Add $500 to Account B
UPDATE accounts
SET balance = balance + 500
WHERE account_id = 'B';

-- Step 4: Set another SAVEPOINT after adding to Account B
SAVEPOINT add_to_B;

-- Step 5: Check balances to validate transaction
SELECT account_id, balance FROM accounts WHERE account_id IN ('A', 'B');

-- Let's assume we find an issue here (e.g., Account B is overdrawn due to a previous transaction error),
-- so we decide to ROLLBACK to the savepoint where we had only deducted from Account A.

-- Step 6: Rollback to the savepoint after deducting from Account A
ROLLBACK TO deduct_from_A;

-- Step 7: Now, decide whether to commit the transaction (if everything is fine), or rollback the entire thing
-- In this case, let's assume we fix the issue and commit the transaction
COMMIT;
```


| DCL (Data Control Language)                       | TCL (Transaction Control Language)   |  Operations                                                                                 |
----------------------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------|
| `GRANT SELECT`, `INSERT ON` employees `TO` user   | `COMMIT`                             | `SELECT` name `AS` employee_name, salary `AS` monthly_salary `FROM` employees;              |
| `REVOKE INSERT ON` employees `FROM` user1;        | `ROLLBACK`;                          | `SELECT` department, `COUNT`(*) `AS` total_employees `FROM` employees `GROUP BY` department;|
|                                                   | `SAVEPOINT` sp1;                     | `SELECT` department, `COUNT`(*) `AS` total_employees `FROM` employees `GROUP BY` department `HAVING COUNT`(*) > 5;|
|                                                   | `ROLLBACK TO` sp1;                   | `SELECT` name, salary `FROM` employees `ORDER BY` salary `ASC`;                             |
|                                                   |                                      | `SELECT` name, salary `FROM` employees `ORDER BY` salary `DESC`;                            |

# Joins

| Joins                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------|
|`SELECT` employees.name, departments.department_name `FROM` employees `INNER JOIN` departments `ON` employees.department_id = departments.id; |
|`SELECT` employees.name, departments.department_name `FROM` employees `LEFT JOIN` departments `ON` employees.department_id = departments.id;  |
|`SELECT` employees.name, departments.department_name `FROM` employees `RIGHT JOIN` departments `ON` employees.department_id = departments.id; |
|`SELECT` employees.name, departments.department_name `FROM` employees `FULL JOIN` departments `ON` employees.department_id = departments.id;  |

# DDL

| **Operation**          | **SQL Query Example**                                             | **Explanation**                                                                                  |
|------------------------|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **SELECT (Columns)**    | `SELECT name, salary FROM employees;`                            | Selects the `name` and `salary` columns from the `employees` table.                              |
| **SELECT (All Table \*)**| `SELECT * FROM employees;`                                      | Selects all columns from the `employees` table.                                                  |
| **INSERT (Data to Table)**| `INSERT INTO employees (name, department, salary) VALUES ('John Doe', 'HR', 5000);` | Inserts a new row into the `employees` table with `name`, `department`, and `salary` values.     |
| **UPDATE (Field)**      | `UPDATE employees SET salary = 6000 WHERE name = 'John Doe';`     | Updates the `salary` field to 6000 for the employee with `name = 'John Doe'`.                    |
| **DELETE (Field)**      | `DELETE FROM employees WHERE name = 'John Doe';`                 | Deletes the row from the `employees` table where the `name` is `John Doe`.                       |

# Windows Functions

| **Window Function**  | **SQL Query Example**                                             | **Explanation**                                                                                  |
|----------------------|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **OVER()**           | `SELECT name, salary, SUM(salary) OVER () AS total_salary FROM employees;` | The `OVER()` function calculates the total salary of all employees without `GROUP BY`.          |
| **ROW_NUMBER()**     | `SELECT name, salary, ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num FROM employees;` | Assigns a unique row number to each row ordered by `salary` in descending order.                 |
| **RANK()**           | `SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS rank FROM employees;` | Assigns a rank to each row based on salary, with gaps if there are ties.                         |
| **DENSE_RANK()**     | `SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank FROM employees;` | Similar to `RANK()`, but without gaps in the ranking when there are ties.                        |
| **NTILE()**          | `SELECT name, salary, NTILE(4) OVER (ORDER BY salary DESC) AS quartile FROM employees;` | Divides the employees into 4 equal groups (quartiles) based on their salary.                     |
| **LAG()**            | `SELECT name, salary, LAG(salary, 1) OVER (ORDER BY salary DESC) AS prev_salary FROM employees;` | Retrieves the previous row’s salary based on the current order, showing `NULL` for the first row.|
| **LEAD()**           | `SELECT name, salary, LEAD(salary, 1) OVER (ORDER BY salary DESC) AS next_salary FROM employees;` | Retrieves the next row’s salary based on the current order, showing `NULL` for the last row.     |

# Functions

| **Function** | **Example Query** | **Explanation** |
|--------------|-------------------|-----------------|
| `AVG()`      | `SELECT AVG(salary) FROM employees;` | Returns the average value of the `salary` column from the `employees` table. |
| `SUM()`      | `SELECT SUM(sales) FROM orders;` | Returns the total sum of the `sales` column from the `orders` table. |
| `COUNT()`    | `SELECT COUNT(*) FROM customers;` | Returns the total number of rows in the `customers` table. |
| `MIN()`      | `SELECT MIN(price) FROM products;` | Returns the minimum value from the `price` column in the `products` table. |
| `MAX()`      | `SELECT MAX(age) FROM people;` | Returns the maximum value from the `age` column in the `people` table. |

# Where Clausule

| **Condition/Clause** | **Example Query** | **Explanation** |
|----------------------|-------------------|-----------------|
| `<, >, <>, <=, >=, =` | `SELECT * FROM employees WHERE salary > 50000;` | Selects all employees with a salary greater than 50,000. |
| `AND, OR, NOT`       | `SELECT * FROM employees WHERE age >= 30 AND department = 'HR';` | Selects employees who are 30 years or older and work in the HR department. |
| `BETWEEN`            | `SELECT * FROM products WHERE price BETWEEN 100 AND 500;` | Selects products with a price between 100 and 500. |
| `LIKE`               | `SELECT * FROM customers WHERE name LIKE 'J%';` | Selects customers whose name starts with "J". |
| `IN`                 | `SELECT * FROM orders WHERE order_status IN ('Shipped', 'Pending');` | Selects orders where the status is either "Shipped" or "Pending". |
| `ANY`                | `SELECT * FROM employees WHERE salary > ANY (SELECT salary FROM managers);` | Selects employees with a salary greater than any of the managers' salaries. |
| `ALL`                | `SELECT * FROM employees WHERE salary > ALL (SELECT salary FROM interns);` | Selects employees whose salary is higher than all the interns' salaries. |
| `EXISTS`             | `SELECT * FROM departments WHERE EXISTS (SELECT * FROM employees WHERE department_id = departments.id);` | Selects departments where there are employees assigned to them. |

# Conclusion
This repository has equipped you with a comprehensive understanding of MySQL, from its core concepts to `advanced functionalities`. You've explored data manipulation, querying, security, administration, and even how to leverage views for optimized data access. 



