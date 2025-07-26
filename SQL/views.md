# Introduction

- VIEW is a database object which will be created over by SQL Query.
- VIEW is like a virtual-table
- VIEW does not store any data, but whenever you call a VIEW it executes the SQL Query underlying.

## TO CREATE A VIEW - This is also refered as a named query.

CREATE VIEW employee_view AS
SELECT id, name FROM Employees;

SELECT * from employee_view;

1. Base table - employees table
2. Derived table (Virtual table) - employee_view

## TO MODIFY THE EXISTING VIEW - (adding a new column and removing an existing column etc)
- If you rename or drop one of the columns referenced by the query, such as id or name, the view 'product_view' will not work anymore. You have to follow the below syntax to modify the existing view with new columns.

CREATE OR REPLACE VIEW employee_view(eID, eName, eEmail, ePhone) AS
SELECT id, name, email, phone from employees;

## Yes — Views are primarily used with SELECT queries.
That’s because a view is essentially a saved SELECT statement. So, by design, views are meant to show data — not change it.
Note: The view does not store data itself; it pulls data from the Employees table whenever it's queried.

- If a view is simple (like selecting from one table, no joins, no aggregations), you can update, insert, or delete data through the view. Then you can do

- UPDATE employee_view SET name = 'John' WHERE id = 1; but this is not a good practice to insert/update records in view.

But if a view has the followings, then it usually becomes read-only. You can only SELECT from it
- Joins
- Group By / Aggregates (like SUM, AVG)
- DISTINCT
- UNION

## TO DROP VIEW
- DROP VIEW IF EXISTS view_name

## ADVANTAGES
- Simplifying data retrieval - Views allow you to encapsulate complex queries with joins, aggregates, unions, and filters, helping you write more straightforward queries.

- Maintaining logical data independence.
- Implementing data security - Views can limit access to sensitive data in the underlying tables by exposing only the relevant data. 