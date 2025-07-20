## DDL COMMANDS
- https://www.dbvis.com/thetable/how-to-create-a-table-like-another-table-in-mysql/
- https://www.datacamp.com/tutorial/sql-ddl-commands

The CREATE statement is used to create new database objects, such as tables, views, or indexes. The syntax of the DDL command changes based on the object to create. To add a new table to the database, the syntax is:

1. CREATE TABLE

	CREATE TABLE [IF NOT EXISTS] table_name(
	column_1_definition,
	column_2_definition,
	...,
	table_constraints
	) ENGINE=storage_engine;
	
	show tables; - it will list out all the tables which has been created and available now in particular database.
	By wrapping the table name(or any identifiers) in backticks, you tell MySQL to treat it as an identifier, 
	thus avoiding any conflicts with reserved keywords
	
2. ALTER TABLE - RENAME, ADD, MODIFY/CHANGE, DROP COLUMN

	ALTER TABLE table_name RENAME TO new_table_name;
	
	RENAME TABLE old_table_name1 to new_table_name_1, 
				 old_table_name2 to new_table_name_2
				 old_table_nameN to new_table_name_N;
	Note: using RENAME TABLE, you cannot rename the temp table so you will have to use above alter command
	
	ALTER TABLE table_name
	ADD COLUMN new_column_definition 
    [FIRST | AFTER existing_column];
	(To add one/more new columns in the table)
	
	ALTER TABLE table_name 
	MODIFY COLUMN existing_column_definition 
	[FIRST | AFTER column_name]
	(To modify existing column datatype, column constraints)
	
	This syntax is used in MySQL to change the datatype of a column. In MySQL, you must repeat the column name after CHANGE COLUMN even if you're not changing the column name itself.
	ALTER TABLE employees CHANGE COLUMN salary salary DECIMAL(10, 2);
	
	ALTER TABLE table_name 
	CHANGE COLUMN original_column new_column_definition 
	[FIRST | AFTER column_name];
	(To rename column name, add new datatype, column constraints)
	
	ALTER TABLE table_name 
	DROP COLUMN column_name1,
	DROP COLUMN column_name2; 
	(To drop one/more columns in the table)

3. DROP TABLE

	1. DROP TABLE table_name
	2. DROP TABLE table_name1, table_name2...table_nameN
	3. DROP TEMPORARY TABLE table_name
	4. TRUNCATE TABLE table_name
	5. SHOW CREATE TABLE parts; - To view if there are any constraints defined.
	6. DROP TABLE IF EXISTS parts; - To delete the table along with data and also if any parts.
	
4. COPY TABLE

	CREATE TABLE new_table_name  
	SELECT column1, column2, column3   
	FROM existing_table_name;
	
	1. Advantage - useful for creating the replica of existing table for testing purpose, w/o affecting the original data.
	2. copy data from original table to duplicate table;
	3. copy data partially from original table to partial table;
	4. copy table from one database to another;
	
4.1. To create only table structure(schema) like columns, datatypes and constraints but does not copy any data.
	CREATE TABLE destination_db.new_table_name   
	LIKE source_db.existing_table_name INCLUDING ALL/INDEXES/CONSTRAINTS;  

5. SHOW COLUMNS - SHOW COLUMNS FROM mytable_name FROM mydb_name;  (OR) SHOW COLUMNS FROM mydb_name.mytable_name;  
	

