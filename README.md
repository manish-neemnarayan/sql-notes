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
