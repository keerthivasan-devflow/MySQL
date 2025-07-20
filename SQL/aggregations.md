
# AGGREGATE FUNCTIONS
There are five core aggregate functions that are most commonly used in SQL, and they include:

- COUNT
- MAX
- MIN
- SUM
- AVG

# GROUP BY CLAUSE

**SCENARIO 1 - SELECT sum(balance) FROM accounts**
This query returns the total sum of the `balance` amounts for all customers in the `accounts` table.

**SCENARIO 2 - SELECT account_type, SUM(balance) FROM accounts GROUP BY account_type**
When retrieving data that includes both an aggregated column (like `SUM(balance)`) and a non-aggregated column (like `account_type`), you'll encounter an error if the non-aggregated column is not included in a `GROUP BY` clause. To avoid this, you must use `GROUP BY` on any non-aggregated columns in the `SELECT` list.

Solution - SELECT account_type, sum(balance) FROM accounts GROUP BY account_type
**Order of execution for the above query**
- FROM — The database retrieves data from the accounts table.
- GROUP BY — Rows are grouped based on the account_type column.
- AGGREGATE — The SUM(balance) is calculated for each group.
- SELECT — The grouped account_type and the corresponding sum are selected.
- (Optional ORDER BY) — Since there is no ORDER BY clause here, the results are returned in an undefined order.


**SCENARIO 3 - SELECT account_type FROM accounts GROUP BY account_type**
This will return the unique values of account_type like
- Savings
- Fixed Deposit
- Checking

Note: Even though NULL is generally considered "unknown", in GROUP BY, all NULLs are grouped together.

# HAVING CLAUSE
The HAVING clause is used specifically with aggregated columns, while the WHERE clause cannot be used with them because it filters rows based on raw (non-aggregated) column values before aggregation occurs.

# LIMIT
Use the LIMIT clause to optimize performance and reduce costs. Since every SELECT query can incur charges—especially when all records are retrieved and stored in the cloud—it's best to use LIMIT when you only need to view a sample of the data.

# NULL HANDLING
- IS NULL
- IS NOT NULL
- COALESCE(amount, '0.00', NULL, 'f.ff') - Here you can pass N'no.of.values
- IFNULL(amount, '0.00') - Here you can give only two values