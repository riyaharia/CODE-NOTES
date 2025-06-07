#DATABASE SCHEMA


###A Database Schema is like the blueprint or layout of your database

##What is an EER Diagram?
###EER stands for Enhanced Entity-Relationship Diagram. 
###Visualizes the structure of a database at a high level

Shows entities (things like Student, Product), their attributes (name, age), and how they relate to each other

Helps you design databases that are flexible, scalable, and ready to handle real-world complexity

#KEY
A key in SQL is a column or set of columns in a table that is used to:

👉 Uniquely identify rows
👉 Maintain relationships between tables


##Primary Key
###Unique Id for a transcation
###A Primary Key is:

A column or a set of columns that uniquely identifies each row in a table.

👉 It CANNOT have NULL values.

👉 It must be UNIQUE — no two rows can have the same primary key value.

##Foreign Key
###A Foreign Key:

👉 Is a column (or group of columns) that creates a link between two tables.

👉 It refers to the Primary Key of another table.

##Unique Key
###A UNIQUE KEY is a column (or set of columns) that ensures all values are unique in that column — no duplicates allowed.
✅ It allows NULL values (but usually only once, depending on the DBMS).
✅ You can have multiple UNIQUE keys in a single table.

##Composite Keys
###A Composite Key is a combination of two or more columns that together uniquely identify a row in a table.

```CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    PRIMARY KEY (student_id, course_id)
);

##Candidate Key
###A Candidate Key is:

Any column or set of columns that can uniquely identify each row in a table.

They’re called “candidates” because they are eligible to be the Primary Key — but only one gets chosen.