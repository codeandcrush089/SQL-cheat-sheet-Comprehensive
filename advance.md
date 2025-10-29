## Advanced Querying & Data Handling in SQL

These are **powerful SQL techniques** used in **data analytics, reporting, and performance optimization**.
They go beyond basic `SELECT` queries and help in handling **complex calculations**, **comparisons**, and **data transformations** efficiently.



| Feature                                         | Description                                                                                                                              | Example / Usage                                                                                                                                                   |
| :---------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Common Table Expressions (CTEs)**             | Used to create **temporary result sets** that can be referenced within a query. Improves readability and reusability of complex queries. | `sql<br>WITH temp AS (SELECT department, COUNT(*) AS emp_count FROM employees GROUP BY department)<br>SELECT * FROM temp WHERE emp_count > 5;`                    |
| **Window Functions**                            | Perform calculations **across a set of rows related to the current row**, without collapsing the result set. Ideal for analytics.        | `sql<br>SELECT name, salary, RANK() OVER(ORDER BY salary DESC) AS rank FROM employees;`                                                                           |
| **ROW_NUMBER(), RANK(), DENSE_RANK(), NTILE()** | Provide **ranking and ordering** within partitions of data.                                                                              | `sql<br>SELECT name, ROW_NUMBER() OVER(ORDER BY join_date ASC) AS row_num FROM employees;`                                                                        |
| **LEAD(), LAG()**                               | Compare **current row values** with **previous or next row** — used in **time-series or trend analysis**.                                | `sql<br>SELECT sale_date, amount, LAG(amount) OVER(ORDER BY sale_date) AS prev_amount FROM sales;`                                                                |
| **Aggregate with OVER()**                       | Apply aggregate functions **without grouping the entire result set** — useful for running totals and moving averages.                    | `sql<br>SELECT department, salary, SUM(salary) OVER(PARTITION BY department) AS dept_total FROM employees;`                                                       |
| **CASE Expressions**                            | Add **conditional logic** inside queries for custom classifications or labels.                                                           | `sql<br>SELECT name, CASE WHEN salary > 80000 THEN 'High' ELSE 'Average' END AS salary_level FROM employees;`                                                     |
| **Nested Subqueries (Correlated)**              | Use a subquery that depends on the outer query — often used for comparisons or filtering based on related data.                          | `sql<br>SELECT name FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department = e.department);`                                         |
| **Pivoting / Unpivoting**                       | Transform rows into columns (pivot) or columns into rows (unpivot) — used for **data reshaping**. *(Syntax varies by database)*          | `sql<br>-- Example (SQL Server)<br>SELECT * FROM Sales PIVOT (SUM(amount) FOR month IN ([Jan],[Feb],[Mar])) AS PivotTable;`                                       |
| **Temporary / Derived Tables**                  | Create **intermediate result sets** for step-by-step processing inside a single query.                                                   | `sql<br>SELECT dept, avg_salary FROM (SELECT department AS dept, AVG(salary) AS avg_salary FROM employees GROUP BY department) AS temp WHERE avg_salary > 60000;` |


### 💡 **Why It Matters**

* Enables **advanced analytics** directly within SQL.
* Reduces need for post-processing in tools like Python or Excel.
* Makes SQL queries **modular, readable, and high-performing**.

---

## Data Cleaning & Transformation in SQL

These SQL techniques are essential for **data preprocessing** — helping analysts clean, standardize, and prepare raw data for analysis.
They focus on **handling missing values**, **formatting strings**, **working with dates**, and **converting data types** efficiently.

> 💡 In short: Data Cleaning ensures your SQL data is **accurate, consistent, and analysis-ready.**



