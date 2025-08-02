# SET OPERATORS RULES

1. Set operators allow you to combine the results of two or more tables without needing a join condition. However, the tables must have the same number of columns, the columns must have the same data types, and the columns must be in the same order in all the SELECT statements. [columns name can be different]

**Example 1 - If the first table contains 'firstname' (string) and 'lastname' (string), and the second table contains 'customerID' (integer) and 'lastname' (string), the first table’s column order and data types will take priority when using set operators. As a result, SQL will attempt to convert or cast the 'customerID' integer column from the second table to match the 'firstname' string column from the first table—which will cause the operation to fail.**

**Example 2 - If the first table has columns 'firstname' (string) and 'lastname' (string), and the second table also has 'firstname' (string) and 'lastname' (string), but you change the column order in the second SELECT statement—such as selecting 'lastname' first and then 'firstname'—the SELECT statements may still satisfy all the requirements for set operations. However, this mismatch in column order can result in inaccurate data, such as combining 'firstname' from the first table with 'lastname' from the second table, and vice versa, leading to incorrect results.**

2. Set operators can be used in almost all the clauses but ORDER BY clause should be applied only once at the last SELECT statement and the TOP clause should be included only once in the first SELECT statement.
3. The column names or aliases in the final result set are taken from the first SELECT statement. Any column names or aliases specified in the subsequent SELECT statements will be ignored by SQL.
4. Always make sure to mention the columns name in both the SELECT statements instead of using asterisk symbol.
5. Set operators combine tables by stacking their rows vertically.

# TYPES OF SET OPERATORS

1. UNION - returns unique records (removes the duplicates)
2. UNION ALL - returns all the records (it just keeps all the records from both the tables)
   1. UNION ALL is faster than UNION because it does not perform the comparison needed to eliminate duplicate rows.
   2. UNION ALL can be used to find duplicate records in the result.
   3. UNION ALL can also be used to retrieve only unique records if you are certain that no duplicates in both tables.
3. INTERSECT - returns only common records from both tables [similar to INNER JOIN]
4. EXCEPT - returns all the distinct records from the first query that are not found in the second query
   1. Here the order of the tables must be considered cautiously, because it may affect the result set.

# Set operators are ideal when you want to:

1. Aggregate similar data from multiple sources
2. Find overlaps or differences between datasets
3. Simplify combining multiple queries without explicit join keys
4. When no join key is available, but result stacking is needed, set operators provide a clean solution to append results.


# The choice between SET operators and JOINs in SQL depends on what you're trying to achieve—and each has its own optimization sweet spot.

## SET Operators

- Combining results from similar structured queries.
- Filtering distinct rows across datasets.

### Optimization Notes:

- UNION removes duplicates, which can be costly—use UNION ALL if duplicates are acceptable.
- INTERSECT and EXCEPT can be slower on large datasets due to row-by-row comparisons.
- Indexes on all involved columns help performance.

## JOINS

- Fetching related data across multiple tables.
- Building richer, wider result sets.

### Optimization Notes:

- INNER JOINs are generally faster than OUTER JOINs.
- Use indexed columns in join conditions.
- Avoid joining on calculated fields or mismatched data types.
- Filter early using WHERE clauses to reduce row volume before joining.

### Which Is More Optimized?

- JOINs are typically more efficient when combining related data from normalized tables.
