# General Order SQL Commands

SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT

# WHERE
The WHERE clause is used to filter records.
It is used to extract only those records that fulfill a specified condition.

- Note: The WHERE clause is not only used in SELECT statements, it is also used in UPDATE, DELETE, etc.!

# Clauses in SQL
Certainly! Here's the list with each clause name followed by a hyphen, and all descriptions aligned with the same indentation:

- SELECT -  Retrieves columns/data from one or more tables.  
- FROM -   Specifies the table(s) from which to retrieve or delete data.  
- WHERE -  Filters rows to include only those that meet specified criteria.  
- GROUP BY -   Groups rows that have the same values in specified columns.  
- HAVING -  Applies filters on grouped data (used with GROUP BY).  
- ORDER BY -   Sorts the result set by one or more columns (ascending/descending).  
- LIMIT -   Restricts the number of rows returned (MySQL, PostgreSQL, SQLite).  
- TOP - Limits rows returned (used in SQL Server).  
- OFFSET -  Specifies the starting point to return rows (used with LIMIT).  
- DISTINCT -   Removes duplicate records from the results.  
- JOIN -   Combines rows from two or more tables based on related columns.  
- UNION -   Combines results of two or more SELECT statements (duplicates removed).  
- UNION ALL -   Combines results of two or more SELECT statements (includes duplicates).  
- AS -  Provides an alias for columns or tables.  
- IN -  Allows specifying multiple values in a WHERE clause.  
- BETWEEN - Selects values within a given range in a WHERE clause.  
- LIKE -   Pattern matching for filtering results in a WHERE clause.  
- AND - Combines multiple conditions in WHERE/HAVING (all must be true).  
- OR -  Combines multiple conditions in WHERE/HAVING (any can be true).  
- EXISTS -  Checks for the existence of rows meeting a subquery’s criteria.  
- ALL - Used with WHERE or HAVING to compare a value to all values in a list.  
- ANY - Used with WHERE or HAVING to compare a value to any one value in a list.  
- SOME -   Same functionality as ANY.  
- CASE -   Implements if-then-else logic in queries.  
- UPDATE -  Modifies existing records in a table.  
- INSERT -  Adds new records into a table.  
- DELETE -  Deletes existing records from a table.  
- LIMIT/FETCH - Restricts result set (FETCH is used in Oracle, SQL Server).  
- OFFSET-FETCH -   Pagination in SQL Server/Oracle.  
- WITH -   Defines CTEs (Common Table Expressions).  

# Resources
[1] https://www.geeksforgeeks.org/sql/sql-clauses/
[2] https://hightouch.com/sql-dictionary/sql-where
[3] https://www.scaler.com/topics/clause-in-sql/
[4] https://data-flair.training/blogs/clause-in-sql/
[5] https://www.w3schools.com/sql/sql_where.asp
[6] https://www.w3schools.com/sql/sql_examples.asp
[7] https://hightouch.com/sql-dictionary/sql-with
[8] https://www.mssqltips.com/sqlservertip/7575/sql-clause-statement-command-expression-batch-definition/