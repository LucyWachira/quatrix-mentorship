
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
**16. VIEW**
- Its a virtual table created based on a SELECT query.
- It does not store data, it stores the query.
- To create a view:
```
CREATE VIEW StudentView AS
SELECT NAME, ADDRESS
FROM StudentDetails;
SELECT * FROM StudentView;
```

- Example from the tables earlier created:

```
management_db=# CREATE VIEW management_view AS
management_db-# SELECT e.name, d.department_name
management_db-# FROM employee e
management_db-# INNER JOIN department d
management_db-# ON e.department_id = d.department_id;
CREATE VIEW
management_db=# SELECT * FROM management_view ;
 name  | department_name 
-------+-----------------
 Lucy  | IT
 Glory | HR
 John  | Sales
 Mary  | Marketing
(4 rows)
```

- You can also use View to update or delete.
- Example I want to update the employees table by adding e.name Grace and the department_id = 25

```
management_db=# INSERT INTO employee_view (name, department_id)
VALUES ('Grace', 25);
INSERT 0 1
management_db=# SELECT * FROM employee_view ;
 name  | department_id 
-------+---------------
 Lucy  |            20
 Glory |            21
 John  |            22
 Mary  |            23
 Peter |              
 Grace |            25
(6 rows)
```
- I can also update an existing employee :

 ```
management_db=# SELECT * FROM employee_view ;
 name  | department_id 
-------+---------------
 Lucy  |            20
 Glory |            21
 John  |            22
 Mary  |            23
 Peter |              
 Grace |            25
(6 rows)

management_db=# UPDATE employee_view 
management_db-# SET department_id =26
management_db-# WHERE name = 'Peter' ;
UPDATE 1
management_db=# SELECT * FROM employee_view ;
 name  | department_id 
-------+---------------
 Lucy  |            20
 Glory |            21
 John  |            22
 Mary  |            23
 Grace |            25
 Peter |            26
(6 rows)
 ```


-  I can also delete a row in a view:- to delete the recently added row for Grace:

```
management_db=# DELETE FROM employee_view 
management_db-# WHERE name = 'Grace' ;
DELETE 1
management_db=# SELECT * FROM employee_view ;
 name  | department_id 
-------+---------------
 Lucy  |            20
 Glory |            21
 John  |            22
 Mary  |            23
 Peter |            26
(5 rows)
```
- To delete a row entry: e.g to delete the department_id for peter:

```
management_db=# UPDATE employee_view 
management_db-# SET department_id = NULL
management_db-# WHERE name = 'Peter' ;
UPDATE 1
management_db=# SELECT * FROM employee_view ;
 name  | department_id 
-------+---------------
 Lucy  |            20
 Glory |            21
 John  |            22
 Mary  |            23
 Peter |              
(5 rows)
```
- To list the views created use: `\dv`
```
management_db=# \dv
               List of views
 Schema |      Name       | Type |  Owner   
--------+-----------------+------+----------
 public | employee_view   | view | postgres
 public | management_view | view | postgres
(2 rows)
```
- To see the query in that view use :
`management_db=# \d+ employee_view`

- To delete a view:
```
management_db=# DROP VIEW employee_view ;
DROP VIEW
```
**17. BEGIN**
- Used to initiate a transaction block, all statements after BEGIN command will be executed in a single transaction until COMMIT or ROLLBACK.
- Transaction is a group of SQL statements treated as one single unit of work.
  - BEGIN - STARTS A transaction.
  - COMMIT - saves changes permanently
  - ROLLBACK - undoes all changes since begin.

**18. SAVEPOINT**
- It is a keyword used inside a transaction to create a checkpoint that you can rollback without cancelling the entire transaction.
- Allows you to undo a part of a transaction not all of it.
- **Importance** - ROLLBACK - undoes everything since BEGIN while SAVEPOINT- Undo only the part that went wrong.
**19. LIMIT**
- Used to specify the number of records to return.

