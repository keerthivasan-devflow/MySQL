# Subquery Introduction - Illustrated w/ simple example for bette understanding

- SELECT INSERT UPDATE DELETE
- WHERE
- FROM

# Example 1 - Find the employee who's salary is more than the average salary earned by all the employee's

1. Firstly, calculate the average salary of all the employees.
2. Filter result based on above results

- SELECT AVG(salary) from employee; // Consider the output is 7503.22177777
- SELECT * from employee where salary > 7503.22177777

- Optimized Query : SELECT * from employee where salary > (SELECT AVG(salary) from employee)

To sum up, Subquery can be executed by SQL on its own only once based on its result the outer/main query will be executed

# Types of subquery
1. Scalar 
2. Multiple row
3. Correlated

# 1. Scalar Subquery
- It always return 1 row and 1 column - (Finally 1 record will be returned)

select * from employee e 
join (select avg(salary) sal from employee) avg_salary 
on e.salary > avg_salary.sal;

Note: whenever a subquery used with JOIN clause, the records returned by the subquery will be considered as a separate table of records.

# 2. Multiple Row Subquery
# 2.1. Subquery which returns multiple column and multiple row
Example 1 - Find the employee who earn the highest salary in each department

select * from employee where (dept_name, salary) in (select dept_name, max(salary) from employee
group by dept_name)

# 2.2. Subquery which returns 1 column and multiple row
Example 1 - Find the departments who do not have any employee

select * from department where dept_name not in (select distinc dept_name from employee)

# 3. Co-related Subquery - A subquery which is related to the outer query
Example 1 - Find the employees in each department who earn more than the average salary in that department

slect * from employee e1 where salary > (select avg(salary) from employee e2 where e1.dept_name = e2.dept_name)

32.00 continue...