# PostgreSQL Notes

#### What is a database ?

**Answer**: An organised collection of data . A method to manipulate and access the data 

#### Database vs DBMS ?

**Answer**:

![](../Assets/database-vs-DBMS.png)

#### What is RDBMS ?

**Answer**:

A type of database system that stores data in structured tables(using rows and columns ) and uses SQL for managing and querying data

#### What is SQL ?

**Answer**:

Structured Query Language which is used to talk to our databases

Example : SELECT * FROM person_db;

#### Basic Installation steps

**Answer**:

psql => Enter the postgresql shell

\conninfo => connection info

\q => quits the shell

\l => lists all the databases

CREATE DATABASE TEST; => creates a database called TEST

ctrl + L => clears screen 

#### Dropping a database

**Answer**:

To drop a database use the following command : 

`drop database h` 
If we get the following error 

`ERROR: database "h" is being accessed by other users
There is 1 other session using the database. 
SQL state: 55006
Detail: There is 1 other session using the database.`

then terminate the sessions manually by 

`SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = 'h'
  AND pid <> pg_backend_pid();`

If we get this error : 

`ERROR: cannot drop the currently open database 
SQL state: 55006`

Then switch to another database and then drop the database 

#### CRUD Operations

Table : A table is a collection of related data held in a table format within a database 

First create a  database called *person_db*

**Creating a new Table***

```sql
CREATE TABLE person(

id INT,

name VARCHAR(100),

city VARCHAR(100)

```

**Inserting Data**

To insert data into a table use the following command 

```sql
INSERT INTO person (id,name,city)
values (201,'Suvadeep','Indore')
```

Note => We must pass 'Suvadeep' with single quotes because double quotes " are for column or table names in PostgreSQL