**20. What is the difference between BEGIN and START TRANSACTION?**
- Start transaction is used as a standard SQL syntax.
- Begin is common to postgresql and MYSQL.
- Start transaction adds a transactional mode (optional)
  - READ WRITE
  - READ ONLY

#### What is normalization?
- Normalization is an important process in database design that helps improve the database's efficiency, consistency, and accuracy. It makes it easier to manage and maintain the data and ensures that the database is adaptable to changing business needs.
- It is the process of organizing data within a database, breaking down a large complex table into smaller and simple tables while maintaining data relationships.

#### Purpose and Benefits

1. Reduce data redundancy: Prevents the same data from being stored in multiple places, saving storage space.
2. Prevent anomalies: Minimizes insertion, update, and deletion anomalies that occur with poorly structured data.
3. Simplify maintenance: Makes the database easier to maintain and modify, as changes only need to be applied in a single location. 
1. First Normal Form (1NF)
- Goal: Eliminate repeating groups and make sure each column contains atomic (indivisible) values.
- Rules:Each column must hold only one value and Each row must be unique.No repeating groups or arrays.

| StudentID | Name | Courses       |
| --------- | ---- | ------------- |
| 1         | Lucy | Math, English |
| 2         | John | Physics, Math |

- 1NF Solution: Split the courses into separate rows.

| StudentID | Name | Course  |
| --------- | ---- | ------- |
| 1         | Lucy | Math    |
| 1         | Lucy | English |
| 2         | John | Physics |
| 2         | John | Math    |

2. 2NF Solution: Split into two tables.
- The student-course table:

| StudentID | Course  |
| --------- | ------- |
| 1         | Math    |
| 1         | English |
| 2         | Math    |

- Instructor table:

| Course  | Instructor | InstructorPhone |
| ------- | ---------- | --------------- |
| Math    | Mr. A      | 12345           |
| English | Ms. B      | 54321           |

3. Third Normal Form (3NF)
- Goal: Remove transitive dependency.
- Non-key columns should depend only on the primary key, not on another non-key column.
- Example:

| StudentID | Name | Dept    | DeptHead |
| --------- | ---- | ------- | -------- |
| 1         | Lucy | Science | Dr. K    |
| 2         | John | Math    | Dr. M    |

- Problem: DeptHead depends on Dept, not on StudentID.
- 3NF Solution: Split into two tables.

1. students table:

| StudentID | Name | Dept    |
| --------- | ---- | ------- |
| 1         | Lucy | Science |
| 2         | John | Math    |

2. Departments

| Dept    | DeptHead |
| ------- | -------- |
| Science | Dr. K    |
| Math    | Dr. M    |

- Transitive dependency removed.

### Create a Database, Table and Insert Records


1. Option #1 - create the database, create your user account and transfer ownership to your user eg. pomollo:
- Create a database and called exam:
`CREATE DATABASE exam;`

- Create a user with the username identical to the username on your local Debian PC e.g.:
`CREATE USER pomollo WITH ENCRYPTED password `replaceThisWithApasswordOfYourChoice`;`

- Transfer ownership of exam to yourself eg:
`ALTER DATABASE exam OWNER TO pomollo;`

- **Example**
```
lwachira@lwachira:~$ sudo -u postgres psql
psql (18.1 (Debian 18.1-1.pgdg12+2))
Type "help" for help.

postgres=# CREATE DATABASE exam;
CREATE DATABASE
postgres=# CREATE USER lwachira WITH ENCRYPTED password 'Lwach1ra';
CREATE ROLE
postgres=# ALTER DATABASE exam OWNER TO lwachira ;
ALTER DATABASE
postgres=# \l
postgres=# 
```

- Option #1 - Test to see if you can access the database from your account:
`psql -d exam`

2. Re-run the generate script exactly as you did in the bash module (NB: This is done outside psql i.e. in bash or zsh):
`./util/generate_exam_data.sh`
```
lwachira@lwachira:~/Documents/git/quatrix-mentor$ ./util/generate_exam_data.sh
Generating Exam data. Please wait... 100%
```
### Query Questions

**1. Display students named Alice.**

