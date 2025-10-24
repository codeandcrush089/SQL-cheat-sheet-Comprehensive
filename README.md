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

> 💡 In short: DDL commands deal with the **blueprint** of your database — its structure and schema.

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

> 💡 In short: In short: DCL focuses on **who can do what** in the database — it manages **security and user access control**.

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

---

## Joining Commands
**JOINs** are used to **combine data from two or more tables** based on a related column between them.
They help in retrieving meaningful data spread across multiple tables by establishing **relationships using keys** (usually primary and foreign keys).

> 💡 In short: **JOIN = Connect related data from multiple tables** into one result set.

| No | Command  | Description  | Syntax | Example  |
|----|----------|--------------|--------|----------|
| 1 | INNER JOIN | The INNER JOIN command returns rows with matching values in both tables. | `SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;` | `SELECT * FROM employees INNER JOIN departments ON employees.department_id = departments.id; ` |
| 2 | LEFT JOIN/LEFT OUTER JOIN  |The LEFT JOIN command returns all rows from the left table (first table) and the matching rows from the right table (second table). | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column; ` |`SELECT * FROM employees LEFT JOIN departments ON employees.department_id = departments.id;` |
| 3 | RIGHT JOIN/RIGHT OUTER JOIN | The RIGHT JOIN command returns all rows from the right table (second table) and the matching rows from the left table (first table). | SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;` | `SELECT *FROM employees RIGHT JOIN departments ON employees.department_id = departments.department_id; `|
| 4 | FULL JOIN/FULL OUTER JOIN | The FULL JOIN command returns all rows when there is a match in either the left table or the right table.| `SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column; ` | `SELECT *FROM employees LEFT JOIN departments ON employees.employee_id = departments.employee_id UNION SELECT *FROM employees RIGHT JOIN departments ON employees.employee_id = departments.employee_id; ` |
| 5 | CROSS JOIN | The CROSS JOIN command combines every row from the first table with every row from the second table, creating a Cartesian product. | `SELECT * FROM table1 CROSS JOIN table2;` | `SELECT * FROM employees CROSS JOIN departments; ` |
| 6 | SELF JOIN   |The SELF JOIN command joins a table with itself.  | `SELECT * FROM table1 t1, table1 t2 WHERE t1.column = t2.column; ` |`SELECT * FROM employees t1, employees t2 WHERE t1.employee_id = t2.employee_id; ` |
| 7 | NATURAL JOIN  | The NATURAL JOIN command matches columns with the same name in both tables.   | `SELECT * FROM table1 NATURAL JOIN table2;` | `SELECT * FROM employees NATURAL JOIN departments; `|

---

## Subqueries in SQL

A **Subquery** (also called an *inner query* or *nested query*) is a query written **inside another SQL statement**.
It is used to **fetch data based on the result of another query**, making SQL queries more dynamic and powerful.

> 💡 In short: A **subquery** allows you to use the result of one query inside another — for filtering, comparison, or validation.


|  No | Command | Description                                                                                                  | Syntax                                                   | Example                                                                                            |
| :-: | :------ | :----------------------------------------------------------------------------------------------------------- | :------------------------------------------------------- | :------------------------------------------------------------------------------------------------- |
|  1  | **IN**  | Checks whether a value matches **any value in a subquery result**. Often used in the `WHERE` clause.         | `SELECT column FROM table WHERE value IN (subquery);`    | `sql<br>SELECT * FROM customers WHERE city IN (SELECT city FROM suppliers);`                       |
|  2  | **ANY** | Compares a value to **any value returned by a subquery** using comparison operators like `=`, `>`, `<`, etc. | `SELECT column FROM table WHERE value < ANY (subquery);` | `sql<br>SELECT * FROM products WHERE price < ANY (SELECT unit_price FROM supplier_products);`      |
|  3  | **ALL** | Compares a value to **all values returned by a subquery**. Used with `=`, `>`, `<`, etc.                     | `SELECT column FROM table WHERE value > ALL (subquery);` | `sql<br>SELECT * FROM orders WHERE order_amount > ALL (SELECT total_amount FROM previous_orders);` |

### 🧠 **Notes:**

* Subqueries can be used inside **SELECT, FROM,** or **WHERE** clauses.
* The inner query is executed first, and its result is used by the outer query.
* **IN** is used for list comparison, <br>
  **ANY** for at least one match,<br>
  and **ALL** for every match (all conditions must be true).
---

## Aggregate Functions in SQL

**Aggregate functions** perform calculations on a set of values and return a **single summarized result** (like total, average, count, etc.).
They are commonly used with the `GROUP BY` clause to analyze data in groups or categories.

> 💡 In short: Aggregate functions help you **summarize data** — for example, counting total rows, finding averages, or getting minimum/maximum values.



