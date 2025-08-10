# Subquery Introduction

- SELECT (INSERT | UPDATE | DELETE)
- FROM
- JOIN
- WHERE (relational and logical operators[IN | ANY | ALL | EXISTS])

Subqueries are accessible only to their immediate outer (main) query; other external queries cannot access the intermediate results produced by these subqueries.

### Why Subquery

For complex tasks,

1. JOIN TABLES
2. FILTERING
3. TRANSFORMATIONS - Handling nulls, creating a new columns
4. AGGREGATIONS

### Example - Find the employee who's salary is more than the average salary earned by all the employee's

1. Firstly, calculate the average salary of all the employees.
2. Find the employees based on above results

```sql
SELECT AVG(salary) FROM employee; -- consider the output is 7503.22177777
SELECT * FROM employee WHERE salary > 7503.22177777

SELECT * FROM employee WHERE salary > (SELECT AVG(salary) FROM employee) -- optimized query (simple example for subquery)
```

- To sum up, Subquery can be executed by SQL on its own only once based on its result the outer/main query will be executed

## Types of subquery

## 1. Scalar Subquery (always returns single record)

```sql
SELECT * FROM employee AS e
JOIN (SELECT avg(salary) AS sal FROM employee) AS avg_sal
ON e.salary > avg_sal.sal;
```

Note: whenever a subquery used with JOIN clause, the records returned by the subquery will be considered as a separate table of records.

## 2. Multiple Row Subquery (Returns single column and multiple row)

- Find the departments who do not have any employee

```sql
SELECT * FROM department WHERE dept_name NOT IN (SELECT distinc dept_name FROM employee)
```

## 3. Table Subquery (Returns multiple row and mutiple column)

- Find the employee who earn the highest salary in each department

```sql
SELECT * FROM employee WHERE (dept_name, salary) IN (SELECT dept_name, max(salary) FROM employee GROUP BY dept_name)
```

**In the above query, the IN clause is used, which allows multiple values. If the assignment operator (=) were used instead, SQL would expect the query to return only a single record.**

## 4. Co-related Subquery - A subquery which is related to the outer query

- Find the employees in each department who earn more than the average salary in that department

```sql
SELECT * FROM employee e1 WHERE salary > (SELECT avg(salary) FROM employee e2 WHERE e2.dept_name = e1.dept_name)

SELECT e1.*
FROM employee e1
JOIN (
    SELECT dept_name, AVG(salary) AS avg_sal
    FROM employee
    GROUP BY dept_name
) e2 ON e2.dept_name = e1.dept_name
WHERE e1.salary > e2.avg_sal;

```

### Key performance drawbacks of correlated subqueries.

If a department (say, HR) has 4 employees, then the subquery calculating the average salary for HR will run 4 times, once for each employee in that department.

This is the main disadvantage of correlated subqueries — they can result in repeated calculations for the same group, which is inefficient.

To avoid this, it's better to use a JOIN with a grouped subquery or CTE to compute the average salary once per department — improving performance and reducing redundancy.

### Subqueries(fast) vs Co-related Subqueries (slow)

### Nested Subquery

- Find store's whose sales where better than the average sales across all the stores.
  - Find total sales for each store
  - Find the average sales for all the stores
  - Compare 1 & 2