`exam=> SELECT * FROM student WHERE name LIKE 'Alice%' ;`

**2. How many students are from Mombasa (count_id=1) county?**

- This one displays all the students from county number=1
`exam=> SELECT * FROM student WHERE county_id =1;`
- To count the total number of students:
```
SELECT COUNT (*) AS total_students FROM student WHERE county_id =1;
```
**3. How many students are from each of the counties?**
```
SELECT county_id, COUNT (*) AS total_students  FROM student
GROUP BY county_id
ORDER BY county_id ASC;
```
**4. Write a query that averages the scores of each student. Hints to assist you:**

- Use the student_subject table for this query.
- To average and round off the resultant to 4 decimal places, use the following function that includes a CAST operation:
- `ROUND(CAST(float8(AVG(score)) as numeric),4) as ave_score`

NB: The topic casting will not be covered in this SQL/Database module but understanding it could be helpful

```
SELECT student_id, AVG(score) AS average_score
FROM student_subject 
GROUP BY student_id
ORDER BY student_id ASC;
```
- To Round off the number:

```
SELECT student_id,ROUND(CAST(float8(AVG(score)) as numeric),4) AS ave_score
FROM student_subject 
GROUP BY student_id
ORDER BY student_id ASC;
```

**5. Do a select query where you show the . after the middle initial eg. Amber C Kimani should be displayed as Amber C. Kimani etc.**

```
SELECT name, REGEXP_REPLACE (name, '([A-Z][a-z]+)\s([A-Z])\s([A-Z][a-z]+)', '\1 \2. \3') AS formatted_name FROM student;
```

**6. Generate a select query that will show potential usernames for each student by combining first letter of first name, middle initial and lastname and last 4 digits of their phone number.**
-  eg.
Student with the following details:
Amber C. Atieno 0783-627-886
Should generate a username such as (use lowercase for all characters):
acatieno7886
- Display this username as an additional column/field - username.

```
SELECT
    name,
    phone,
    REGEXP_REPLACE(
        name,
        '([A-Z][a-z]+)\s([A-Z])\s([A-Z][a-z]+)',
        '\1 \2. \3'
    ) AS formatted_name,
LOWER(
SUBSTRING(name FROM '^([A-Z])') ||
SUBSTRING(name FROM '\s([A-Z])\s') ||
SUBSTRING(name FROM '([A-Z][a-z]+)$') ||
RIGHT(REGEXP_REPLACE(phone, '\D','','g'),4)
) AS username FROM student;
```


### Queries involving Multiple Tables - utilizing SQL JOINS

**1. Display students with name Ami with an average score of 90% and above.**

```
SELECT s.name, AVG (ss.score)
FROM student s
INNER JOIN student_subject ss
ON s.id = ss.student_id
WHERE s.name LIKE 'Ami%'
GROUP BY s.id, s.name
HAVING AVG(ss.score) >=90;
```
- OUTPUT
```
     name      |        avg        
----------------+-------------------
 Ami P Nuru     |           90.9307
 Ami W Nuru     | 93.71068333333335
 Ami C Yebo     | 95.00277142857144
 Ami P Kamau    | 93.98751666666668
 Ami W Otieno   |          93.95166
 Ami P Maribe   | 92.10785000000001
 Ami L Otieno   |          93.62736
 Ami L Wambugu  | 94.40417142857143
 Ami W Wanyonyi | 90.25220000000002
 Ami L Ratemo   | 92.12822499999999
 Ami C Kamau    |           90.7693
 Ami P Idris    | 92.50361428571429
 Ami P Ouma     | 93.03051666666666
(13 rows)
```
- To round off the decimal places:
```
SELECT s.name, ROUND(CAST(float8(AVG(score)) as numeric),4) as ave_score
FROM student s
INNER JOIN student_subject ss
ON s.id = ss.student_id
WHERE s.name LIKE 'Ami%'
GROUP BY s.id, s.name
HAVING AVG(ss.score) >=90;
```

**2. What are the averages scores per county?**

