# LEFT JOIN | RIGHT JOIN

- LEFT JOIN = INNER JOIN + any additional records in the left table(primary table)
- If the `SELECT` clause includes columns from the right table that do not meet the join condition, those columns will return `NULL`.
- Example - Fetch all the employees with their department name, manager name and project they're working on!

# FULL OUTER JOIN

- FULL OUTER JOIN = INNER JOIN + [any additional records in the right table] + [any additional records in the left table]
- Example - Fetch all the employees with their dept name, manager name and project they're working on!

SELECT e.emp_name, d.dept_name
from employee e FULL OUTER JOIN department d
ON e.emp_id = d.dept_id;

# CROSS JOIN

- No join condition is required.
- No of records returned by cross join = No of records in the left table * No of records in the right table

SELECT e.emp_name, d.dept_name
from employee e CROSS JOIN department d;

- SECNARIO 1 : When there is no common column to join the tables, but you still need to combine and fetch data from both, a CROSS JOIN is the appropriate choice.

1. Fetch the employee name and their corresponding department name
2. Also make sure to fetch the company name and company location to each employee

SELECT e.emp_name, d.dept_name, c.company_name, c.company_location
from employee e
inner join
department d on e.emp_id = d.dept_id
cross join company c;

Sure! Here's a clearer and more professional rephrasing:

# NATURAL JOIN (Not recommended for use in real-time projects)

- No join condition is required. Instead, SQL automatically determines which columns to match based on identical column names in both tables.
- If there is a matching column exist, SQL performs an INNER JOIN based on that column.
- If there are no matching columns, SQL defaults to CROSS JOIN.
- If there are multiple matching columns, SQL uses all of them to perform the INNER JOIN.

- Note - Due to its implicit behavior, NATURAL JOIN can lead to unpredictable results and is generally avoided in production environments.
