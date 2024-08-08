# SQLite Tutorial: SELECT, WHERE, GROUP BY, ORDER BY, JOINS

## Introduction

SQLite is a lightweight, disk-based database that doesn’t require a separate server process. It is widely used in applications due to its simplicity and ease of setup. This tutorial will guide you through some basic SQL operations in SQLite, including SELECT, WHERE, GROUP BY, ORDER BY, and JOINS.

### Prerequisites
- Basic understanding of SQL
- SQLite installed on your system

## 1. Setting Up SQLite

### Step 1: Install SQLite
Download and install SQLite from the [official website](https://www.sqlite.org/download.html) and follow the installation instructions for your operating system.

### Step 2: Verify Installation
Open your terminal and run the following command to verify that SQLite is installed correctly:
```bash
sqlite3 --version
```
You should see the installed SQLite version.

## 2. Creating a Database and Table

### Step 1: Create a Database
Create a new SQLite database by running the following command in your terminal:
```bash
sqlite3 mydatabase.db
```

### Step 2: Create a Table
Create a table named `employees` with the following structure:
```sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    department TEXT NOT NULL,
    salary REAL NOT NULL,
    hire_date TEXT NOT NULL
);
```

Insert some sample data into the `employees` table:
```sql
INSERT INTO employees (name, department, salary, hire_date) VALUES
('Alice', 'HR', 60000, '2018-01-15'),
('Bob', 'Engineering', 80000, '2019-03-22'),
('Charlie', 'Engineering', 85000, '2017-05-30'),
('Diana', 'Sales', 50000, '2020-07-12'),
('Eve', 'HR', 55000, '2019-11-01');
```

## 3. Basic SQL Operations

### SELECT Statement
The `SELECT` statement is used to query data from a database. The data returned is stored in a result table, sometimes called the result set.

**Example:**
```sql
SELECT name, department, salary FROM employees;
```

**Discussion:**
1. **SELECT**: Specifies the columns to retrieve.
2. **FROM**: Specifies the table to query.

### WHERE Clause
The `WHERE` clause is used to filter records. It is used to extract only those records that fulfill a specified condition.

**Example:**
```sql
SELECT name, salary FROM employees WHERE department = 'Engineering';
```

**Discussion:**
1. **WHERE**: Specifies the condition to filter the records.

### GROUP BY Clause
The `GROUP BY` statement groups rows that have the same values into summary rows, like "find the number of employees in each department."

**Example:**
```sql
SELECT department, COUNT(*) AS count FROM employees GROUP BY department;
```

**Discussion:**
1. **GROUP BY**: Groups rows that have the same values in specified columns.
2. **COUNT**: An aggregate function that returns the number of input rows.

### ORDER BY Clause
The `ORDER BY` statement is used to sort the result set in either ascending or descending order.

**Example:**
```sql
SELECT name, salary FROM employees ORDER BY salary DESC;
```

**Discussion:**
1. **ORDER BY**: Specifies the column to sort by.
2. **DESC**: Sorts the result set in descending order (use `ASC` for ascending order).

### JOIN Operations
Joins are used to combine rows from two or more tables, based on a related column between them.

#### INNER JOIN
The `INNER JOIN` keyword selects records that have matching values in both tables.

**Example:**
Create another table named `departments`:
```sql
CREATE TABLE departments (
    department_name TEXT PRIMARY KEY,
    location TEXT NOT NULL
);

INSERT INTO departments (department_name, location) VALUES
('HR', 'New York'),
('Engineering', 'San Francisco'),
('Sales', 'Los Angeles');
```

Perform an INNER JOIN between `employees` and `departments`:
```sql
SELECT employees.name, employees.department, departments.location
FROM employees
INNER JOIN departments ON employees.department = departments.department_name;
```

**Discussion:**
1. **INNER JOIN**: Selects records that have matching values in both tables.
2. **ON**: Specifies the condition to match records in both tables.

#### LEFT JOIN
The `LEFT JOIN` keyword returns all records from the left table (employees), and the matched records from the right table (departments). The result is `NULL` from the right side, if there is no match.

**Example:**
```sql
SELECT employees.name, employees.department, departments.location
FROM employees
LEFT JOIN departments ON employees.department = departments.department_name;
```

**Discussion:**
1. **LEFT JOIN**: Returns all records from the left table and matched records from the right table. If no match is found, `NULL` values are returned for columns of the right table.

#### RIGHT JOIN
SQLite does not support `RIGHT JOIN` directly. However, it can be emulated by swapping the tables and using `LEFT JOIN`.

## Conclusion

By following this tutorial, you’ve learned the basics of using SQLite to perform common SQL operations such as `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`, and various `JOIN` operations. SQLite is a powerful and lightweight database, and mastering these commands will help you manage and query your databases effectively.

Happy querying!