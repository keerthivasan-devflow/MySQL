Note:  If you execute any query like INSERT, UPDATE, DELETE - It will return no.of rows affected!

# INSERT QUERY

### To insert records for all the columns

INSERT INTO table_name(column1,column2,...columnN)
VALUES(value1, value2,...valueN);
(OR)
INSERT INTO table_name VALUES(value1, value2...ValueN) - but the order of values must be the same as table deinition

### To insert records for only selective columns
Please note that you may skip only the nullable columns, and if any columns are omitted during the data insertion, the output will be NULL.

INSERT INTO table_name(column1,column2, column4,column6)
VALUES(value1, value2, value4, value6);

## Copy data from customer(source) to person(destination) table
To copy data from source to destination table, both should have same schema otherwise operation will be failed.

- customers: id, first_name, country, score — (4 columns)
- persons: id (NOT NULL), person_name (NOT NULL), birth_date (NULL), phone (NOT NULL) — also 4 columns

- Firstly, retrieve all the necessary data from the source table, and then insert the records into the target table.
- Step 1 - SELECT \* FROM customers
- Step 2 - SELECT id, first_name, NULL, 'Unknown' FROM customers
- Step 3 - INSERT into person(id, person_name, birth_date, phone)
  SELECT id, first_name, NULL, 'unknown' FROM customer

- Since the persons table does not have a country column, we only include values for columns that exist. We can insert NULL for the birth_date column because it allows null values. However, since the phone column is NOT NULL, we cannot insert a null value. Instead, we provide a default string like 'Unknown', assuming that the phone column in the persons table is of type VARCHAR.

- As a result, this query retrieves the id and first_name values from the customers table, while the birth_date field will return NULL and the phone field will display 'Unknown' for all records. However, the birth_date and phone columns will not have any assigned column names and will appear as (No column name).

### To specficy the default value while insert query

- you can leave both the column name and its default value (OR) You can mention the column name and value as keyword "DEFAULT"

  INSERT IGNORE query - allows you to disregard rows containing invalid data that would otherwise trigger an error
  and insert only rows that contain valid data. However, if you use the INSERT IGNORE statement, MySQL will issue a
  warning instead of an error & will try to adjust the values to make them valid before adding the value to the table.

  You can limit the multiple rows inserted.
  show variables like "max_allowed_packet";
  set global max_allowed_packet = size(which should be an integer and bytes form);

  Dealing w/ auto_increment attribute - if you have only one attribute "RollNo";
  INSERT INTO student VALUES() (OR) INSERT INTO student() VALUES() - To insert a single row
  INSERT INTO student VALUES(),(),() or INSERT INTO student VALUES(NULL),(NULL),(NULL) - To insert multiple records at once.


# UPDATE QUERY

	UPDATE [LOW_PRIORITY] [IGNORE] table_name 
	SET column_name1 = value1,
        column_name2 = value2,
    	...
	[WHERE condition];

1. What will happen if you don't specify the where clause while updating records? If you omit the WHERE clause, all records in the table will be updated! Always use WHERE condition so as to avoid updating all the rows unintentionally.

2. How to update mutiple columns with a single where condition?

3. How to update multiple rows of data at once?
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


# DELETE QUERY
After executing this command, you cannot recover the deleted records. Therefore, you should have a database backup before executing this command. Always use WHERE condition so as to avoid deleting all the rows unintentionally from the table.

	DELETE FROM table_name
	WHERE condition;

	DELETE FROM table_name = TRUNCATE TABLE table_name