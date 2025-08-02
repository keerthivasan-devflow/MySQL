# CASE STATEMENT

- CASE can be placed anywhere in the SQL query
- It will always add a new column in the result set, therefore better to give alias at the end of the case statement

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END AS alias_name
```

# There is only one rule to define CASE statement

- All the results must be the same datatype otherwise error will occur

```sql
CASE
    WHEN amount > 500 THEN "costly"
    WHEN amount > 300 THEN "reasonable price"
    ELSE 1 -- Rule break - Syntactically invalid code
END
```

# If there is only one column in the case statement and condition is based on equal [=] operator, here you go!

```sql
CASE country
    WHEN "US" THEN "The United States of America"
    WHEN "IN" THEN "India"
    ELSE "Not Applicable"
END
```
