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


## Candidate Key

A **Candidate Key** is any column or set of columns that can uniquely identify each row in a table.

They’re called "candidates" because they are eligible to become the Primary Key — but only one gets chosen. The rest remain as alternate unique identifiers.

---

## Creating a Database

```sql
CREATE DATABASE sample_pizza;

-- This is a keyword to USE a particular database and not any other database
USE sample_pizza;

pizza_id INT PRIMARY KEY,
pizzanames VARCHAR(50),
toppings VARCHAR(150);
```

---

## SQL Comments

- Single-line comment → Use `--`  
- Multi-line comment → Use `/* */`

---

## ALTER vs UPDATE

- `ALTER` is used to **change the structure** (like column type, name).
- `UPDATE` is used to **change the values** in a table.

---

## Write a Query to Retrieve Only the Product Names from the Table `"pizza"`

```sql
SELECT product_name
FROM pizza;
```

---

## Selecting from a Column

```sql
SELECT COLUMN_NAME
FROM TABLE_NAME;
```

- Gets one or more columns from the specified table  
- Uses comma (`,`) to separate each column/field

---

## Selecting Only Unique or Distinct Values of a Field from a Table

```sql
SELECT DISTINCT size
FROM pizza;

SELECT DISTINCT products
FROM pizza;
```

---

### Selecting Distinct Values from Multiple Columns

```sql
SELECT DISTINCT color, size
FROM pizza;
```

- Basically filters **distinct combinations** of values.

---

## WHERE Clause

The `WHERE` clause is used to filter rows from a table based on a condition.  
It filters the data so you don’t get everything — just the exact piece you need.  
**Precision. Power. Control.**

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Limitations of WHERE clause:

- Can't filter on aggregated data (use `HAVING` for that)

---

## Operators in SQL

| Operator | Meaning                   | Works With         |
|----------|---------------------------|--------------------|
| =        | Equals                    | Numerical & Text   |
| >        | Greater than              | Numerical, Date    |
| <        | Less than                 | Numerical, Date    |
| >=       | Greater than or equal to  | Numerical, Date    |
| <=       | Less than or equal to     | Numerical, Date    |
| !=       | Not equal to              | Numerical & Text   |

---

## Filtering Examples

```sql
SELECT * FROM employee_data
WHERE Employee_Employment_status = 'Inactive';

SELECT * FROM employee_data
WHERE Employee_Employment_status = 'Active';
```

---

## Selecting Employees with Salary Less Than 40k

```sql
SELECT * FROM employee_data
WHERE Current_Annual_Cost <= 40000;
```

---

## Employees with Salary Greater Than 80k

```sql
SELECT * FROM employee_data
WHERE Current_Annual_Cost >= 80000;
```

---

## Employees with Salary ≥ 80k Who Are Non-Managers, on Contract, and Not Senior

```sql
SELECT Employment_Type,
       Employee_name,
       Employment_level,
       Current_Annual_Cost
FROM employee_data
WHERE Current_Annual_Cost >= 80000
  AND Manager_Non_Manager_tag != 'Manager'
  AND Employment_Type = 'Contract'
  AND Employment_level != 'senior';
```

---

## Filter Employees Who Are on Contract OR Part-Time

```sql
SELECT * FROM employee_data
WHERE Employment_Type = 'contract'
   OR Employment_Type = 'part-time';
```

---

## Filter Employees Who Are on Contract OR Part-Time AND Salary > 60k

⚠️ Be careful with operator precedence (`AND` > `OR`)

```sql
SELECT * FROM employee_data
WHERE Employment_Type = 'contract'
   OR (Employment_Type = 'part-time' AND Current_Annual_Cost > 60000);
```

---

## Filter Contract or Part-Time Employees with Salary > 60k and Not Senior

```sql
SELECT * FROM employee_data
WHERE Employment_Type IN ('contract', 'part-time')
  AND Current_Annual_Cost > 60000
  AND Employment_level != 'senior';
```

---

## Why Use IN Instead of Multiple ORs?

When you want to filter multiple possible values from the same column, using `IN` makes the query shorter, cleaner, and more efficient.

```sql
-- Instead of this:
SELECT * FROM employee_data
WHERE Employment_Type = 'contract'
   OR Employment_Type = 'part-time';

-- Use this:
SELECT * FROM employee_data
WHERE Employment_Type IN ('contract', 'part-time');
```

