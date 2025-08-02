# Data Definition Language - [DDL]

# 1. CREATE TABLE

```sql
   CREATE TABLE [IF NOT EXISTS] table_name(
   column_1_definition,
   column_2_definition,
   ...
   column_N_definition
   )
```

show tables; - it will list out all the tables which has been created and available now in particular database.
By wrapping the table name(or any identifiers) in backticks, you tell MySQL to treat it as an identifier,
thus avoiding any conflicts with reserved keywords

# 2. ALTER TABLE

```sql
	ALTER TABLE table_name RENAME TO new_table_name;

	RENAME TABLE old_table_name1 to new_table_name_1,
				 old_table_name2 to new_table_name_2
				 old_table_nameN to new_table_name_N;
	-- Note: using RENAME TABLE, you cannot rename the temporary table so you will have to use above alter command

	-- add any extra column if you need to include in an already existing table
    ALTER TABLE table_name
    ADD column_definition_1, column_definition_2, column_definition_N

	-- drop column if you need to include in an already existing table
    ALTER TABLE table_name
    DROP COLUMN column_name_1, column_name_2, column_name_N

	-- To rename a column name
    ALTER TABLE table_name
    RENAME COLUMN column_name TO new_name;

	-- To change the datatype of an already existing column
    ALTER TABLE table_name
    ALTER COLUMN column_name SET datatype;
```

# 3. DROP TABLE

```sql
   DROP TABLE table_name -- drop a single table
   DROP TABLE table_name1, table_name2...table_nameN -- drop mutiple tables at a time
   DROP TEMPORARY TABLE table_name -- drop temporary table
   TRUNCATE TABLE table_name -- deleted all the records from the table, but it just keeps table structure
```

# Questions

1. What is CREATE statement?
   - The CREATE statement is used to create new database objects, such as tables, views, or indexes.
