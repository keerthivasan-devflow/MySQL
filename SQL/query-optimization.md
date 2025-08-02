- Always use TOP clause
- Never use asterisk

# Introduction

- SQL aliases are used to give a table, or a column in a table, a temporary name.
- Aliases are often used to make column names more readable.
- An alias only exists for the duration of that query.
- An alias is created with the AS keyword. [Actually, in most database languages, you can skip the AS keyword and get the same result]
- If you want your alias to contain one or more spaces, like "My Great Products", surround your alias with square brackets or double quotes. [Note: Some database systems allows both [] and "", and some only allows one of them.]

# Aliases can be useful in the following scenario

- There are more than one table involved in a query
- Functions are used in the query
- Column names are big or not very readable
- Two or more columns are combined together

# Subquery A query nested inside another query. Can be scalar, correlated, or derived.

Pros: Simple for small, straightforward tasks.

Cons: Correlated subqueries especially can be slower, as they execute repeatedly.

# CTE (Common Table Expression) Defined using WITH and used like a temporary result set.

Pros: Great for breaking down complex logic, improving readability. Can be reused multiple times.

Cons: Not always the fastest, especially in older versions of some SQL engines.

# Join Combines rows from two or more tables based on a related column.

Pros: Generally faster and more efficient, especially when indexes are used effectively.

Cons: Can be harder to read if many joins are involved.

For performance, a well-optimized JOIN usually wins.
For clarity and modularity, CTEs make your queries easier to maintain.
For quick filtering or scalar checks, a subquery might do the trick.
