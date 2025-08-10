## 1. YouTube channel

- techFTQ
- Data with baraa
- Riti Kumari
- Jenny's Lecture

## 2. Online Materials

- https://learnsql.com/
- https://docs.snowflake.com/
- https://www.oracletutorial.com/oracle-basics

## To set up a sql-notebook using jupyter

1. mkdir sql-botebook
2. cd sql-notebook
3. python -m venv env
4. env\Scripts\activate
5. pip install --upgrade pip
6. pip install notebook
7. pip install ipython-sql
8. pip install prettytable==0.7.2
9. pip install mysql-connector-python
10. jupyter notebook

- %load_ext sql
- %sql mysql+mysqlconnector://root:root@localhost:port/database_name

- !pip install ipython-sql mysql-connector-python (Run in notebook cell)
