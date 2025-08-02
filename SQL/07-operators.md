# 1. Arithmetic Operators
- Addition, subtraction, multiplication, division, modulo

# 2. Comparison | Relational operators - <, >, !=, <>, <=, >=

- Column1 = Column2
- Column = Value
- Functions = value
- Expression = value
- Subquery = value

# 3. Logical operators - AND | OR | NOT

# 4. Range operator - BETWEEN (both lower and upper boundaries are inclusive)

# 5. Membership operators - IN | NOT IN 
- Always use the IN operator when checking for multiple values in the same column, rather than using multiple OR | AND conditions.
- IN operator ignores the duplicates
```sql
SELECT first_name, country 
	FROM Customers
		WHERE country IN ('USA', 'UK', 'USA');
```

# 6. Search operator - LIKE
**% - 0 | 1 | any number of subsequence characters - represents zero or more characters**
1. Example: "a%" - First character must start with letter 'a'
- Apple - true
- Ah - true
- Accident - true
- Orange - false

2. Example: "%in" - Last two characters must end with letters 'in'
- Martin - true
- in - true
- Jasmine - false

3. Example: "%r%" - if you found 'r' anywhere in the text it's true
- Martin - true
- Ryan - true
- R - true
- Alice - false

**Wildcard Characters - underscore(_)**
The string must contain exactly one character. The first two characters can be anything, but the third character must be 'b'. The remaining characters, if any, can be anything.
4. Example: "_ _ b%"
- Robin - true
- Lib - true
- Albert - true
- Barb - false
- Alice - false 

The LIKE operator is case-insensitive by default in MySQL, so 'A%' and 'a%' will match
the same results unless the column has a case-sensitive collation.