|  No |Command    | Description                                                              | Syntax                                       | Example                                     |
| :-: | :---------- | :----------------------------------------------------------------------- | :------------------------------------------- | :------------------------------------------ |
|  1  | **COUNT()** | Counts the total number of rows or non-null values in a specific column. | `SELECT COUNT(column_name) FROM table_name;` | `sql<br>SELECT COUNT(age) FROM employees;`  |
|  2  | **SUM()**   | Calculates the total (sum) of all numeric values in a column.            | `SELECT SUM(column_name) FROM table_name;`   | `sql<br>SELECT SUM(salary) FROM employees;` |
|  3  | **AVG()**   | Returns the average (mean) of all numeric values in a column.            | `SELECT AVG(column_name) FROM table_name;`   | `sql<br>SELECT AVG(price) FROM products;`   |
|  4  | **MIN()**   | Returns the smallest (minimum) value from a column.                      | `SELECT MIN(column_name) FROM table_name;`   | `sql<br>SELECT MIN(age) FROM employees;`    |
|  5  | **MAX()**   | Returns the largest (maximum) value from a column.                       | `SELECT MAX(column_name) FROM table_name;`   | `sql<br>SELECT MAX(salary) FROM employees;` |


### 🧠 **Notes:**

* Aggregate functions **ignore NULL values** during calculations.
* You can combine them with `GROUP BY` to calculate summaries by category.
* They are **read-only** functions — they do not modify data.


---

## ✨ **String Functions in SQL**

**String functions** are used to **manipulate and transform text data** in SQL.
They help in cleaning, formatting, and extracting parts of strings — which is especially useful for data analysis and reporting.

> 💡 In short: String functions make it easy to **combine, format, or modify text** stored in database columns.


| No | Command | Description | Syntax | Example |
| :-: | :--- | :--- | :--- | :--- |
| 1 | **CONCAT()** | Joins two or more strings into a single string. | `SELECT CONCAT(string1, string2, ...);` | `SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;` |
| 2 | **SUBSTRING() / SUBSTR()** | Extracts a portion of a string starting from a given position (and optional length). | `SELECT SUBSTRING(string FROM start [FOR length]);` | `SELECT SUBSTRING(product_name FROM 1 FOR 5) AS short_name FROM products;` |
| 3 | **CHAR_LENGTH() / LENGTH()** | Returns the number of characters in a string. | `SELECT CHAR_LENGTH(string) AS length;` | `SELECT CHAR_LENGTH(product_name) AS name_length FROM products;` |
| 4 | **UPPER()** | Converts all characters in a string to uppercase. | `SELECT UPPER(string);` | `SELECT UPPER(first_name) AS upper_name FROM employees;` |
| 5 | **LOWER()** | Converts all characters in a string to lowercase. | `SELECT LOWER(string);` | `SELECT LOWER(last_name) AS lower_name FROM employees;` |
| 6 | **TRIM()** | Removes spaces or specified characters from the beginning or end of a string. | `SELECT TRIM([LEADING \| TRAILING \| BOTH] 'char' FROM string);` | `SELECT TRIM(BOTH ' ' FROM full_name) AS clean_name FROM customers;` |
| 7 | **LEFT()** | Returns a specified number of characters from the **left** side of a string. | `SELECT LEFT(string, number);` | `SELECT LEFT(product_name, 4) AS prefix FROM products;` |
| 8 | **RIGHT()** | Returns a specified number of characters from the **right** side of a string. | `SELECT RIGHT(string, number);` | `SELECT RIGHT(order_id, 3) AS suffix FROM orders;` |
| 9 | **REPLACE()** | Replaces all occurrences of a substring with a new substring. | `SELECT REPLACE(string, old_substring, new_substring);` | `SELECT REPLACE(description, 'old', 'new') AS updated_desc FROM products;` |
| 10 | **POSITION() / INSTR()** | Finds the starting position of a substring within a string. | `SELECT POSITION('substring' IN string);` | `SELECT POSITION('@' IN email) AS at_sign_position FROM users;` |
| 11 | **LPAD() / RPAD()** | Left or Right pads a string with a specified character up to a certain length. | `SELECT LPAD(string, length, 'pad_char');` | `SELECT RPAD(id, 5, '0') AS padded_id FROM orders;` |
---

### 🧠 **Notes:**

* These functions are **supported in most SQL databases** (MySQL, PostgreSQL, SQL Server, Oracle).
* `TRIM()` is useful for removing extra spaces in text fields.
* `CONCAT()` and `REPLACE()` are especially common in **data cleaning** operations.

---


##  **Date and Time SQL Commands**

**Date and Time functions** in SQL are used to **work with date, time, and timestamp values**.
They allow you to retrieve the current date/time, extract specific parts (like year or month), perform calculations, and format date outputs.

