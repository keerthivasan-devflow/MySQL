# 1. PRIMARY KEY

CREATE TABLE student(
studentID INT AUTO_INCREMENT PRIMARY KEY,
studentName VARCHAR(255) NOT NULL
);

ALTER TABLE student ADD PRIMARY KEY(studentID); // To add primary key constraint to an existing table
ALTER TABLE student DROP PRIMARY KEY; // To remove primary key constraint from an existing table

# 2. NOT NULL
- By default, all the columns will accept NULL

# 3. UNIQUE (Column/Integrity Constraint)
- It accepts null but does not allow duplicated values.

column name column_defintion UNIQUE; (OR)
column_1_definition, column_2_definition .... column_N_definition, UNIQUE(column1, column2...columnN);
Note: MySQL will use combination of values in both columns to enforce uniqueness.

# 4. DEFAULT

Default constraint should contain only literal constant like a number or string or boolean or enum/sets. 
It cannot be an expression or function, However it can accept CURRENT DATE & DATETIME functions and UUID() if you're using
char/varchar

However, if you explicitly provide a value for the default column in the INSERT query, it will override the default value and be accepted by the database.

# 5. CHECK

To ensure that values stored in a column or group of columns satisfy a Boolean expression.

ALTER TABLE table_name ADD CHECK (expression);
ALTER TABLE table_name ADD CONSTRAINT contraint_name CHECK (expression);
ALTER TABLE table_name DROP CHECK constraint_name;

# 6. AUTO INCREMENT (OR) MySQL SEQUENCE

In MySQL, a sequence is a list of integers generated in the ascending order. MySQL doesn't provide any built-in
functions to generate unique id, whereas we are going to achieve this by using SQL.

If we will insert a new row into a table along with specifying a value for the sequence column,
then MySQL first checks it whether the specified value has already existed or not. If it does 
not exist, it will insert the sequence number in the column; otherwise, issue an error. Again, 
if we insert a value greater than the next sequence number, MySQL will use it as the starting 
sequence number. Now, MySQL will generate the next sequencing value from the current sequence 
number. It is to note that it will create gaps in our sequence.

If we update the AUTO_INCREMENT column's value that already exists by using the UPDATE statement, 
MySQL will issue a duplicate-key error if the column stores only distinct value. If we update an 
AUTO_INCREMENT column with a value greater than the existing values, MySQL inserts the next value 
of the last sequence number for the next row. For example, the AUTO_INCREMENT column's last sequence 
value is 3, and we want to update it with 10, then the sequence number for the next row should be 4.

If we want to delete the last inserted row using the DELETE statement, it is not necessary that 
MySQL will reuse the removed sequence number again because it depends on the table's storage engine(MyISAM). 
For example,if we use the MyISAM table and remove the last insert Id that is 5, MySQL still inserts 
the next sequence number as 6 for the new row. Similar to MyISAM tables, InnoDB tables do not reuse 
sequence number when rows are deleted.

We can use the LAST_INSERT_ID() function to get the last generated sequence number.

	1. Each table has only one AUTO_INCREMENT column whose data type is typically the integer.

	2. The  AUTO_INCREMENT column must be indexed, which means it can be either PRIMARY KEY or UNIQUE index.

	3. The AUTO_INCREMENT column must have a NOT NULL constraint. When you set the AUTO_INCREMENT to a column, 	
	MySQL automatically adds the NOT NULL  constraint to the column implicitly.


# 7. FOREIGN KEY
Foriegn helps to create a relationship between two tables, but both tables should have a column with the same name. In the master table, this column must be defined as the primary key, while in the referencing table, it should be designated as a foreign key.

Example: FOREIGN KEY(rollno) REFERENCES faculty(rollno)

- FOREIGN KEY(rollno) – Specifies that the rollno column in the child table is a foreign key.
- REFERENCES faculty(rollno) – Indicates that this foreign key references the rollno column in the faculty table, where it is defined as a primary key.

Note: If you remove the foreign key definition from the tables, the relationship between them will no longer be enforced.

Student Table - Primary key
Faculty Table - Foreign key

1. If you try to drop the Student table while it has a relationship with the Faculty table, you'll encounter an error so, you must first drop the foreign key constraint or delete the referencing table, and then you can successfully drop the Student table.

2. When a relationship exists between tables, attempting to insert records in the child table may result in a foreign key constraint violation error if the referenced data in the parent table is missing.

3. Deleting records from the parent table can result in a foreign key constraint violation error if related records still exist in the referencing (child) table. To avoid this, you must first remove the corresponding records from the child table that reference the same ID in the parent table. But there is an issue with that - see below

Soft Delete vs Hard Delete
**Student Table (Parent Table)**
101 Keerthivasan keerthivasan@gmail.com
102 Suresh		 suresh.r@gmail.com

**Course Table (Referencing Table)**
101 React
101 Python
102 React

If you perform a hard delete on the records with ID 101 from the Course table, it will permanently remove all course records for Keerthivasan. As a result, it may appear as though he never enrolled in any courses, even though he did — the data is lost. This highlights the risk of hard deletes, as they can lead to loss of important historical information.

To avoid permanent data loss, you can add a new column named `is_delete` with a Boolean data type and a default value of `false` (or `0`). Instead of actually deleting a record, you can perform a **soft delete** by updating this column to `true` (or `1`) using an `UPDATE` query when you no longer need the record. This way, the data remains in the table for reference or auditing purposes.

4. Alternatively, you can define the foreign key with `ON DELETE CASCADE` like this: `FOREIGN KEY (rollno) REFERENCES faculty(rollno) ON DELETE CASCADE`. With this option enabled, deleting a record from the parent (`Student`) table will automatically remove all related records from the referencing (child) table.