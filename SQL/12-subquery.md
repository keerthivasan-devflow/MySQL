# Subquery Introduction

- SELECT INSERT UPDATE DELETE
- WHERE
- FROM

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

## 1. Scalar Subquery

- It always return 1 row and 1 column

```sql
SELECT * FROM employee e
JOIN (SELECT avg(salary) sal FROM employee) avg_salary
ON e.salary > avg_salary.sal;
```

Note: whenever a subquery used with JOIN clause, the records returned by the subquery will be considered as a separate table of records.

## 2. Multiple Row Subquery

## A. Subquery which returns multiple column and multiple row

- Find the employee who earn the highest salary in each department

```sql
SELECT * FROM employee WHERE (dept_name, salary) IN (SELECT dept_name, max(salary) FROM employee GROUP BY dept_name)
```

## B. Subquery which returns 1 column and multiple row

- Find the departments who do not have any employee

```sql
SELECT * FROM department WHERE dept_name NOT IN (SELECT distinc dept_name FROM employee)
```

## 3. Co-related Subquery - A subquery which is related to the outer query

- Find the employees in each department who earn more than the average salary in that department

```sql
SELECT * FROM employee e1 WHERE salary > (SELECT avg(salary) FROM employee e2 WHERE e1.dept_name = e2.dept_name)
```