> 💡 In short: These functions help you **analyze and manipulate time-based data**, such as calculating durations, formatting timestamps, or filtering by date.



|  No | Command                   | Description                                                                             | Syntax                                                                                         | Example                                                                                 |
| :-: | :-------------------------- | :-------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------- |
|  1  | **CURRENT_DATE()**          | Returns the current system date.                                                        | `SELECT CURRENT_DATE();`                                                                       | `sql<br>SELECT CURRENT_DATE() AS today_date;`                                           |
|  2  | **CURRENT_TIME()**          | Returns the current system time.                                                        | `SELECT CURRENT_TIME();`                                                                       | `sql<br>SELECT CURRENT_TIME() AS current_time;`                                         |
|  3  | **CURRENT_TIMESTAMP()**     | Returns the current date and time (timestamp).                                          | `SELECT CURRENT_TIMESTAMP();`                                                                  | `sql<br>SELECT CURRENT_TIMESTAMP() AS current_datetime;`                                |
|  4  | **DATE_PART()**             | Extracts a specific part (like year, month, or day) from a date or timestamp.           | `SELECT DATE_PART('part', date_expression);`                                                   | `sql<br>SELECT DATE_PART('year', order_date) AS order_year FROM orders;`                |
|  5  | **DATE_ADD() / DATE_SUB()** | Adds or subtracts a specific interval (like days or months) from a date.                | `SELECT DATE_ADD(date, INTERVAL value unit);`<br>`SELECT DATE_SUB(date, INTERVAL value unit);` | `sql<br>SELECT DATE_ADD('2025-01-01', INTERVAL 7 DAY) AS next_week;`                    |
|  6  | **EXTRACT()**               | Similar to DATE_PART(), extracts a specific part from a date or time value.             | `SELECT EXTRACT(part FROM date_expression);`                                                   | `sql<br>SELECT EXTRACT(MONTH FROM order_date) AS order_month FROM orders;`              |
|  7  | **TO_CHAR()**               | Converts a date or timestamp to a string in a specified format.                         | `SELECT TO_CHAR(date_expression, 'format');`                                                   | `sql<br>SELECT TO_CHAR(order_date, 'YYYY-MM-DD') AS formatted_date FROM orders;`        |
|  8  | **TIMESTAMPDIFF()**         | Returns the difference between two timestamps in a specified unit (like days or hours). | `SELECT TIMESTAMPDIFF(unit, datetime1, datetime2);`                                            | `sql<br>SELECT TIMESTAMPDIFF(DAY, order_date, delivery_date) AS days_diff FROM orders;` |
|  9  | **DATEDIFF()**              | Calculates the number of days between two date values.                                  | `SELECT DATEDIFF(date1, date2);`                                                               | `sql<br>SELECT DATEDIFF('2025-10-20', '2025-10-01') AS days_between;`                   |


### 🧠 **Notes:**

* `CURRENT_DATE()` and `CURRENT_TIMESTAMP()` are commonly used in **logging** and **auditing**.
* Use `DATE_ADD()` or `DATE_SUB()` for **date calculations** (like adding days/months).
* `EXTRACT()` and `DATE_PART()` are similar — their usage depends on the SQL dialect.
* `TO_CHAR()` is especially useful for **custom date formatting** in Oracle and PostgreSQL.

---

##  **Conditional Expressions in SQL**

**Conditional expressions** in SQL are used to perform **logic-based operations** within queries.
They allow you to add **decision-making capability** — for example, returning different results based on conditions (like an IF-ELSE statement in programming).

> 💡 In short: Conditional expressions make your queries **dynamic and smart**, letting SQL choose results based on data values.



|  No |Command     | Description                                                                                                   | Syntax                                                                                                         | Example                                                                                                                                                                                                    |
| :-: | :------------- | :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  1  | **CASE**       | Evaluates multiple conditions and returns a value when the first condition is true. Works like IF–ELSE logic. | `sql<br>CASE<br> WHEN condition1 THEN result1<br> WHEN condition2 THEN result2<br> ELSE default_result<br>END` | `sql<br>SELECT order_id, total_amount,<br>CASE<br> WHEN total_amount > 1000 THEN 'High Value'<br> WHEN total_amount > 500 THEN 'Medium Value'<br> ELSE 'Low Value'<br>END AS order_status<br>FROM orders;` |
|  2  | **IF()**       | Checks a condition and returns one value if true, another if false. (Mostly used in MySQL.)                   | `SELECT IF(condition, true_value, false_value);`                                                               | `sql<br>SELECT name, age, IF(age > 50, 'Senior', 'Junior') AS category FROM employees;`                                                                                                                    |
|  3  | **COALESCE()** | Returns the first **non-NULL** value from a list of expressions.                                              | `SELECT COALESCE(value1, value2, ...);`                                                                        | `sql<br>SELECT COALESCE(middle_name, first_name) AS display_name FROM employees;`                                                                                                                          |
|  4  | **NULLIF()**   | Returns `NULL` if two expressions are equal; otherwise, returns the first expression.                         | `SELECT NULLIF(expression1, expression2);`                                                                     | `sql<br>SELECT NULLIF(total_amount, discounted_amount) AS diff FROM orders;`                                                                                                                               |