| Category                   | Function(s)                                                              | Description                                                                                        | Example                                                                                                    |
| :------------------------- | :----------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| **NULL Handling**          | `COALESCE()`, `NULLIF()`, `ISNULL()`                                     | Manage missing or null values by replacing, ignoring, or comparing them.                           | `sql<br>SELECT COALESCE(middle_name, first_name) AS display_name FROM employees;`                          |
| **String Manipulation**    | `TRIM()`, `REPLACE()`, `CONCAT()`, `REGEXP_REPLACE()`, `REGEXP_SUBSTR()` | Clean and format text by trimming spaces, replacing substrings, or extracting text with regex.     | `sql<br>SELECT REPLACE(TRIM(name), 'Mr. ', '') AS clean_name FROM customers;`                              |
| **Date & Time Operations** | `DATEADD()`, `DATEDIFF()`, `EXTRACT()`, `TO_DATE()`, `FORMAT()`          | Perform date arithmetic, extract components (like year/month), and format or convert date strings. | `sql<br>SELECT DATEDIFF(day, order_date, delivery_date) AS days_taken FROM orders;`                        |
| **Time Bucketing**         | `DATE_TRUNC()`                                                           | Round or group timestamps by month, week, or year — great for time-series aggregation.             | `sql<br>SELECT DATE_TRUNC('month', order_date) AS order_month, COUNT(*) FROM orders GROUP BY order_month;` |
| **Type Conversion**        | `CAST()`, `CONVERT()`                                                    | Convert data between types (e.g., string → integer, date → text).                                  | `sql<br>SELECT CAST(salary AS DECIMAL(10,2)) AS formatted_salary FROM employees;`                          |
| **Data Rounding**          | `ROUND()`, `CEIL()`, `FLOOR()`                                           | Round numeric values up, down, or to specific precision levels.                                    | `sql<br>SELECT ROUND(sales_amount, 2) AS rounded_value FROM sales;`                                        |


### 🧠 **Notes:**

* Always clean your data **before analysis or visualization** to avoid incorrect results.
* `COALESCE()` is great for filling missing data, while `NULLIF()` prevents divide-by-zero errors.
* Use regex (`REGEXP_REPLACE`, `REGEXP_SUBSTR`) for **pattern-based cleaning** in databases like PostgreSQL and Oracle.
* Time bucketing (`DATE_TRUNC`) is very useful in **Power BI / Tableau time-series dashboards**.

---

## Aggregations & Analytical Computations in SQL

These functions and techniques allow you to perform **advanced data summarization and statistical analysis** directly inside SQL.
They help analysts calculate totals, averages, rankings, and statistical measures across groups or time periods — without external tools.

> 💡 In short: Aggregation and analytical functions turn **raw data into insights** by grouping, comparing, and computing trends.



| Category                              | Function(s)                                       | Description                                                                                      | Example                                                                                                                         |
| :------------------------------------ | :------------------------------------------------ | :----------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------ |
| **Advanced GROUP BY**                 | `GROUP BY` with multiple columns                  | Aggregate data across more than one dimension (e.g., region + category).                         | `sql<br>SELECT region, category, SUM(sales) FROM orders GROUP BY region, category;`                                             |
| **Rollups & Cubes**                   | `ROLLUP()`, `CUBE()`, `GROUPING SETS()`           | Generate hierarchical summaries and multi-level totals automatically.                            | `sql<br>SELECT region, category, SUM(sales) FROM orders GROUP BY ROLLUP(region, category);`                                     |
| **Percentiles & Ranking**             | `PERCENT_RANK()`, `CUME_DIST()`, `NTILE(4)`       | Calculate rank positions, cumulative distribution, and quartiles within result sets.             | `sql<br>SELECT name, salary, PERCENT_RANK() OVER(ORDER BY salary DESC) AS pct_rank FROM employees;`                             |
| **Statistical Functions**             | `STDDEV()`, `VARIANCE()`, `CORR()`, `COVAR_POP()` | Compute statistical metrics such as standard deviation, variance, and correlation (DB-specific). | `sql<br>SELECT STDDEV(sales), VARIANCE(sales) FROM orders;`                                                                     |
| **Conditional Aggregations**          | `SUM(CASE WHEN ...)`                              | Apply aggregate logic only to rows meeting a condition.                                          | `sql<br>SELECT department, SUM(CASE WHEN gender='M' THEN salary ELSE 0 END) AS male_salary FROM employees GROUP BY department;` |
| **Moving Averages / Rolling Windows** | `AVG() OVER()` with window frame                  | Calculate rolling or moving averages over time or sequence data.                                 | `sql<br>SELECT region, date, AVG(sales) OVER(PARTITION BY region ORDER BY date ROWS 6 PRECEDING) AS moving_avg FROM sales;`     |


### 🧠 **Notes:**

* Use `ROLLUP` for **subtotals and grand totals** automatically.
* `NTILE(4)` divides data into **quartiles**, great for distribution analysis.
* `WINDOW functions` like `AVG() OVER()` and `SUM() OVER()` are key for **trend and time-series analytics**.
* Most statistical functions (`STDDEV`, `VARIANCE`, `CORR`) depend on your SQL engine (e.g., PostgreSQL, Oracle, Snowflake).

