---
published: true

layout: post
title: "Introduction to Database Management Systems"
date: 2019-06-27
description: Basic SQLite3 commands and DBMS concepts
img: db.jpg  
fig-caption: Database Management Systems
tags: [SQL, programming, database, big data, model]
---
A database is an organized collection of data that can be queried to retrieve information as needed. Structured Query Language or SQL (generally pronounced "sequel"), is a popular method for managing databases. Based on the relational model, SQL codifies a series of data tables and relations between them. In the following article, I'll show you how to quickly get started with your own database management system.

**Article contents:**
- TOC
{:toc}

<br>


## When to use (or not use) a DBMS
A **database management system (DBMS)** is a collection of programs that enables users to create and maintain a database. The database and software together form a database system. Popular DBMS's include:

![popular database management systems](../assets/img/sql_dbms.png)


What advantages does using a DBMS offer?
* A DBMS gives you insulation between your programs and your data.
* It can support multiple views of the data, assisting with having multiple user interfaces.
* Helps to control redundancy, which cuts down duplication of effort and unintended errors.
* A DBMS is useful for sharing data and processing transactions over multiple users.
* Keeping organized meta-data helps to describe the structure of the primary database.

When should you NOT use a DBMS?
* When you have a simple, well-defined database application that isn’t expected to change at all.
* When you don’t need multiple-user access to data.
* When the initial investment in hardware, software and training are too high.

Therefore, a DBMS is most useful when you have a variety of data that will be accessed in different ways by multiple users. But if your data management needs are modest or relatively uncomplicated, it may not be worth the time and effort to set up and maintain a DBMS.

To get an idea of these strengths and weaknesses, let's practice on a small database using SQLite3. If you already have python installed, then you likely already have SQLite3 available. You can check by typing in `sqlite3` into your command prompt. Optionally, you can follow this by the name of the database you wish to work on/create.

![sqlite3 command prompt](../assets/img/sqlite3_command_prompt.png)

(Note: this article is written from a Windows perspective, some commands may vary by OS).
<br>

# Structure of the Database
A **schema** describes the structure of a database. In SQL, the schema is defined through the use of **Data Definition Language (DDL)**. These DDL statements describe how data should reside within the database.

* `CREATE` – to create database and its objects (e.g. table, index, views, store procedure, function and triggers)
* `ALTER` – alters the structure of the existing database
* `DROP` – delete objects from the database

As an example, a DDL statement to create a new SQL table may look like:

{% highlight ruby %}
### Example - creating a table
CREATE TABLE table_name (
	field_name data_type constraint_name,
	field_name data_type constraint_name);
{% endhighlight %}


We can practice by using a DDL statement to create our first table in SQLite3. For this exercise, let's pretend that we are working for a doctor's office and we want to keep a file containing patient information.

{% highlight ruby %}
## Create table containing patient information
CREATE TABLE patients (
	patient_id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	firstname TEXT NOT NULL,
	lastname TEXT NOT NULL,
	age SMALLINT CHECK(age < 120),
	city TEXT NOT NULL,
	got_flu_shot BOOLEAN DEFAULT 0 );
{% endhighlight %}

Great! We've created a table, but it doesn't contain any information yet. To fill the table, we'll need the help of DML.

## Data Manipulation Language (DML)
Once you have created a database schema, **Data Manipulation Language** can be used to manipulate the information and try to gather meaningful insight. DML is used to store, modify, retrieve, delete and update data in database through statements such SELECT, INSERT, UPDATE, and DELETE, among others.
* `SELECT` – retrieve data from the a database
* `INSERT` – insert data into a table
* `UPDATE` – updates existing data within a table
* `DELETE` – Delete all records from a database table

To populate our table containing the structure for patient information, let's try using a DML `INSERT` statement:
{% highlight ruby %}
## Populate the table using INSERT
INSERT INTO patients values(1, 'Kevin', 'Smith', 30, 'Denver',0);
INSERT INTO patients values(2, 'Nancy','Smith', 25, 'Denver',0);
INSERT INTO patients values(3, 'David','Allan',73, 'Denver',0);
INSERT INTO patients values(4, 'Gerald','Tavish',52, 'Fort Collins',1);
INSERT INTO patients values(5, 'Jane','Hammond',32, 'Fort Collins',1);
INSERT INTO patients values(6, 'Karen','Daniels',42, 'Aurora',0);
{% endhighlight %}

Now, we can view the newly populated table using a DML `SELECT` statement. For instance, a query to retrieve information from a particular table may look like:

{% highlight ruby %}
### Example - basic selection query
SELECT *
FROM patient;
{% endhighlight %}


![sqlite3 basic table](../assets/img/sqlite3_create_table.png)

To make this output a little more user-friendly, we can add `.mode column` and `.headers ON` before the select statement.

![sqlite3 format output](../assets/img/sqlite3_create_table_columns.png)

Much easier to read!

Now that you can see what's inside the table, you might spot an error within it. It's easy to fix a particular row using an `UPDATE` statement:

{% highlight ruby %}
### Example UPDATE statement
UPDATE patients
SET got_flu_shot=1
WHERE firstname = 'Karen';
{% endhighlight %}

![sqlite3 update statement](../assets/img/sqlite3_update_table.png)
<br>


> **Keep in mind**
>
Use `UPDATE` to modify *existing* rows. Use `INSERT` for adding *new* rows.

We can keep inserting (and updating) our table information in this manner. However, if we have a large volume of patient information, we may wish to import it for instance from a csv file. I have prepared an example csv of patient data, which you can copy from [my github](www.google.com).

