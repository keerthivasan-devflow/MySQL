## SELECT INTO STATEMENT

1. Advantage - useful for creating the replica of existing table for testing purpose, w/o affecting the original data.
2. copy data from original table to duplicate table;
3. copy data partially from original table to partial table;
4. copy table from one database to another;

This will work only in SQL Server and PostgreSQL Server

```sql
SELECT * INTO customersCopy FROM customers -- To copy data from existing table to a new table
SELECT * INTO customersCopy FROM customers WHERE false -- To copy only table structure but not contraints, indexes, triggers, etc.
```

This works in MySQL

```sql
CREATE TABLE customerCopy AS
    SELECT * from customers
```

# General Order SQL Commands

- SELECT
- TOP
- FROM
- JOIN
- WHERE
- GROUP BY
- HAVING
- ORDER BY
