## SQL Datatypes

    Signed & Unsigned
    TINYINT UNSIGNED (0 TO 255)
    TINYINT (-128 TO 127)

## Types of SQL Commands

    - DDL Data Definition Langauage : create, alter, rename, truncate & drop
    - DQL Data Query Language : select
    - DML Data Manipulation Language : insert, update & delete
    - DCL Data Control Language : grant & revoke permission to users
    - TCL Transaction Control Language : start transaction, commit, rollback

## Database related Queries

```
CREATE DATABASE db_name;
CREATE DATABASE IF NOT EXIST db_name;

DROP DATABASE db_name;
DROP DATABASE IF EXISTS db_name;

SHOW DATABASES;
SHOW TABLES;
```

## Table related queries

```
1.
CREATE TABLE table_name (
    column_name1 datatype constraint,
    column_name2 datatype constraint
)

-- primary key can't be null

CREATE TABLE student (
	id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT NOT NULL
)

2.
SELECT * FROM table_name;

3.
INSERT INTO
table_name (colname1, colname2)
VALUES (col1val1, col2val1), (col1val2, col2val2)

for adding just one row
INSERT INTO table_name VALUES(val1, val2, val3);
```

## KEYS

    Primary Key:
    it is a column (or set of columns) in a table that uniquely identifies each row like (unique id). There is only 1 PK $ it should be NOT NULL.

    Foreign Key:
    it is a column(or set of columns) in a table that refers to the primary key in another table. There can be multiple FKs. Fks can have duplicate & null values.

## Constraints

    1. NOT NULL: VALUE CAN'T BE NULL

    2. UNIQUE: ALL VALUES IN COLUMN ARE DIFFERENT

    3. PRIMARY KEY : unique and not null but if it is set for one column. And if more than one column combo is primary key then one of the col could be duplicate but combo of both would not be.
    Like: id: 101, 102, 101
          pet: me,  he,  he
    PRIMARY KEY (id, pet);

    4. foreign key:
    FOREIGN KEY (cust_id) references customer(id);
    cust_id: new table column
    customer(id): old table col where foreign key is Pk

    5. DEFAULT : salary INT DEFAULT 23000;

    6. CHECK:
    CREATE TABLE city (
    id INT PRIMARY KEY,
    city VARCHAR(50),
    age INT,
    CONSTRAINT age_check CHECK (age >= 18 AND city = "Delhi")
    );

    for single check:
    CREATE TABLE newTab (
        age INT CHECK (age >= 18)
    );

## SELECT IN DETAIL

    - SELECT col1, col2 FROM table_name;
    - SELECT * FROM table_name; -- to select all
    - SELECT DISTINCT col FROM table_name; --> it is for unique values

## WHERE CLAUSE CONDITION

    SELECT * FROM city WHERE (age > 24 AND city = "Delhi");

    ** Operators in Where
    1. Arithmetic
    2. Comparison
    3. Logical
    4. Bitwise

    Between: BETWEEN 80 AND 90; --> range from 80 to 90.

    In: IN ("delhi", "mumbai"); --> matches any value in the list.

    Not: NOT IN("", "")

## LIMIT Clause

    sets an upper limit on number of tuples or rows to be returned

    SELECT * FROM city LIMIT 3;
    SELECT col1, col2 FROM table_name LIMIT number;

    LIMIT should be in the end of query.

## ORDER BY Clause

    To sort in ascending (ASC) or descending order (DESC)

    SELECT col1, col2 FROM table_name ORDER BY col_name ASC;

## Aggregate Functions

    aggregate functions perform a calcutlation on a set of values, and return a single value.

    1. COUNT()
    2. MAX()
    3. MIN()
    4. SUM()
    5. AVG()

    SELECT MAX(column) FROM table_name;

