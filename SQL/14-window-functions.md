## Reference Table

| product_id | product_name | product_price |
| ---------- | ------------ | ------------- |
| 1          | laptops      | 10            |
| 3          | laptops      | 5             |
| 2          | Bags         | 20            |
| 4          | Bags         | 50            |

## GROUP BY - Returns one row per category, reducing the level of detail

| product_name | total_price |
| ------------ | ----------- |
| laptops      | 15          |
| Bags         | 70          |

## Window functions - Return a result for each individual row, so the level of detail remains unchanged. (granularity stays the same)

| product_id | product_name | product_price | total_price_per_product |
| ---------- | ------------ | ------------- | ----------------------- |
| 1          | laptops      | 10            | 15                      |
| 3          | laptops      | 5             | 15                      |
| 2          | Bags         | 20            | 70                      |
| 4          | Bags         | 50            | 70                      |

## Window Functions / Analytics Functions

- Simple Aggregations (simple data analysis) - Only aggregate functions can be used
- Aggregations + Keeping details (Advanced data analysis) - Aggregate functions + many other window functions

### A. Aggregate Functions

1. COUNT() - This allows all the datatypes but other aggregate functions accept only numerical datatype
2. SUM()
3. AVG()
4. MIN()
5. MAX()

### B. Rank Functions

1. Integer-Based Ranking(discrete) (Top | Bottom Analysis) - Find the top 3 products
   1. ROW_NUMBER()
   2. RANK()
   3. DENSE_RANK()
   4. NTILE(n) - only this fuction accepts numerical value as parameter
2. Percentage-Based Ranking(continuous) (Distribution Analysis) - Find top 20% products
   1. CUME_DIST()
   2. PERCENT_RANK()

### C. Value Functions - accepts all the datatypes

1. LEAD(expr, offset, default)
2. LAG(expr, offset, default)
3. FIRST_VALUE(expr)
4. LAST_VALUE(expr)

## Why Window Functions?

```sql
-- If you would like to get total price of each category, It works really good!
SELECT category SUM(product_price) AS total_price
    FROM products GROUP BY category

-- but when you want additional details, it breaks!
SELECT product_id, product_name, category, SUM(price) AS total_price
    FROM products GROUP BY product_id, product_name, category

-- Finally expected output
SELECT product_id, product_name, category,
    SUM(price) OVER(PARTITION BY category) AS total_category_price FROM products
```

## Syntax to write window functions

- window functions -> OVER clause (to tell SQL that window function is used)
- window functions -> PARTITION BY -> ORDER BY -> FRAME

| category  | partition | order by | frame                                                                |
| --------- | --------- | -------- | -------------------------------------------------------------------- |
| aggregate | optional  | optional |
| rank      | optional  | required | not allowed                                                          |
| value     | optional  | required | not allowed (LAG, LEAD), optional(FIRST_VALUE), required(LAST_VALUE) |

## Input Table To Explore OVER() clause

| month | product | price |
| ----- | ------- | ----- |
| Jan   | Apple   | 100   |
| Jan   | Apple   | 150   |
| Jan   | Banana  | 80    |
| Feb   | Apple   | 120   |
| Feb   | Banana  | 90    |
| Feb   | Banana  | 110   |
| Feb   | Orange  | 130   |

## 1. PARTITON BY - divides the entire dataset into partitions / windows (similiar to GROUP BY)

```sql
-- Find sum of the total products for each row
SELECT month, product, SUM(price) OVER() AS total_price FROM products

-- Total sum of product of each month
SELECT month, product, SUM(price) OVER(PARTITION BY month) AS total_price FROM products

-- Total sum of each month and product category
SELECT month, product, SUM(price) OVER(PARTITION BY month, product) AS total_price FROM products

-- Flexibility of window function allows aggregation of data at different granularities within the same query
SELECT month, product,
    SUM(price) OVER() AS total_price,
    SUM(price) OVER(PARTITION BY month) AS total_price
    FROM products
```

## 2. ORDER BY - sorts the dataset by window in ascending | descending order

```sql
-- sorted the dataset based on overall price column
SELECT month, product, RANK() OVER(ORDER BY price) AS Ordered_Products FROM products

-- sorted the dataset based on each product category (by considering different windows of product category)
SELECT month, product, RANK() OVER(PARTITION by product ORDER BY price) FROM products
```

## 3. FRAME (Sliding Window Technique)

- defines a subset of rows within each window that is relevant for the calculation
- PARTITION BY -> ORDER BY -> FRAME (frame_types BETWEEN lower_boundary_value AND higher_boundary_value)
  - frame_types - ROWS | RANGE
  - lower_boundary_value (Lower Boundary Value) - CURRENT ROW | N PRECEDING | UNBOUNDED PRECEDING
  - higher_boundary_value (Higher Boundary Value) - CURRENT ROW | N FOLLOWING | UNBOUNDED FOLLOWING
- Rules for defining FRAME's
  - FRAME can be used together with ORDER BY clause
  - Lower boundary value must be before the higher boundary value

### Reference Table for the FRAME Concept

| month | product | price |
| ----- | ------- | ----- |
| Jan   | Apple   | 100   |
| Feb   | Apple   | 150   |
| Mar   | Banana  | 80    |
| Apr   | Apple   | 120   |
| May   | Banana  | 90    |
| Jun   | Banana  | 110   |
| Jul   | Orange  | 130   |

```sql
-- Note - FRAME returns the different result of dataset when we have PARTITION BY clause
-- N FOLLOWING
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN CURRENT ROW AND 2 FOLLOWING) AS cumulative_price
    FROM products

-- UNBOUNDED FOLLOWING (last possible row within a window/partition)
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS cumulative_price
    FROM products

-- N PRECEDING
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN 1 PRECEDING AND CURRENT ROW) AS cumulative_price
    FROM products

-- UNBOUNDED PRECEDING
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_price
    FROM products

-- 1 PRECEDING AND 1 FOLLOWING
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS cumulative_price
    FROM products

-- UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING (total of all the products in which current rows never considered, it can be anywhere!)
SELECT month, product, SUM(price) OVER(ORDER BY month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS cumulative_price
    FROM products
```

### CURRENT ROW can be skipped only for preceding

- ROWS BETWEEN 2 PRECEDING AND CURRENT ROW `(ROWS 2 PRECEDING)`
- ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW `(ROWS UNBOUNDED PRECEDING)`

### DEFAULT FRAME will be used - if ORDER BY used without FRAME

- Therefore default frame is `ROWS UNBOUNDED PRECEDING`

### 4 Important Rules for defining window functions

1. Nested window function is not allowed.
2. Window function can be used with SELECT and ORDER BY clause only.
3. SQL will execute window function only after the WHERE clause.
4. window function can be used together with GROUP BY in the same query, only if the same columns are used.