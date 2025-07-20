1. SELECT - you can get all the columns values or specific set of columns

SELECT * FROM table_name
SELECT name, email, city FROM table_name

2. WHERE CLAUSE - can be used with DELETE/UPDATE etc.

Comparison: <, >, <=, >=, =, <>/!=, between, like, in
Logical: and, or, not
Null: is null, is not null
Aggregation: min, max, count, sum, avg

3. LIMIT number OFFSET number
Example: SELECT * FROM table_name LIMIT 5 OFFSET 3 
Note: always offset values start from offset + 1, so 3 + 1 = 4. Therefore, 4, 5, 6, 7, 8

4. LIKE
% is a wildcard character that represents zero or more characters. So, 'a%' means any 
string that begins with "a" and is followed by any number of characters (or even no characters at all).

The LIKE operator is case-insensitive by default in MySQL, so 'A%' and 'a%' will match 
the same results unless the column has a case-sensitive collation.

"a%" - Starts with 'a'
"%a"- Ends with 'a'
"a%o"- Starts with 'a' & Ends with 'o'
"%ra%"- if phrase contains 'ra' anywhere
"_a%" - second character must be 'a'

	UPDATE employees
	SET salary = CASE
   		WHEN id = 1 THEN 5000.00
    	WHEN id = 2 THEN 6000.00
    	WHEN id = 3 THEN 7000.00
    	ELSE salary
		END
	WHERE id IN (1, 2, 3);

	UPDATE employees
	SET salary = IF(id = 1, 5000.00, 
				 IF(id = 2, 6000.00, 
                 IF(id = 3, 7000.00, salary)))
	WHERE id IN (1, 2, 3);