## GROUP BY Clause

    It collects data from multiple records and groups the result by one or more column.
    *generally we use group by with some aggregation function.

    SELECT city, count(age) FROM city GROUP BY city;

    SELECT city, AVG(age) FROM city GROUP BY city ORDER BY AVG(age) ASC ;
    --> this query make group of cities and avg of age in those cities with ascending order by age.

## HAVING Clause

    SELECT city, count(id) FROM city GROUP BY city HAVING MAX(age) > 28;

    similar to where clause i.e. applies some condition on rows.
    but Having is used to apply any condition after grouping.

## General Order

    1. SELECT column
    2. FROM
    3. WHERE
    4. GROUP BY
    5. HAVING
    6. ORDER BY

## Table Related Queries

    safe-mode: SET sql_safe_updates=0; //false
    1. UPDATE
    UPDATE  table_name
    SET col1 = val1, col2 = val2
    WHERE condition;

    2. DELETE
    DELETE FROM table_name WHERE condition;
    * use it carefully.

## Cascading : UPDATE | DELETE

    CREATE TABLE student (
        id INT PRIMARY KEY,
        courseID INT,
        FOREIGN KEY(courseID) REFERENCES course(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
    )

## ALTER to change the schema

    1. ADD column
    ALTER TABLE table_name
    ADD COLUMN col datatype constraint;

        MODIFY age VARCHAR(2); --> to modify existing col schema
        CHANGE age cap_age INT; --> to rename column

    2. DROP column
    ALTER TABLE table_name
    DROP COLUMN col;

    3. RENAME table
    ALTER TABLE table_name
    RENAME TO new_table_name

    4. TRUNCATE:
        to delete table's data unlike drop which delete the table itself.

        TRUNCATE TABLE  table_name;

## A small practice table:

```
CREATE TABLE student (
	id INT PRIMARY KEY NOT NULL,
    name VARCHAR(30) NOT NULL,
    roll_no INT UNIQUE,
    marks INT NOT NULL,
    grades VARCHAR(2)
);

INSERT INTO student
(id, name, roll_no, marks, grades)
VALUES
(1, "rajesh", 11, 86, "B"),
(2, "simran", 13, 89, "B"),
(3, "komal", 15, 78, "C"),
(4, "sahil", 14, 91, "A"),
(6, "manoj", 17, 63),
(5, "rekha", 16, 46, "");

ALTER TABLE student
CHANGE name full_name VARCHAR(30);

SET sql_safe_updates=0;
DELETE FROM student
WHERE marks < 80;

ALTER TABLE student
DROP grades;

SELECT * FROM student;

```

## JOINS in SQL

    join is used to combine rows from two or more tables, based on a related column between them.

    ## Venn diagrams
    inner join
    Outer Join
        - left join, right join, full join

## Inner JOIN

        A           B
    |-------|---|-------|
    |       |---|       |
    |-------|---|-------|
              ⬇
    RETURNS COMMON/MATCHING DATA FROM BOTH A & B TABLE based on same column data in both tables.

    Syntax:
    SELECT column(s)
    FROM tableA
    INNER JOIN tableB
    ON tableA.col_name = tableB.col_name

## Left JOIN

        A           B
    |-------|---|-------|
    |-------|---|       |
    |-------|---|-------|
       ⬇      ⬇
    returns all records from the left table and the matched records from the right table.

    Syntax:
    SELECT column(s)
    FROM tableA
    LEFT JOIN tableB
    ON tableA.col_name = tableB.col_name

    same thing goes for right join.

## full join:

    it doesn't exist in mySql but

    LEFT JOIN
    UNION
    RIGHT JOIN

## LEFT EXCLUSIVE JOIN

## RIGHT EXCLUSIVE JOIN

## SELF JOIN

    it is a regular join but the table is joined with itself

    Syntax:
    SELECT column(s)
    FROM table as a
    JOIN table as b
    ON a.col_name = b.col_name;

## UNION && UNION ALL

    UNION ALL contain duplicated too

## View in SQL
