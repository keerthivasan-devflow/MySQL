# Data Manipulation Language

- Important Note - If you execute any DML query, it will return nnumber of rows affected!

## 1. INSERT STATEMENT / INSERT QUERY

### TO INSERT RECORDS FOR ALL THE COLUMNS

```sql
INSERT INTO table_name(column1,column2,...columnN)
VALUES(value1, value2,...valueN);
```

### TO INSERT RECORDS WITHOUT SPECIFYING THE COLUMN NAMES

- If we don't specify column names, the order of columns in the database table must match the order of values in the SQL query. We also need to provide the value(s) for the auto-incremented field.

```sql
INSERT INTO table_name VALUES(value1, value2...ValueN)
```

### TO INSERT RECORDS FOR ONLY SELECTIVE COLUMNS

- Please note that you may skip only the nullable columns, and if any columns are omitted during the data insertion, the output will be NULL.

```sql
INSERT INTO table_name(column1, column2, column4, column6)
VALUES(value1, value2, value4, value6);
```

## 2. INSERT INTO SELECT

- To copy data from one table to another existing table, but tables must have same schema definition otherwise operation will be failed.
- customers: id, first_name, country, score — (4 columns)
- persons: id (NOT NULL), person_name (NOT NULL), birth_date (NULL), phone (NOT NULL) — also 4 columns

- Firstly, retrieve all the necessary data from the source table, and then insert the records into the target table.

```sql
INSERT into person(id, person_name, birth_date, phone) -- destination table (person)
SELECT id, first_name, NULL, 'unknown' FROM customer -- source table (customer)
```

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
  INSERT INTO student VALUES(); - To insert a single row
  INSERT INTO student VALUES(),(),() or INSERT INTO student VALUES(NULL),(NULL),(NULL) - To insert multiple records at once.

# UPDATE QUERY

```sql
    UPDATE [LOW_PRIORITY] [IGNORE] table_name
    SET column_name1 = value1,
        column_name2 = value2,
    	...
    [WHERE condition];
```

# DELETE QUERY

After executing this command, you cannot recover the deleted records. Therefore, you should have a database backup before executing this command. Always use WHERE condition so as to avoid deleting all the rows unintentionally from the table.

    DELETE FROM table_name
    WHERE condition;

    DELETE FROM table_name = TRUNCATE TABLE table_name

# DELETE Statement

1. Removes specific rows using a WHERE clause.
2. Can be rolled back if wrapped in a transaction.
3. Triggers and constraints are executed.
4. Slower for large tables—deletes row by row.

# TRUNCATE Statement

1. Removes all rows from a table. (No need of WHERE clause)
2. Often cannot be rolled back (depends on the DBMS).
3. Triggers do not fire, and constraints may be bypassed.
4. Generally faster and less resource-intensive than DELETE.

# Questions

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

4. What is soft vs hard delete?
5. What happens if we dont give any WHERE condition
6. difference between truncate and delete