---

## Database Objects for Analysts

Database objects are **structured components** that store, organize, and optimize data operations in SQL.
Analysts and developers use them to **simplify queries**, **reuse logic**, and **improve performance** for recurring analytical tasks.

> 💡 In short: Database objects make your SQL environment **modular, efficient, and scalable** for complex analysis.



| Object Type                       | Purpose                                                                                                                                                         | Example / Usage                                                                                                                                                     |
| :-------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Views**                         | A **virtual table** created from a SQL query. Helps simplify complex joins or aggregations into a single reusable object.                                       | `sql<br>CREATE VIEW sales_summary AS<br>SELECT region, SUM(sales) AS total_sales<br>FROM sales<br>GROUP BY region;`                                                 |
| **Materialized Views**            | Similar to views but **physically store** the query result for faster access. Useful in analytical systems (if supported by DBMS).                              | `sql<br>CREATE MATERIALIZED VIEW monthly_sales AS<br>SELECT DATE_TRUNC('month', order_date) AS month, SUM(amount) AS total_sales<br>FROM orders<br>GROUP BY month;` |
| **Indexes**                       | Improve query performance by allowing faster data retrieval. Can be **clustered** (data stored in index order) or **non-clustered** (separate index structure). | `sql<br>CREATE INDEX idx_customer_city ON customers(city);`                                                                                                         |
| **Stored Procedures / Functions** | Store **reusable SQL logic** (procedures) or return calculated results (functions). Great for repeated transformations or reports.                              | `sql<br>CREATE PROCEDURE get_sales_by_region()<br>BEGIN<br>  SELECT region, SUM(sales) FROM orders GROUP BY region;<br>END;`                                        |


### 🧠 **Notes:**

* **Views** help analysts avoid rewriting the same query multiple times.
* **Materialized Views** are ideal for **large datasets** with repetitive analytics — refresh periodically.
* **Indexes** improve performance but increase **storage and write overhead**, so use them strategically.
* **Stored Procedures** and **Functions** help encapsulate logic and make analysis pipelines reusable.

---

## Performance Optimization in SQL

Performance optimization focuses on writing **efficient SQL queries** that use minimal resources while delivering fast results — especially important when dealing with **large datasets**.
By understanding how the SQL engine executes your queries, you can significantly improve both speed and scalability.

> 💡 In short: Query optimization is about **doing more with less** — faster queries, fewer reads, and smarter resource usage.



| Technique                  | Description                                                                                                                                                              | Example / Usage                                                                                                                                                                                                                                  |
| :------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Query Execution Plans**  | Use `EXPLAIN` or `EXPLAIN ANALYZE` to understand how your query is executed — indexes used, joins applied, and cost estimation.                                          | `sql<br>EXPLAIN ANALYZE SELECT * FROM orders WHERE customer_id = 101;`                                                                                                                                                                           |
| **Avoiding `SELECT *`**    | Select only required columns instead of all. Reduces data transfer and speeds up queries.                                                                                | `sql<br>SELECT customer_id, order_date, total_amount FROM orders;`                                                                                                                                                                               |
| **Using Indexes Properly** | Indexes make lookups faster, but too many can slow down inserts/updates. Use them wisely for high-read columns.                                                          | `sql<br>CREATE INDEX idx_orders_customer ON orders(customer_id);`                                                                                                                                                                                |
| **Joins vs Subqueries**    | Prefer **joins** over correlated subqueries when possible — joins are often more efficient as they are optimized during query planning.                                  | `sql<br>-- Better<br>SELECT e.name, d.department_name<br>FROM employees e JOIN departments d<br>ON e.dept_id = d.id;`                                                                                                                            |
| **Partitioning**           | Splits large tables into smaller chunks (by date, region, etc.) to improve query speed and manageability.                                                                | `sql<br>CREATE TABLE orders_2025 PARTITION OF orders FOR VALUES IN ('2025');`                                                                                                                                                                    |
| **CTE vs Temp Tables**     | Common Table Expressions (`WITH`) improve readability but may not always be optimized for reuse. Temporary tables can perform better for large repeated data operations. | `sql<br>-- Using CTE<br>WITH sales_cte AS (SELECT * FROM sales WHERE region = 'North')<br>SELECT * FROM sales_cte WHERE amount > 500;<br><br>-- Using Temp Table<br>CREATE TEMP TABLE temp_sales AS SELECT * FROM sales WHERE region = 'North';` |