```
SELECT c.id, c.name, AVG(ss.score)
FROM county c
JOIN student s
ON c.id = s.county_id
JOIN student_subject ss
ON s.id = ss.student_id
GROUP BY c.id, c.name
ORDER BY c.id;
```

**3. List all students from Turkana county. Display only the following fields: id, name and their school name.**

```
SELECT s.id, s.name, sc.name
FROM student s
JOIN school sc
ON s.school_id = sc.id
JOIN county c
ON c.id = sc.county_id
WHERE c.name = 'Turkana' ;
```
- OUTPUT:
```
 id  |         name         |         name         
------+----------------------+----------------------
 1026 | Amber K Maxx         | Turkana - Homeschool
 1085 | Amber W Ouma         | Turkana - District
 1199 | Alice K Atieno       | Turkana - Homeschool
 1224 | Alice L Maxx         | Turkana - Homeschool
 1233 | Alice L Yegon        | Turkana - Homeschool
 1249 | Alice P Wambugu      | Turkana - Homeschool
 1367 | Conrad C Maribe      | Turkana - Homeschool
 1400 | Conrad L Kamau       | Turkana - District
 1443 | Conrad W Nuru        | Turkana - Provincial
 1541 | Elizabeth C Atieno   | Turkana - Provincial
 1559 | Elizabeth K Atieno   | Turkana - Homeschool
 1574 | Elizabeth K Wanyonyi | Turkana - Homeschool
 ```



**4. List the top students for each subject in the country, include their county name and school name.**

```
SELECT sub.name AS subject_name, s.name AS student_name, c.name AS county_name, sc.name AS school_name               
FROM student_subject ss
JOIN student s ON s.id = ss.student_id
JOIN subject sub ON sub.id = ss.subject_id
JOIN school sc ON sc.id = s.school_id
JOIN county c ON c.id = s.county_id WHERE (ss.subject_id, ss.score)
IN (
SELECT ss.subject_id, MAX(ss.score)
FROM student_subject ss
GROUP BY ss.subject_id
) ;
```

**5. List the top 10 students in the country. Use the average score of all their subjects. Include a field that shows their ranks ie 1 to 10. Additionally, list the county and school name.**

**6. List the top schools (school name, total number of students in each school and county name) based on type/category ie top school:**
 - Homeschool
 -  National
 - Provincial
 - District
 -  Private


```
SELECT * FROM ( 
 SELECT sc.name AS school_name, 'National' AS school_type, c.name AS county_name, COUNT(s.id) AS total_students
FROM school sc
JOIN student s ON s.school_id = sc.id
JOIN student_subject ss ON ss.student_id = s.id
JOIN county c ON c.id = sc.county_id
WHERE sc.name LIKE '%National%'
GROUP BY sc.id, sc.name, c.name
ORDER BY AVG(ss.score) DESC
LIMIT 1
) national
UNION ALL
SELECT * FROM (
SELECT sc.name AS school_name, 'Homeschool' AS school_type, c.name AS county_name, COUNT(s.id) AS total_students
FROM school sc
JOIN student s ON s.school_id = sc.id
JOIN student_subject ss ON ss.student_id = s.id
JOIN county c ON c.id = sc.county_id
WHERE sc.name LIKE '%Homeschool%'
GROUP BY sc.id, sc.name, c.name
ORDER BY AVG(ss.score) DESC
LIMIT 1 ) homeschool
UNION ALL
SELECT * FROM (
SELECT sc.name AS school_name, 'Provincial' AS school_type, c.name AS county_name, COUNT(s.id) AS total_students
FROM school sc
JOIN student s ON s.school_id = sc.id
JOIN student_subject ss ON ss.student_id = s.id
JOIN county c ON c.id = sc.county_id
WHERE sc.name LIKE '%Provincial%'
GROUP BY sc.id, sc.name, c.name
ORDER BY AVG(ss.score) DESC
LIMIT 1
) provincial
UNION ALL
SELECT * FROM (
SELECT sc.name AS school_name, 'District' AS school_type, c.name AS county_name, COUNT(s.id) AS total_students
FROM school sc
JOIN student s ON s.school_id = sc.id
JOIN student_subject ss ON ss.student_id = s.id
JOIN county c ON c.id = sc.county_id
WHERE sc.name LIKE '%District%'
GROUP BY sc.id, sc.name, c.name
ORDER BY AVG(ss.score) DESC
LIMIT 1
) district
UNION ALL
SELECT * FROM (
SELECT sc.name AS school_name, 'Private' AS school_type, c.name AS county_name, COUNT(s.id) AS total_students
FROM school sc
JOIN student s ON s.school_id = sc.id
JOIN student_subject ss ON ss.student_id = s.id
JOIN county c ON c.id = sc.county_id
WHERE sc.name LIKE '%Private%'
GROUP BY sc.id, sc.name, c.name
ORDER BY AVG(ss.score) DESC
LIMIT 1 
) private ;
```