### Add data from a .csv file
{% highlight ruby %}
.mode csv patients
.import patient_data.csv patients
{% endhighlight %}

Let's check that the patient data was successfully added to our data table:

![sqlite3 csv insert](../assets/img/sqlite3_csv_insert.png)

### Saving table to a file
Alternatively, we may wish to save the full table (or other query output) to a file. We can easily do this using `.output`, followed by the name of the file we wish to create. The result of any query between `.output` and `.exit` will be saved to the text file.
{% highlight ruby %}
.output test_patients.txt
SELECT * FROM patients;
.exit
{% endhighlight %}
 The `.exit` statement takes us out of SQLite3 and into the regular command prompt. From here, we can type `dir` to see if the text file was indeed created, and type `more test_patients.txt` to view its contents in the prompt.

![command line read text file](../assets/img/sqlite3_cli_read.png)

# More Complex Operations & Join Types
Database management systems frequently involve more than one table, therefore more complex operations like [joins](https://www.sqlitetutorial.net/sqlite-join/) are necessary. Keep in mind that there are different possible types of joins for combining columns across related tables.

Let's create a second table so that we can test more complex queries.

{% highlight ruby %}
## Create table containing doctor office visit information
CREATE TABLE visits (
    visit_id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    date TEXT NOT NULL,
    patient_id INTEGER NOT NULL,
    symptom TEXT,
        FOREIGN KEY(patient_id)
        REFERENCES patients(patient_id)
    );

## Populate the table
INSERT INTO visits values(101, “11-1-2019”, 1, “sore throat”);
INSERT INTO visits values(102, “10-1-2019”, 3, “sore throat”);
INSERT INTO visits values(103, “15-1-2019”, 1, “runny nose”);
INSERT INTO visits values(104, “5-1-2019”, 2, “fever”);
INSERT INTO visits values(105, “25-1-2019”, 6, “sore throat”);
INSERT INTO visits values(106, “7-1-2019”, 4, “fever”);

## Can also add visit information from csv file
.mode csv visits
.import visit_data.csv visits
{% endhighlight %}

![SQL populate table](../assets/img/sqlite3_populate_table.png)

<br>

### Natural Join
Now that we have a second table, we can query both using joins. For now, I'll just cover the **Natural Join**, although keep in mind that there are other options such as Cross Joins and Outer Joins to manipulate multiple relations.
{% highlight ruby %}
SELECT firstname, lastname, symptom, visit_id, date
FROM patients natural join visits
WHERE patient_id = 10;
{% endhighlight %}

![SQL natural join](../assets/img/sqlite3_natural_join.png)

Natural join applies when you have the same column names in both tables, so bear in mind that it has some redundancy.

<!-- **NULL values in a Join**. Foreign key can have nulls. If you use a foreign key to join and one of the entries is null, then that row will be dropped from the query result. -->

<br>

## Other Common Operations
### Remove duplicates
{% highlight ruby %}
SELECT DISTINCT patient_id
FROM visits;
{% endhighlight %}

![SQL select distinct](../assets/img/sqlite3_select_distinct.png)

### Sorting
{% highlight ruby %}
SELECT *
FROM visits
ORDER BY symptom ASC;
{% endhighlight %}
![SQL sorting](../assets/img/sqlite3_sort_asc.png)

<!--
### 1. Cross Join (aka Cartesian Product)
Combine every row in table1 with every row in table2 (result is a very large table).
{% highlight ruby %}
SELECT * FROM Employee, Department WHERE Depname = Dname;
{% endhighlight %}
* Note: Disadvantage to this is - what happens when the department name changes?
* Solution: reference should be a key for a Dnumber is Unique and Not Null -->


<!-- ### 3. Outer Join
Preserves rows (inserts NULLs in the missing fields instead of dropping the whole row)
* **Query using LIKE**
{% highlight ruby %}
SELECT Mgr_ssn
FROM DEPARTMENT NATURAL JOIN DEPT_LOCATIONS
WHERE Dlocation LIKE ‘%d’;
{% endhighlight %}


### Aliasing
{% highlight ruby %}
SELECT Fname, 1.1*Salary as NewSalary
FROM Employee WHERE  Salary > 30000;
{% endhighlight %} -->



## Relational versus Object Oriented Databases
The way that a database management system accesses and processes its information can be grouped into two distinct categories. On the one had, you have **relational databases** which are systems that rely on key-value pairs to connect and transfer information. Alternatively there are **object-oriented databases (OODBs)**, where data is stored in the form of an *object* consisting of (1) the data and (2) the instruction for software.

OODBs initially seemed like they would be a major competitor to relational databases, since they were more general and used popular object-oriented principles. However, the complexity of the OO model and the lack of an early standard meant that they weren’t as widely adopted as initially anticipated. Examples of current OODBs include MongoDB and Neo4j.

#### What's so different about NoSQL (Not Only SQL) databases?

   """" |SQL |	NoSQL
:---:|:---:|:---:
TYPE | Relational Databases (RDBMS)	| Non-relational or distributed database
BASIS| Table-based databases | Document-based, key-value pairs, graph databases or wide-column stores
SCHEMA| Schema is predefined | Dynamic schema for unstructured data
EXAMPLES |MySql, Oracle, Sqlite, Postgres	| MongoDB, Neo4j
STRENGTHS |Better for complex queries |	Better for big data
{:.post-table-med}

<br>

(Note: page under development)

<br>

# Conclusion
With the advent of [Big Data](/big-data/), more and more systems are increasingly using databases to manage the high volume, variety and velocity of information.

# Reference
* Database Systems (Elmasri and Navathe)