### 🧠 **Notes:**

* Always **analyze query plans** (`EXPLAIN ANALYZE`) before deploying queries in production.
* Use **indexes on JOIN keys and WHERE filters** for faster lookups.
* Avoid unnecessary subqueries or nested logic — use **CTEs or joins** for clarity and performance.
* **Partitioning** and **materialized views** help optimize large-scale analytical workloads.
* Test performance changes with **real data** — small samples can give misleading results.

---


## Analytical Scenarios (Real Data Use)

These are **real-world analytical SQL patterns** used by data analysts and business intelligence professionals.
They combine multiple SQL concepts — like joins, subqueries, window functions, and aggregates — to derive **actionable insights from data**.

> 💡 In short: These examples help you turn **raw transactional data** into **business insights** such as churn, retention, or top performers.



| Scenario                                        | Description                                                                                                           | Example SQL Pattern                                                                                                                                                                                                       |
| :---------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Customer Retention / Churn Analysis**         | Identify customers who made repeat purchases or those who haven’t returned within a given period.                     | `sql<br>SELECT customer_id, COUNT(DISTINCT order_date) AS purchase_count<br>FROM orders<br>GROUP BY customer_id<br>HAVING COUNT(DISTINCT order_date) > 1;`                                                                |
| **Cohort Analysis**                             | Group users by **signup month** (cohort) and measure how many are still active in later months.                       | `sql<br>SELECT DATE_TRUNC('month', signup_date) AS cohort,<br>DATE_TRUNC('month', last_active_date) AS active_month,<br>COUNT(DISTINCT user_id) AS retained_users<br>FROM users<br>GROUP BY cohort, active_month;`        |
| **RFM (Recency, Frequency, Monetary) Analysis** | Classify customers based on **Recency**, **Frequency**, and **Monetary value** using date differences and aggregates. | `sql<br>SELECT customer_id,<br> DATEDIFF(DAY, MAX(order_date), CURRENT_DATE) AS recency,<br> COUNT(order_id) AS frequency,<br> SUM(order_amount) AS monetary<br>FROM orders<br>GROUP BY customer_id;`                     |
| **Trend Analysis (Week-over-Week)**             | Measure weekly performance changes using **LAG()** to compare current vs previous period.                             | `sql<br>SELECT week, SUM(sales) AS total_sales,<br> LAG(SUM(sales)) OVER(ORDER BY week) AS prev_week_sales,<br> (SUM(sales) - LAG(SUM(sales)) OVER(ORDER BY week)) AS week_change<br>FROM weekly_sales<br>GROUP BY week;` |
| **Top-N Analysis (Category-Wise)**              | Find top-performing items, customers, or regions using **ROW_NUMBER() OVER()** ranking.                               | `sql<br>SELECT category, product_name, sales,<br> ROW_NUMBER() OVER(PARTITION BY category ORDER BY sales DESC) AS rank<br>FROM products_sales<br>WHERE rank <= 3;`                                                        |


### 🧠 **Notes:**

* These queries form the foundation of **real-world data analytics projects** and dashboards.
* Combine them with **CTEs**, **window functions**, and **aggregates** for advanced insights.
* Useful in **marketing analytics, e-commerce, finance, and SaaS** performance tracking.
* Most of these can be integrated easily into **Power BI**, **Tableau**, or **Python notebooks** for visualization.

---

## Integration & Data Science Readiness

Modern analytics doesn’t stop inside SQL — analysts often need to **export, integrate, or connect** SQL results with other tools like **Python, R, Power BI**, or **machine learning pipelines**.
This section shows how SQL becomes the **foundation of your data science workflow**.

> 💡 In short: SQL is not just for querying — it’s the **first step in your data science process**, powering visualizations, automation, and ML datasets.