**7. Similar to above query, list the top student from each school type.**

```
SELECT * FROM (
    SELECT
        s.name AS student_name,
        'National' AS school_type,
        sc.name AS school_name,
        c.name AS county_name,
        ROUND(CAST(AVG(ss.score) AS numeric), 2) AS average_score
    FROM student s
    JOIN student_subject ss ON ss.student_id = s.id
    JOIN school sc ON s.school_id = sc.id
    JOIN county c ON c.id = sc.county_id
    WHERE sc.name LIKE '%National%'
    GROUP BY s.id, s.name, sc.name, c.name
    ORDER BY AVG(ss.score) DESC
    LIMIT 1 
) national 
UNION ALL
SELECT * FROM (
    SELECT
        s.name AS student_name,
        'Homeschool' AS school_type,
        sc.name AS school_name,
        c.name AS county_name,
        ROUND(CAST(AVG(ss.score) AS numeric), 2) AS average_score
    FROM student s
    JOIN student_subject ss ON ss.student_id = s.id
    JOIN school sc ON s.school_id = sc.id
    JOIN county c ON c.id = sc.county_id
    WHERE sc.name LIKE '%Homeschool%'
    GROUP BY s.id, s.name, sc.name, c.name
    ORDER BY AVG(ss.score) DESC
    LIMIT 1 
) Homeschool
UNION ALL
SELECT * FROM (
    SELECT
        s.name AS student_name,
        'Provincial' AS school_type,
        sc.name AS school_name,
        c.name AS county_name,
        ROUND(CAST(AVG(ss.score) AS numeric), 2) AS average_score
    FROM student s
    JOIN student_subject ss ON ss.student_id = s.id
    JOIN school sc ON s.school_id = sc.id
    JOIN county c ON c.id = sc.county_id
    WHERE sc.name LIKE '%Provincial%'
    GROUP BY s.id, s.name, sc.name, c.name
    ORDER BY AVG(ss.score) DESC
    LIMIT 1 
 ) Provincial
 UNION ALL
SELECT * FROM (
    SELECT
        s.name AS student_name,
        'District' AS school_type,
        sc.name AS school_name,
        c.name AS county_name,
        ROUND(CAST(AVG(ss.score) AS numeric), 2) AS average_score
    FROM student s
    JOIN student_subject ss ON ss.student_id = s.id
    JOIN school sc ON s.school_id = sc.id
    JOIN county c ON c.id = sc.county_id
    WHERE sc.name LIKE '%District%'
    GROUP BY s.id, s.name, sc.name, c.name
    ORDER BY AVG(ss.score) DESC
    LIMIT 1 
 ) District
UNION ALL
SELECT * FROM (
    SELECT
        s.name AS student_name,
        'Private' AS school_type,
        sc.name AS school_name,
        c.name AS county_name,
        ROUND(CAST(AVG(ss.score) AS numeric), 2) AS average_score
    FROM student s
    JOIN student_subject ss ON ss.student_id = s.id
    JOIN school sc ON s.school_id = sc.id
    JOIN county c ON c.id = sc.county_id
    WHERE sc.name LIKE '%Private%'
    GROUP BY s.id, s.name, sc.name, c.name
    ORDER BY AVG(ss.score) DESC
    LIMIT 1 ) private;
```


