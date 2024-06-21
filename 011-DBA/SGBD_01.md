![Banner](https://github.com/AleMorales9011/ForgeWare/blob/912757a3619eb391442ee6c245fb9dd5210d952b/src/images/medium-shot-man-living-as-digital-nomad.jpg)
# SQL 101

1 hour

By learning commands within their category, you can see how they relate to each other and their overall purpose. For instance, DDL commands for creating tables (like CREATE) complement DML commands for inserting data (like INSERT) into those tables.  This fosters a deeper understanding of how different commands work together to manage a database

![SQL_101](https://github.com/AleMorales9011/ForgeWare/blob/912757a3619eb391442ee6c245fb9dd5210d952b/src/images/SQL_101.jpeg)

# Window Functions

Window functions in SQL are powerful tools that allow you to perform calculations on a set of rows related to the current row within a result set.

```SQL
-- Sample table with sales data
CREATE TABLE Sales (
  order_id INT PRIMARY KEY,
  customer_id INT,
  product_name VARCHAR(50),
  sale_amount DECIMAL(10,2),
  order_date DATE
);

-- Insert some sample data
INSERT INTO Sales (order_id, customer_id, product_name, sale_amount, order_date)
VALUES
  (1, 101, 'Headphones', 129.99, '2024-01-10'),
  (2, 102, 'Laptop', 799.99, '2024-02-15'),
  (3, 101, 'Monitor', 249.99, '2024-03-01'),
  (4, 102, 'Tablet', 349.99, '2024-03-15'),
  (5, 103, 'Mouse', 29.99, '2024-04-10'),
  (6, 101, 'Keyboard', 49.99, '2024-05-01');

-- Select all sales data with additional columns using window functions
SELECT
  s.order_id,
  s.customer_id,
  s.product_name,
  s.sale_amount,
  s.order_date,
  -- Row number within the entire table
  ROW_NUMBER() OVER (ORDER BY s.order_date) AS row_num,
  -- Rank of sale amount within the entire table (with gaps for ties)
  RANK() OVER (ORDER BY s.sale_amount DESC) AS sale_rank,
  -- Dense rank of sale amount within the entire table (no gaps for ties)
  DENSE_RANK() OVER (ORDER BY s.sale_amount DESC) AS dense_sale_rank,
  -- Bucket (quartile) for sale amount within the entire table (4 buckets)
  NTILE(4) OVER (ORDER BY s.sale_amount DESC) AS sale_quartile,
  -- Sale amount of the previous order for the same customer (if any)
  LAG(s.sale_amount) OVER (PARTITION BY s.customer_id ORDER BY s.order_date) AS prev_sale_amount,
  -- Sale amount of the next order for the same customer (if any)
  LEAD(s.sale_amount) OVER (PARTITION BY s.customer_id ORDER BY s.order_date) AS next_sale_amount
FROM Sales s
ORDER BY s.customer_id, s.order_date;

```
![window_functions](https://github.com/AleMorales9011/ForgeWare/blob/0ffa65f9b255708d1fac746bed43551d80b9c91c/src/images/windows_functions.jpg)

# DCL

DCL commands are used to manage access privileges for users and objects within a database

# Grant

```SQL

GRANT SELECT ON products TO sales_rep;

```
# Revoque

```SQL
REVOKE INSERT, DELETE ON products FROM sales_rep;
```