| Task                                    | Description                                                                                                                                                             | Example / Usage                                                                                                                                                                                                     |
| :-------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Exporting Results to CSV / Excel**    | Export query results for reporting or further analysis. Most SQL clients and engines (like MySQL, PostgreSQL, Snowflake) support direct export or command-line options. | `sql<br>\COPY (SELECT * FROM sales_summary) TO 'sales_summary.csv' CSV HEADER;` *(PostgreSQL)*<br>or use client tools like MySQL Workbench → Export Results.                                                        |
| **Connecting SQL to Python**            | Use libraries like **`pandas`**, **`sqlalchemy`**, or **`psycopg2`** to query databases and load results into DataFrames.                                               | `python<br>import pandas as pd<br>import sqlalchemy<br>engine = sqlalchemy.create_engine('postgresql://user:pass@localhost/db')<br>df = pd.read_sql('SELECT * FROM sales_summary', engine)`                         |
| **Connecting SQL to R**                 | R’s **`DBI`** and **`RPostgres`** (or `RODBC`) packages connect to SQL databases for statistical analysis.                                                              | `R<br>library(DBI)<br>con <- dbConnect(RPostgres::Postgres(), dbname='analytics', host='localhost')<br>data <- dbGetQuery(con, 'SELECT * FROM customers')`                                                          |
| **Using SQL inside Power BI / Tableau** | Connect dashboards directly to SQL queries or stored views. Enables **real-time visualization** and filtering.                                                          | Create a **custom SQL query** connection inside Tableau or Power BI → paste your SQL (e.g., “SELECT region, SUM(sales) FROM sales GROUP BY region;”).                                                               |
| **Creating Analytical Datasets for ML** | Build **feature-ready datasets** using SQL joins, aggregations, and encodings before feeding into machine learning models.                                              | `sql<br>SELECT customer_id,<br> COUNT(order_id) AS order_freq,<br> AVG(order_amount) AS avg_value,<br> DATEDIFF(CURRENT_DATE, MAX(order_date)) AS days_since_last_purchase<br>FROM orders<br>GROUP BY customer_id;` |



### 🧠 **Notes:**

* SQL is often the **first layer** in any data science workflow — feature engineering, preprocessing, and aggregations start here.
* Use **CTEs and joins** to prepare complex datasets before importing into ML environments.
* Direct SQL connections in Power BI/Tableau help **avoid redundant data exports**.
* Export results with correct formats (CSV, Parquet) for compatibility with Python/R tools.


---

## Bonus (Optional but Impressive SQL Features)

These advanced SQL concepts are often used in **real-world enterprise analytics and data engineering**.
They go beyond standard querying — enabling complex transformations, time-series analytics, and semi-structured data handling.

> 💡 In short: These advanced features make your SQL skills stand out — perfect for interviews, projects, and big data work.



| Feature                                  | Description                                                                                                                                              | Example / Usage                                                                                                                                                                                                                                                                                                        |
| :--------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Recursive CTEs**                       | Used to handle **hierarchical or tree-structured data** (like org charts, file systems, or category trees). A CTE calls itself until a condition is met. | `sql<br>WITH RECURSIVE org_chart AS (<br>  SELECT employee_id, manager_id, name<br>  FROM employees<br>  WHERE manager_id IS NULL<br>  UNION ALL<br>  SELECT e.employee_id, e.manager_id, e.name<br>  FROM employees e<br>  INNER JOIN org_chart oc ON e.manager_id = oc.employee_id<br>)<br>SELECT * FROM org_chart;` |
| **JSON / Semi-Structured Data Handling** | Parse and extract data from JSON columns using built-in functions — useful in modern databases like MySQL, PostgreSQL, Snowflake, and BigQuery.          | `sql<br>SELECT JSON_EXTRACT(details, '$.customer.name') AS customer_name FROM orders;`                                                                                                                                                                                                                                 |
| **Array & Map Functions**                | Work with array or key-value (map) data types, common in analytical databases like BigQuery, Redshift, or Snowflake.                                     | `sql<br>SELECT customer_id, item FROM orders, UNNEST(items) AS item;`                                                                                                                                                                                                                                                  |
| **Advanced Window Frames**               | Define **custom time-based ranges** for moving calculations, useful for rolling metrics or trend analysis.                                               | `sql<br>SELECT date, SUM(sales) OVER (<br>  ORDER BY date<br>  RANGE BETWEEN INTERVAL '7' DAY PRECEDING AND CURRENT ROW<br>) AS seven_day_sales<br>FROM sales;`                                                                                                                                                        |


### 🧠 **Notes:**

* **Recursive CTEs** are great for exploring **hierarchical relationships** without procedural code.
* **JSON functions** make SQL powerful for working with **API or log data** in semi-structured form.
* **UNNEST()** and array functions simplify **exploding nested data** for analysis.
* **Window frame clauses** (like `RANGE BETWEEN`) help in **rolling time-based aggregations** — a key skill for analytics and forecasting.

---