### Update Data Questions

- The following involve updating records, tables, or deleting records. Make use of database transactions to be safe.

**1. Delete all records for students with the name Joan and be careful not to delete Joanne**

- To match only Joan and not Joanne: 

```
SELECT * FROM student
WHERE name LIKE 'Joan %' ;
```
- To match both: `Joan%' without a space.

- Here are the steps to delete Joan since the student has rows in the student_subject table. The student_id is the foreign key in the student_subject table.
```
BEGIN;

-- Step 1: see affected students
SELECT * FROM student
WHERE name LIKE 'Joan %';

-- Step 2: delete dependent records
DELETE FROM student_subject
WHERE student_id IN (
    SELECT id
    FROM student
    WHERE name LIKE 'Joan %'
);

-- Step 3: delete students
DELETE FROM student
WHERE name LIKE 'Joan %';

-- Step 4: commit if correct
COMMIT;

-- or ROLLBACK if unsure
```

**2. Update all students names to UPPERCASE so that e.g. Amber K Ratemo becomes AMBER K RATEMO**

```
BEGIN;

UPDATE student
SET name = UPPER(name);

-- If everything looks good
COMMIT;

-- Or, to undo
-- ROLLBACK;
```


**3. Update all county names to UPPERCASE.**

```
BEGIN;

UPDATE county
SET name = UPPER(name);

-- If everything looks good
COMMIT;

-- Or, to undo
-- ROLLBACK;
```

**4. Update all phone numbers so that they change from format 0707-155-302 to format 254707155302**

```
BEGIN;
SELECT * FROM student;
UPDATE student
SET phone = '254' || REGEXP_REPLACE(phone, '^0|\D', '', 'g');
SELECT * FROM student;
COMMIT;
```

**5. Update records for students from TRANS, THARAKA and WEST counties so that they read TRANS-NZOIA, THARAKA-NITHI and WEST-POKOT respectively.**

```
BEGIN;
UPDATE county SET name = 'TRANS-NZOIA' WHERE name = 'TRANS'
UPDATE county SET name = 'THARAKA-NITHI' WHERE name = 'THARAKA'
;
UPDATE county SET name = 'WEST-POKOT' WHERE name = 'WEST'
;
SELECT * FROM county ;
COMMIT;
```


**6. Update all students with ALICE .... to ALLISA.**

```
BEGIN;

-- Update only the first name from ALICE to ALLISA, keeping middle & last names

UPDATE student
SET name = 'ALLISA' || SUBSTRING(name FROM 6)  -- keep characters from position 6 onwards

WHERE name LIKE 'ALICE%';

SELECT * FROM student WHERE name LIKE 'ALLISA%';

ROLLBACK;  -- use COMMIT if you are happy with changes
```



- This will only change the first name and exempt the middle and last name.
```
BEGIN;
SELECT * FROM student WHERE name LIKE 'ALICE%';
UPDATE student SET name = 'ALLISA' WHERE name LIKE 'ALICE%';
SELECT * FROM student WHERE name LIKE 'ALLISA%';
COMMIT;
```


**7. Write an SQL query where that shows the letter grade using the following scale - If a student's average score is between:**

95 and 100 then the grade => 'A'
90 and 95 then the grade => 'A-'
85 and 90 then the grade => 'B+'
80 and 85 then the grade => 'B'
75 and 80 then the grade => 'B-'
70 and 75 then the grade => 'C+'
65 and 70 then the grade => 'C'
60 and 65 then the grade => 'C-'
55 and 60 then the grade => 'D+'
50 and 55 then the grade => 'D'
49 and below, the grade => 'FAIL'


```
SELECT
    s.id,
    s.name,
    ROUND(AVG(ss.score)) AS score,
    CASE
        WHEN AVG(ss.score) BETWEEN 95 AND 100 THEN 'A'
        WHEN AVG(ss.score) >= 90 THEN 'A-'
        WHEN AVG(ss.score) >= 85 THEN 'B+'
        WHEN AVG(ss.score) >= 80 THEN 'B'
        WHEN AVG(ss.score) >= 75 THEN 'B-'
        WHEN AVG(ss.score) >= 70 THEN 'C+'
        WHEN AVG(ss.score) >= 65 THEN 'C'
        WHEN AVG(ss.score) >= 60 THEN 'C-'
        WHEN AVG(ss.score) >= 55 THEN 'D+'
        WHEN AVG(ss.score) >= 50 THEN 'D'
        ELSE 'FAIL'
    END AS grade
