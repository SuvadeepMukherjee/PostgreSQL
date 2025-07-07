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
);
```

**Inserting Data**

To insert data into a table use the following command 

```sql
INSERT INTO person (id,name,city)
values (101,'Suvadeep','Indore')
```

Note => We must pass 'Suvadeep' with single quotes because double quotes " are for column or table names in PostgreSQL

To insert multiple values 

```sql
insert into person (id,name,city)
values (102,'Sham','Mumbai'),
(103,'Paul','Chennai'),
(104,'Alex','Pune');
```

#### Reading data from a Table

To read data from a table run the following commands

```sql
select * from <table_name>;

select <column_name> from <table_name>;
```

Example 

```sql
select * from person;

select name from person;
```

#### Updating data

To update data run the following command 

```sql
update person set city ="london" where id =101
```

#### Delete data from a table

To delete data run the following command 

```sql
delete from person where id =102
```

#### Data Types

Data types => An attribute that specifies the type of data in a column of our database_table 

Most commonly used are 

Numerc - INT DOUBLE FLOAT DECIMAL 

String - VARCHAR

Date - DATE

Boolean - BOOLEAN

#### Constraint

A constraint in PostgreSQL Is a rule applied to a column

#### Primary Key

- The PRIMARY KEY constraint uniquely identifies each record in a table

- Primary keys must contain UNIQUE values , and cannot contain NULL values 

- A table can have only ONE primary key

#### Not Null

```sql
create table customers 

(

id int not null , 

name varchar(100) not null

)
```

#### Default Value

```sql
create table customers(

acc_no int primary key,

name varchar(100) not null,

acc_type varchar(50) not null default 'Savings'

)
```

#### Auto Increment

```sql
create table employees(

id serial primary key,

firstname varchar(50),

lastname varchar(50)

)
```

#### Task 1

Create Database bank_db

```sql
CREATE TABLE employees(

    emp_id SERIAL PRIMARY KEY,

    fname varchar(50) NOT NULL,

    lname varchar(50) NOT NULL,

    email varchar(100) NOT NULL UNIQUE,

    dept VARCHAR(50),

    salary DECIMAL(10,2) DEFAULT 30000.00,

    hire_date DATE NOT NULL DEFAULT CURRENT_DATE 

)
```
