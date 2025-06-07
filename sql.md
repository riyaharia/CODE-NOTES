# DATABASE SCHEMA

A **Database Schema** is like the **blueprint or layout** of your database.

---

## What is an EER Diagram?

**EER** stands for **Enhanced Entity-Relationship Diagram**.

✅ Visualizes the structure of a database at a high level  
✅ Shows **entities** (like Student, Product), their **attributes** (name, age), and how they relate  
✅ Helps you design databases that are **flexible**, **scalable**, and **real-world ready**

---

# KEYS

A **key** in SQL is a column or set of columns in a table used to:

👉 Uniquely identify rows  
👉 Maintain relationships between tables  

---

## Primary Key

**Primary Key** is the unique ID for a record or transaction.

✅ Uniquely identifies each row  
❌ Cannot have NULL values  
✅ Must be UNIQUE — no two rows can have the same value

---

## Foreign Key

**Foreign Key** is used to link tables.

👉 It refers to the **Primary Key** in another table  
👉 Enforces **referential integrity** between tables

---

## Unique Key

**UNIQUE KEY** ensures no duplicates in a column or set of columns.

✅ Allows **NULL values** (once)  
✅ Multiple UNIQUE keys can exist in one table

---

## Composite Key

**Composite Key** = Multiple columns used together to uniquely identify a row.

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    PRIMARY KEY (student_id, course_id)
);

---

## Candidate Key

A **Candidate Key** is any **column or set of columns** that can **uniquely identify each row** in a table.

They’re called **"candidates"** because they are **eligible to become the Primary Key** — but only one gets chosen. The rest remain as **alternate unique identifiers**.