FROM student s
JOIN student_subject ss
    ON ss.student_id = s.id
GROUP BY s.id, s.name
ORDER BY s.id;
```                       

### Securing PostgreSQL Databases

**1. What type of authentication did we utilize in the above user creation ie given that we have matched the database user to the Linux system username?**

- PEER authentication method - it checks your system username, so if your linux username matches the postgresql user, you can login without a password.

**- Other Authentication methods**
- Ident authentication method - similar to peer but works over the network, asks the OS of the connecting machine who the user is , then maps to the DB user.

- scram-sha-256 - it is password based authentication method , uses database password, you type your password on your computer , your computer keeps the password locally and the server checks if it is correct.

- md5 - it is a password based authentication method, postgresql asks for a database password and verifies it using an md5hash, postgresql compares it with the stored hash, if its a match the login succeeds.

### Accessing a Remote Database (Traccar)

- You will need to access the test.traccar database for the following questions. We will access the test.traccar database using ssh tunneling as outlined below: Create an ssh tunnel to test.traccar server:

```
ssh -f -o ExitOnForwardFailure=yes -L 63333:localhost:5432 yourusername@test.traccar.quatrixglobal.com sleep 30
Connect to traccar database:
```
```
psql -d traccar -h localhost -p 63333 -U yourUsername
```
- You will be prompted to enter a password: ``` wachira1234```

- Proceed to generate the following reports using SQL:

**1. All devices and their corresponding groups using one query.**


```
SELECT name, category AS groups 
FROM tc_devices;
```
**2. All position data for the last one day. Should include the vehicle, the group**

```
SELECT 
    p.*,
    d.name AS vehicle,
    d.category AS groups
FROM tc_positions p
JOIN tc_devices d
    ON p.deviceid = d.id
WHERE p.servertime >= NOW() - INTERVAL '1 day'
ORDER BY p.servertime DESC;
```
**3. All devices that are not motorcycles and not trucks.**

```
SELECT 
    name AS vehicle,
    category AS groups
FROM tc_devices
WHERE category NOT IN ('motorcycle', 'truck');
```
- Since there are truck and Truck, to remove both use :

```
SELECT 
    name AS vehicle,
    category AS groups
FROM tc_devices
WHERE category NOT ILIKE 'motorcycle'
  AND category NOT ILIKE 'truck';
```

### Give Access to Other Users to exam Database
- Create a user account/role for a fellow mentee (if you're a remote Quatrix mentee, the admin will suggest a fellow mentee's names). The following should apply:

Ensure they can access the database using Ident Authentication meaning they should also have a regular Linux system user account on your local PC.
Give them read only access to the exam database.

1. Create postgresql role for jdoe.
```CREATE ROLE jdoe LOGIN;```

2. Allow jdoe to connect to exam database:
```GRANT CONNECT ON DATABASE exam TO jdoe;```

3. Connect to exam database:
```\c exam```

4. Give schema Access:
```GRANT USAGE ON SCHEMA public TO jdoe;```

5. Give Read only access to the exam database:
 ```GRANT SELECT ON ALL TABLES IN SCHEMA public TO jdoe;```
 6. Ensure Ident Authentication is Enabled: 

```sudo vi /etc/postgresql/18/main/pg_hba.conf```
- Add:
``` 
# "local" is for Unix domain socket connections only
local   all             all                                     peer
local   exam            jdoe                                    ident
```
- Test jdoe access: ```sudo -u jdoe psql -d exam```
- To check permissions: \du , \dp