### 🧠 **Notes:**

* `CASE` is the **most powerful** and **cross-database compatible** conditional expression.
* `IF()` works mainly in **MySQL**, while `IIF()` is used in **SQL Server**.
* `COALESCE()` is commonly used for **handling NULL values** gracefully.
* `NULLIF()` helps **avoid division-by-zero** or redundant calculations.

---

##  **Set Operations in SQL**

**Set operations** are used to **combine the results** of two or more `SELECT` statements into a single result set.
They help compare or merge data from multiple queries, just like mathematical set operations (UNION, INTERSECT, EXCEPT).

> 💡 In short: Set operations let you **merge, match, or exclude** data between multiple result sets.


|  No | Command                           | Description                                                                         | Syntax                                                                                        | Example                                                                                                       |
| :-: | :-------------------------------- | :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------ |
|  1  | **UNION**                         | Combines the result sets of two or more queries and **removes duplicate rows**.     | `sql<br>SELECT column1, column2 FROM table1<br>UNION<br>SELECT column1, column2 FROM table2;` | `sql<br>SELECT first_name, last_name FROM customers<br>UNION<br>SELECT first_name, last_name FROM employees;` |
|  2  | **UNION ALL**                     | Combines results like `UNION` but **includes duplicates**.                          | `sql<br>SELECT column1 FROM table1<br>UNION ALL<br>SELECT column1 FROM table2;`               | `sql<br>SELECT city FROM customers<br>UNION ALL<br>SELECT city FROM suppliers;`                               |
|  3  | **INTERSECT**                     | Returns only the **common rows** found in both result sets.                         | `sql<br>SELECT column1 FROM table1<br>INTERSECT<br>SELECT column1 FROM table2;`               | `sql<br>SELECT first_name FROM customers<br>INTERSECT<br>SELECT first_name FROM employees;`                   |
|  4  | **EXCEPT** *(or MINUS in Oracle)* | Returns rows from the **first query** that are **not present** in the second query. | `sql<br>SELECT column1 FROM table1<br>EXCEPT<br>SELECT column1 FROM table2;`                  | `sql<br>SELECT first_name FROM customers<br>EXCEPT<br>SELECT first_name FROM employees;`                      |

---

### 🧠 **Notes:**

* Each `SELECT` in a set operation **must have the same number of columns** and **matching data types**.
* The **order of columns** in each query must also match.
* `UNION ALL` is faster than `UNION` because it **does not remove duplicates**.
* `INTERSECT` and `EXCEPT` may not be supported in all databases (e.g., MySQL lacks them natively).

---
## Transaction Control Commands

| No | Command                   | Description                                                                                             | Syntax                                     | Example                                                                                                                                                                          |
|--| ------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|1| **COMMIT**                | Saves all changes made in the current transaction permanently to the database.                          | `COMMIT;`                                  | `sql BEGIN; UPDATE accounts SET balance = balance - 100 WHERE acc_id = 1; COMMIT;`                                                                                               |
|2| **ROLLBACK**              | Undoes all changes made in the current transaction, reverting the database to the last committed state. | `ROLLBACK;`                                | `sql BEGIN; DELETE FROM employees WHERE emp_id = 10; ROLLBACK;`                                                                                                                  |
|3| **SAVEPOINT**             | Creates a point within a transaction to which you can later roll back. Useful for partial rollbacks.    | `SAVEPOINT savepoint_name;`                | `sql BEGIN; UPDATE accounts SET balance = balance - 100 WHERE acc_id = 1; SAVEPOINT sp1; UPDATE accounts SET balance = balance + 100 WHERE acc_id = 2; ROLLBACK TO sp1; COMMIT;` |
|4| **ROLLBACK TO SAVEPOINT** | Rolls back the transaction to a specific savepoint without affecting prior operations.                  | `ROLLBACK TO savepoint_name;`              | `sql ROLLBACK TO sp1;`                                                                                                                                                           |
|5| **SET TRANSACTION**       | Sets the properties of the transaction like isolation level.                                            | `SET TRANSACTION [ISOLATION LEVEL level];` | `sql SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;`                                                                                                                              |

### 🧠 **Notes:**

* TCL commands are used to **control transactions** in a database.
* Transactions allow you to **ensure data integrity**: either all operations succeed (commit) or none (rollback).
* `SAVEPOINT` is optional but helpful in complex transactions.

---


