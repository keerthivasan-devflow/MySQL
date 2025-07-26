
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
