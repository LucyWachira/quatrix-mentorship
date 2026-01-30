
### SQL 101 - Learning the Basics
#### SQL & Database General Questions
**1. What is SQL?**
- SQL stands for Structured Query Language.
- This is a standard language for accesing and manipulating databases.

**2. What databases other than PostgreSQL use SQL?**
- Database is an organized , electronic collection of structured data (any collection of related information)
  -  MySQL
  -  SQLite
  -  Oracle Database
  -  MariaDB
  -  Microsoft SQL Server
  - Amazon RDS, Google Cloud SQL

**3. What is a table?**
- Table is where data is stored in a database, which consists of rows and columns.

**4. What is a row?**
- Also known as a record or tuple, it represents a single, horizontal, structured entry in a database.
- It is one complete record in a table.

**5. What is a column?**
- It is the vertical entity within a database table that holds data for a specific attribute or field accross all records.

**6. How do you comment out an SQL line so that it is ignored by the SQL engine?**

- Single line comments start with `--`.
```
-- Select all:
SELECT * FROM Customers;
```

- Multi-line comments start with `/*` and end with `*/`.
- Any text between /* and */ will be ignored.
```
/*Select all the columns
of all the records
in the Customers table:*/
SELECT * FROM Customers;
```

### SQL Keywords (Specific to PostgreSQL)

**1. SELECT**
- Used to retrieve data from a table.

```
SELECT name, age
FROM students
WHERE age > 18;
```

**2. FROM**
- Specifies the table to select or delete data from.

```
SELECT name
FROM employees;
```

**3. WHERE**
- Filters records based on a condition.
- You can use operators like =, <, >, <=, >=, <>, LIKE.

```
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

**4. CREATE**
- Used to create databases or tables.

**5. CREATE DATABASE**

```CREATE DATABASE my_database;```

**6. CREATE TABLE**

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);
```


- Example: 
```
postgres=# CREATE DATABASE vegetable_store;
CREATE DATABASE
postgres=# \l
postgres=# \c vegetable_store ;
You are now connected to database "vegetable_store" as user "postgres".
vegetable_store=# CREATE TABLE vegetables(
vegetable_store(# id SERIAL PRI

vegetable_store(# id SERIAL PRIMARY KEY,
vegetable_store(# name VARCHAR (50),
vegetable_store(# price INT );
CREATE TABLE
vegetable_store=# INSERT INTO vegetables (name, price) VALUES
vegetable_store-# ('cabbage', 50),
vegetable_store-# ('kales', 30);
INSERT 0 2
vegetable_store=# \dt
             List of tables
 Schema |    Name    | Type  |  Owner   
--------+------------+-------+----------
 public | vegetables | table | postgres
(1 row)

vegetable_store=# SELECT * FROM vegetables;
 id |  name   | price 
----+---------+-------
  1 | cabbage |    50
  2 | kales   |    30
(2 rows)
```

**7. DROP**
- Used to delete databases or tables permanently.

**8. DROP DATABASE**
- Deletes an entire database and all its associated tables.
```DROP DATABASE my_database;```
- Switch to postreg first because you can't delete the database while connected to it.
```
vegetable_store=# \c postgres 
You are now connected to database "postgres" as user "postgres".
postgres=# \l
postgres=# DROP DATABASE vegetable_store ;
DROP DATABASE
postgres=# \l
postgres=# \dt
Did not find any tables.
```

**9. DROP TABLE**
- Deletes a table permanently including its data and structure.
```DROP TABLE students;```

**10. TRUNCATE TABLE**
- Deletes all records in a table but keeps the table structure.
```TRUNCATE TABLE students;```
vegetable_store=# SELECT * FROM vegetables;
 id |  name   | price 
----+---------+-------
  1 | cabbage |    50
  2 | kales   |    30
(2 rows)
```
vegetable_store=# TRUNCATE TABLE vegetables ;
TRUNCATE TABLE
vegetable_store=# SELECT * FROM vegetables;
 id | name | price 
----+------+-------
(0 rows)
```
**11. DELETE**
- DELETE is used to remove one or more rows from a table.
- Example of using detete with **WHERE** clause for condition:

```
vegetable_store=# SELECT * FROM vegetables;
 id |  name   | price 
----+---------+-------
  3 | cabbage |    50
  4 | kales   |    30
(2 rows)

vegetable_store=# DELETE FROM vegetables WHERE name = 'kales';
DELETE 1
vegetable_store=# SELECT * FROM vegetables;
 id |  name   | price 
----+---------+-------
  3 | cabbage |    50
(1 row)
```
- Example of using delete similar to truncate, it deletes the rows:

```
vegetable_store=# DELETE FROM vegetables ;
DELETE 1
vegetable_store=# SELECT * FROM vegetables;
 id | name | price 
----+------+-------
(0 rows)
```
**12. JOIN**
- Combines rows from two or more tables based on a related column

```
management_db=# SELECT e.name, d.department_name
FROM employee e
INNER JOIN department d
ON e.department_id = d.department_id;
 name  | department_name 
-------+-----------------
 Lucy  | IT
 Glory | HR
 John  | Sales
 Mary  | Marketing
(4 rows)
```

**13. LEFT JOIN**
- Returns all records from the left table and matched records from the right table. 
- Unmatched right table rows return NULL.

```
management_db=# SELECT e.name, e.department_id, d.department_name
FROM employee e
LEFT JOIN department d
ON e.department_id = d.department_id;
 name  | department_id | department_name 
-------+---------------+-----------------
 Lucy  |            20 | IT
 Glory |            21 | HR
 John  |            22 | Sales
 Mary  |            23 | Marketing
 Peter |               | 
(5 rows)
```


**14. RIGHT JOIN**
- A RIGHT JOIN keeps all rows from the table on the RIGHT side of the JOIN, and only matching rows from the LEFT table.

```
management_db=# SELECT e.name, d.department_id, d.department_name
FROM employee e
RIGHT JOIN department d 
ON e.department_id = d.department_id;
 name  | department_id | department_name 
-------+---------------+-----------------
 Lucy  |            20 | IT
 Glory |            21 | HR
 John  |            22 | Sales
 Mary  |            23 | Marketing
       |            24 | Finance
(5 rows)
```

**15. OUTER JOIN**
- Return every row from both tables, matching where possible, and show NULL where no match exists.”

```
management_db=# SELECT e.name, d.department_id, d.department_name
FROM employee e
FULL OUTER JOIN department d
ON e.department_id = d.department_id ;
 name  | department_id | department_name 
-------+---------------+-----------------
 Lucy  |            20 | IT
 Glory |            21 | HR
 John  |            22 | Sales
 Mary  |            23 | Marketing
       |            24 | Finance
 Peter |               | 
(6 rows)
```
