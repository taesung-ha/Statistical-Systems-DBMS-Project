# Lecture Note: Modern SQL & dbt (CMU Intro to DB)

## 1. The Survival of SQL
Honestly, it’s crazy that SQL was invented in the early 70s (System R at IBM) and it's still the king. People keep saying "Natural Language" or "LLMs" will replace it, but as Andy says, SQL was here before we were born and will probably be here after we die. It keeps evolving—the latest SQL:2023 standard even added things like property graph queries.

### Key Concepts:
*   <strong>Relational Model vs. SQL:</strong> Relational model is based on <strong>Sets</strong> (no duplicates), but SQL is based on <strong>Bags</strong> (duplicates allowed). This is a huge practical distinction.
*   <strong>The Three Pillars:</strong> 
    1.  <strong>DML (Data Manipulation):</strong> SELECT, INSERT, UPDATE, DELETE.
    2.  <strong>DDL (Data Definition):</strong> CREATE TABLE, CREATE INDEX.
    3.  <strong>DCL (Data Control):</strong> GRANT, REVOKE (Permissions).

## 2. The "Dialect" Nightmare
One of the funniest parts of the lecture was seeing how inconsistent SQL is across different systems. 
*   <strong>Strings:</strong> Most are case-sensitive and use single quotes (`'`), but MySQL is case-insensitive and allows double quotes (`"`). 
*   <strong>Date Math:</strong> This is a total mess. Calculating "Days from Jan 1st to Now" requires a different function in almost every DB (e.g., `DATEDIFF` in MySQL vs. simple subtraction in Postgres vs. Julian days in SQLite).

## 3. Aggregations & Grouping
We use aggregate functions (AVG, MIN, MAX, COUNT) to collapse multiple tuples into a single value.
*   <strong>GROUP BY:</strong> Used to partition data into clusters before aggregating.
*   <strong>HAVING vs. WHERE:</strong> This is important. `WHERE` filters before aggregation; `HAVING` filters after. Some DBs won't let you use aliases in the `HAVING` clause because of the execution order.

## 4. Advanced Query Patterns
### Nested Queries
You can put a SELECT inside another SELECT. While powerful, the "dumb" way to run these is like nested loops (very slow). Modern systems like Umbra or DuckDB are getting better at rewriting these into joins.

### CTEs (Common Table Expressions)
Instead of messy nested queries, use the `WITH` clause. It’s like creating a temporary macro/table that exists only for that query. Much more readable and helps "software engineer" your SQL.

### Window Functions
The `OVER` and `PARTITION BY` clauses. This is how you do "moving averages" or "rankings" without collapsing the rows into a single group. It keeps the individual row identity while still performing a calculation across a "window" of data.

## 5. dbt (Data Build Tool)
Drew from dbt Labs gave a guest talk. The big takeaway is that in real-world companies, the data warehouse is usually a "giant mess" of raw tables. 
*   <strong>What dbt does:</strong> It’s a transformation layer. You write SQL (plus some Jinja templates) to define how raw data becomes clean, business-ready tables.
*   <strong>Why it matters:</strong> It brings software engineering best practices—Version Control (Git), CI/CD, and Data Lineage (seeing exactly where a column comes from)—to the world of data analytics.

---
*Next up: Storage Engines & how the DB actually stores these bits on disk!*