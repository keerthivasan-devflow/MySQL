# 1. Comparison | Relational operators - <, >, ==, !=, <>, <=, >=

- Column1 = Column2
- Column = Value
- Functions = value
- Expression = value
- Subquery = value

# 2. Logical operators - AND | OR | NOT

# 3. Range operator - BETWEEN (both lower and upper boundaries are inclusive)

# 4. Membership operators - IN | NOT IN 
	- Always use the IN operator when checking for multiple values in the same column, rather than using multiple OR conditions.

# 5. Search operator - LIKE
**% - 0 | 1 | any number of subsequence characters - represents zero or more characters**
   Example: "a%" - First character must start with letter 'a'
	Apple - true
	Ah - true
	Accident - true
	Orange - false

   Example: "%in" - Last two characters must end with letters 'in'
	Martin - true
	in - true
	Jasmine - false

   Example: "%r%" - if you found 'r' anywhere in the text it's true
	Martin - true
	Ryan - true
	R - true
	Alice - false

**Wildcard Characters - underscore(_)**
The string must contain exactly one character. The first two characters can be anything, but the third character must be 'b'. The remaining characters, if any, can be anything.
   Example: "_ _ b%"
	Robin - true
	Lib - true
	Albert - true
	Barb - false
	Alice - false 

The LIKE operator is case-insensitive by default in MySQL, so 'A%' and 'a%' will match
the same results unless the column has a case-sensitive collation.

# TIMELIME - Data with baraa BootCamp SQL Video
2.08.02 - Comparison Operator
2.17.15 - Logical Operator
2.28.21 - Range Operator (BETWEEN)
2.33.00 - Membership Operator (IN | NOT IN)
2.37.00 - LIKE Operator (%)