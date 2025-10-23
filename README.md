## 🧠 SQL Cheat Sheet

A **comprehensive SQL reference guide** covering all major commands — from the basics of querying data to advanced operations like joins, subqueries, and transactions.
Useful for **Data Analysts, Data Engineers, and Developers** preparing for projects or interviews.

---

### 💡 What is SQL?

**SQL (Structured Query Language)** is a standard programming language used to interact with **Relational Databases**.
It allows you to **store, manage, and retrieve data efficiently** from tables using simple commands.


### 🧱 Types of SQL Commands

| Category                               | Purpose                     | Example Commands                       |
| -------------------------------------- | --------------------------- | -------------------------------------- |
| **DDL** (Data Definition Language)     | Defines database structure  | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`  |
| **DML** (Data Manipulation Language)   | Manages data inside tables  | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** (Data Control Language)        | Controls access permissions | `GRANT`, `REVOKE`                      |
| **TCL** (Transaction Control Language) | Manages transactions        | `COMMIT`, `ROLLBACK`, `SAVEPOINT`      |
| **DQL** (Data Query Language)          | Fetches data                | `SELECT`                               |


### 🧩 Basic SQL Query Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE condition
GROUP BY column_name
HAVING condition
ORDER BY column_name ASC|DESC;
```

> 📝 **Note:** SQL keywords are **not case-sensitive**,
> but it’s a best practice to write commands in **UPPERCASE** for readability.


### 🧾 Example Table

| customer_id | name | city     | age |
| ----------- | ---- | -------- | --- |
| 1           | John | New York | 25  |
| 2           | Mary | London   | 30  |
| 3           | Alex | Delhi    | 22  |

---


## Data Manipulation Language (DML) Commands
**Data Manipulation Language (DML)** commands are used to manage and manipulate data stored in database tables.
They allow users to **insert new records, retrieve existing data, update information,** and **delete records** as needed — without altering the database structure itself.

| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | SELECT | The SELECT command retrieves data from a database. | `SELECT column1, column2 FROM table_name;` | `SELECT first_name, last_name FROM customers;` |
| 2 | INSERT  |The INSERT command adds new records to a table. | `INSERT INTO table_name (column1, column2) VALUES (value1, value2);` |` INSERT INTO customers (first_name, last_name) VALUES ('Mary', 'Doe');` |
| 3 | UPDATE | The UPDATE command is used to modify existing records in a table. | `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` | `UPDATE employees SET employee_name = ‘John Doe’, department = ‘Marketing’; `|

