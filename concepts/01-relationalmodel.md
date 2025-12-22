

# 01 - Relational Model & Algebra


## 1. Course Info & Logistics

This course is all about how relational database systems work under the hood. Enrollment and waitlists change every semester, and the admin team handles the details. All announcements and Q&A are done online (Piazza, etc.), and grades are posted on Canvas. Anyone can follow along with the public materials, but only enrolled students can submit assignments. The first project is a simple multithreaded data structure—it's required to stay in the class.


## 2. Course Goals & Expectations

The main goal is to understand how DBMSs actually work, not just how to use Oracle or MySQL. The focus is on the computer science behind the scenes. Projects use BusTub (C++20), and you'll need to pick up C++ on your own if you aren't already comfortable with it.


## 3. Plagiarism & AI Tools

All work must be your own. Using generative AI tools is allowed, but if you don't understand the basics, you won't know if the code is right. After Project 1, there's a leaderboard for code performance and a chance for extra credit.


## 4. Industry & Seminars

Every Wednesday, there are guest lectures from people working in the data industry, which helps connect theory to real-world systems. There are also recruiting sessions for internships and jobs. This semester's optional seminar series is about data lake systems and current trends.


## 5. Personal Notes & Outreach

The instructor says databases are the second most important thing in his life. He also sends learning materials to people in prison, as part of outreach to underserved communities.


## 6. Why Databases Matter & Lecture Overview

Databases are at the core of almost every information system. This lecture covers the background of data systems, the basics of the relational model, and then moves on to relational algebra and other data models.


## 7. Database vs. Data System

Postgres and MySQL are data systems (software), while a database is the actual collection of data that models the real world. Data systems help store, analyze, and query data. For new projects, it's best to use proven open-source systems like Postgres instead of building your own. A data model is a set of rules for representing data (relational, document, etc.), and a schema is the concrete design for your data. Most modern systems use the relational model, but there are also key-value, array, hierarchical, and network models.


## 8. Why CSV Files Fall Short

If you try to manage data like artists and albums with a CSV file, you run into a lot of problems:
- Every search is a linear scan, which is slow.
- All data is stored as strings, so you have to convert types for calculations.
- Code is tied to field order, making it inflexible.
- You have to rewrite logic for every new programming language.
- It's hard to guarantee integrity (ACID), model relationships, handle concurrency, or recover from crashes.
There have even been real-world cases where unsafe default settings in a DBMS led to data loss. Understanding these fundamentals is important.


## 9. Historical Background of Data Models

In the 1960s and 70s, systems like GE's IDM and IBM's IMS appeared. There was no SQL, so people wrote procedural code to work with low-level data structures. In 1974, Ted Codd's relational model was recognized as the best approach and became the standard.


## 10. Key Concepts of the Relational Model

Data is organized as sets called relations. Each row is a tuple, and each attribute has a domain (the set of allowed values). Relationships are expressed logically by values, not by physical pointers. The primary key uniquely identifies each tuple, and foreign keys link tables together. Many-to-many relationships use a separate cross-reference table. With SQL, you declare what you want, and the system figures out the best way to get it.


## 11. Data Independence

The relational model separates physical storage from logical structure, so changes at a lower level don't break things higher up. The layers go: storage → physical schema → logical schema → external schema (views) → application. Physical independence means you can change storage without breaking apps; logical independence means you can change the schema and hide it with views.


## 12. DML & Relational Algebra

Data manipulation languages include procedural (relational algebra) and declarative (like SQL) styles. Relational algebra spells out the steps, while SQL just says what you want. Main operators:
- Selection (σ): filter rows (like SQL WHERE)
- Projection (π): pick columns (like SQL SELECT)
- Union (∪), Intersection (∩), Difference (−): set operations on tables with the same structure
- Cartesian product (×): all combinations (CROSS JOIN)
- Join: combine rows from different tables based on a condition
The order of operations can have a big impact on performance, but SQL lets the system choose the best plan.