✅ `IN` is preferred when checking a column against multiple values

- - -

# SQL Concepts, Queries & Examples

## 1. Filtering with WHERE + IN

### Ratings 1, 2, 3 from `deliveries` table:
```sql
SELECT * FROM deliveries
WHERE Delivery_ratings IN (1, 2, 3);
```

### Employees in IT, HR, Sales departments:
```sql
SELECT * FROM employee_data
WHERE Department IN ('IT', 'SALES', 'HR');
```

### Orders delivered to customers from Branch 7, 9, 18:
```sql
SELECT * FROM orders_info
WHERE Delivery_Y_N = 'Y'
  AND Branch_ID IN (7, 9, 18);
```

---

## 2. Wildcards in SQL (LIKE)

| Wildcard | Meaning                             | Example                                |
|----------|-------------------------------------|----------------------------------------|
| `%`      | Matches zero or more characters     | `'A%'` → matches 'A', 'Apple', 'Android' |
| `_`      | Matches exactly one character       | `'J_n'` → matches 'Jan', 'Jon', 'Jen'    |

### Example: Find pizzas with 'Veg' in name
```sql
SELECT color, calorie
FROM pizza
WHERE Pizza_Name LIKE '%Veg%';
```

---

## 3. Aggregations

### SUM
```sql
SELECT SUM(income_amount) FROM incomes;
```

### Using Alias with Aggregation
```sql
SELECT SUM(income_amt) AS total_income FROM table;
```

### COUNT
```sql
SELECT COUNT(person_name) FROM expenses;
```

### AVG
```sql
SELECT AVG(expense_amount) FROM expenses;
```

### MAX & MIN
```sql
SELECT MAX(expense_amount), MIN(expense_amount) FROM expenses;
```

---

## 4. LeetCode Example Query

> Report movies with an odd-numbered ID and a description not equal to "boring", ordered by rating descending.

```sql
SELECT * FROM Cinema
WHERE MOD(id, 2) = 1
  AND description != 'boring'
ORDER BY rating DESC;
```

---

## 5. GROUP BY

### Example: Total spent by expense type
```sql
SELECT expense_type,
       SUM(expense_amount) AS total_spent
FROM expense
GROUP BY expense_type;
```

### Average asset cost per status
```sql
SELECT asset_status,
       AVG(asset_cost) AS avg_cost
FROM assets
GROUP BY asset_status;
```

### Total, Average, and Count per asset type
```sql
SELECT asset_type,
       SUM(asset_cost) AS TOTAL_COST,
       AVG(asset_cost) AS AVG_COST,
       COUNT(asset_cost) AS NO_OF
FROM assets
GROUP BY asset_type;
```

### Campaign data per marketing channel
```sql
SELECT Channel,
       COUNT(campaign_spend) AS NO_OF,
       SUM(campaign_spend) AS TOTAL_SPEND,
       AVG(campaign_spend) AS AVG_SPEND
FROM marketing_campaigns
GROUP BY Channel;
```

### Campaign data per marketing format
```sql
SELECT Campaign_format,
       COUNT(campaign_spend) AS NO_OF,
       SUM(campaign_spend) AS TOTAL_SPEND,
       AVG(campaign_spend) AS AVG_SPEND
FROM marketing_campaigns
GROUP BY Campaign_format;
```

---

## 6. ORDER BY

### Average cost per asset status in ascending order
```sql
SELECT asset_status,
       AVG(asset_cost) AS avg_cost
FROM assets
GROUP BY asset_status
ORDER BY avg_cost ASC;
```

### Total/Avg/Count per asset type, sorted
```sql
SELECT asset_type,
       SUM(asset_cost) AS TOTAL_COST,
       AVG(asset_cost) AS AVG_COST,
       COUNT(asset_cost) AS NO_OF
FROM assets
GROUP BY asset_type
ORDER BY TOTAL_COST, AVG_COST, NO_OF;
```

---

## 7. WHERE vs HAVING

| Clause  | Use Case                    |
|---------|-----------------------------|
| WHERE   | Non-aggregated fields       |
| HAVING  | Aggregated fields + GROUP BY|

### Example: Average salary for active Part-time and Contract employees
```sql
SELECT Employment_Type,
       AVG(Current_Annual_Cost)
FROM employee_data
WHERE Employee_Employment_status = 'active'
GROUP BY Employment_Type
HAVING Employment_Type IN ('Part-time', 'Contract');
```
