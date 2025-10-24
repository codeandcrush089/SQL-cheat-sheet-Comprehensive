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
| 4 | DELETE | The DELETE command removes records from a table | `DELETE FROM table_name WHERE condition;` | `DELETE FROM employees WHERE employee_name = ‘John Doe’;` |

---
## Data Definition Language (DDL) Commands
**Data Definition Language (DDL) Commands** are used to **define, modify, and manage the structure of database objects** such as tables, schemas, and indexes.
They focus on **how the data is stored**, not the data itself.
Using DDL, you can create new tables, alter existing ones, or remove database objects entirely.

* In short: DDL commands deal with the **blueprint** of your database — its structure and schema.

| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | CREATE | The CREATE command creates a new database and objects, such as a table, index, view, or stored procedure. | `CREATE TABLE table_name (column1 datatype1, column2 datatype2, ...);` | `CREATE TABLE employees ( employee_id INT PRIMARY KEY, first_name VARCHAR(50), last_name VARCHAR(50), age INT ); ` |
| 2 | ALTER  |The ALTER command adds, deletes, or modifies columns in an existing table.  | `ALTER TABLE table_name ADD column_name datatype; ` |`ALTER TABLE customers ADD email VARCHAR(100);` |
| 3 | DROP | The DROP command is used to drop an existing table in a database.  | `DROP TABLE table_name;` | `DROP TABLE customers; `|
| 4 | TRUNCATE | The TRUNCATE command is used to delete the data inside a table, but not the table itself.  | `TRUNCATE TABLE table_name; ` | `TRUNCATE TABLE customers; ` |

---

## Data Control Language (DCL) Commands
**Data Control Language (DCL) Commands** are used to **control access and permissions** within a database.
They help database administrators **grant or revoke privileges** to users or roles, ensuring that only authorized users can perform certain actions like selecting, inserting, or deleting data.
Using DDL, you can create new tables, alter existing ones, or remove database objects entirely.

* In short: In short: DCL focuses on **who can do what** in the database — it manages **security and user access control**.

| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | GRANT | The GRANT command is used to give specific privileges to users or roles. | `GRANT SELECT, INSERT ON table_name TO user_name;` | `GRANT SELECT, INSERT ON employees TO ‘John Doe’;  ` |
| 2 | REVOKE  |The REVOKE command is used to take away privileges previously granted to users or roles.  | `REVOKE SELECT, INSERT ON table_name FROM user_name;  ` |`REVOKE SELECT, INSERT ON employees FROM ‘John Doe’;` |

---

## Transaction Control Language (TCL) Commands
**TCL commands** are used to manage transactions in a database.
A transaction is a sequence of one or more SQL operations that are executed as a single unit of work.
TCL ensures that either all **operations succeed (COMMIT)** or **none of them do (ROLLBACK)**, maintaining **data integrity and consistency.**


| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | COMMIT | Saves all the changes made during the current transaction permanently in the database. Once committed, the changes cannot be rolled back. | `COMMIT;` | `BEGIN;<br>UPDATE employees SET salary = 50000 WHERE id = 101;<br>COMMIT; ` |
| 2 | ROLLBACK  |Undoes all the changes made during the current transaction and restores the database to its previous state. | `ROLLBACK; ` |`BEGIN;<br>UPDATE employees SET salary = 50000 WHERE id = 101;<br>ROLLBACK;` |
| 3 | SAVEPOINT | Sets a savepoint within a transaction that can be rolled back to, without affecting the entire transaction.  | `SAVEPOINT savepoint_name;` | `BEGIN;<br>INSERT INTO employees VALUES (105, 'Alice', 28);<br>SAVEPOINT before_update;<br>UPDATE employees SET age = 30 WHERE id = 105;<br>ROLLBACK TO before_update; `|
| 4 | ROLLBACK TO SAVEPOINT | Rolls back the transaction to a previously defined savepoint, undoing only part of the transaction. | `ROLLBACK TO SAVEPOINT savepoint_name; ` | `ROLLBACK TO SAVEPOINT before_update;` |
| 5 | SET TRANSACTION | Configures properties of a transaction such as isolation level or access mode (read/write). | SET TRANSACTION READ WRITE|  |

---

## Data Query Language (DQL) Commands
**DQL commands** are used to **fetch data** from a database.
They allow users to retrieve specific information from one or more tables using different conditions, filters, and sorting options.
Although DQL technically has only one main command — SELECT, it is the **most used SQL command** and forms the base of almost every SQL query.

| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | WHERE | Filters records based on a specific condition. | `SELECT * FROM table_name WHERE condition;` | `SELECT * FROM employees WHERE department = 'HR'; ` |
| 2 | ORDER BY  |Sorts the result set in ascending or descending order. | `SELECT * FROM table_name ORDER BY column_name ASC; ` |`` |
| 3 | GROUP BY | Groups rows that have the same values into summary rows. Often used with aggregate functions like COUNT(), SUM(), AVG().  | `SELECT column, COUNT(*) FROM table_name GROUP BY column;` | `SELECT department, COUNT(*) FROM employees GROUP BY department; `|
| 4 | HAVING | Filters grouped results (used with GROUP BY). Similar to WHERE but for aggregated data. | `SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING COUNT(*) > value; ` | `SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;` |

