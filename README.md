# Resources
### 1. YouTube channel
- techFTQ
- Riti Kumari
- Jenny's Lecture
- Data with baraa

### 2. Sources
- https://learnsql.com/






UPDATE customers 
SET 
    salesRepEmployeeNumber = (SELECT 
            employeeNumber
        FROM
            employees
        WHERE
            jobtitle = 'Sales Rep'
        ORDER BY RAND()
        LIMIT 1)
WHERE
    salesRepEmployeeNumber IS NULL;

1. How to create an empty table like already existing table? https://dev.mysql.com/doc/refman/8.0/en/create-table.html

2. Difference between truncate and delete
- https://www.simplilearn.com/tutorials/sql-tutorial/sql-truncate-vs-delete
- https://www.tutorialspoint.com/sql/sql-truncate-table.htm


- To learn sql - https://docs.snowflake.com/
- To learn oracle - https://www.oracletutorial.com/oracle-basics


mkdir sql-botebook
cd sql-notebook
python -m venv env
env\Scripts\activate
pip install --upgrade pip
pip install notebook
pip install ipython-sql
pip install prettytable==0.7.2
pip install mysql-connector-python
jupyter notebook

%load_ext sql
%sql mysql+mysqlconnector://root:root@localhost:port/database_name

!pip install ipython-sql mysql-connector-python (Run in notebook cell)