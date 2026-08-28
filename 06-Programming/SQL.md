#sql #programming #databases #web-security

# SQL

SQL (Structured Query Language) is a language used to interact with relational database management systems. It allows applications and administrators to retrieve, insert, modify, and delete structured data while also providing mechanisms for defining database structures and controlling access.

Relational databases organize information into tables containing rows and columns. Tables can be related to one another through keys, allowing complex datasets to be represented while reducing unnecessary duplication.

## Relational Database Model

A table represents a collection of related records. Each row represents a record, while each column represents an attribute of that record.

A primary key uniquely identifies a row within a table. Foreign keys establish relationships between tables by referencing keys in another table.

For example, an application might separate users and orders into different tables and connect them through a user identifier. This allows the database to represent relationships without storing the same user information repeatedly.

## Queries

The `SELECT` statement retrieves data from one or more tables. Filtering can be performed using conditions, while sorting and limiting can control the resulting dataset.

SQL can combine information from multiple tables using joins. Common join types include `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`. Understanding joins is essential for interpreting how relational data is connected.

Aggregation functions such as `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX` allow calculations to be performed over groups of records. `GROUP BY` organizes records into groups for aggregation, while `HAVING` can filter the resulting groups.

## Data Modification

SQL provides statements for inserting, modifying, and deleting records. These operations are commonly used by applications when users create accounts, update information, or remove data.

Database transactions allow multiple operations to be treated as a logical unit. Transactional systems commonly provide properties described by the ACID model: atomicity, consistency, isolation, and durability.

## Database Design

Good relational database design aims to maintain data integrity while avoiding unnecessary duplication. Normalization divides data into logically related tables and establishes relationships between them.

Constraints can enforce rules at the database level. Examples include primary keys, foreign keys, unique constraints, and checks. These mechanisms help prevent invalid states from being introduced into the database.

Indexes improve query performance by providing additional structures that allow the database engine to locate records more efficiently. However, indexes consume storage and can increase the cost of data modification.

## SQL and Applications

Web applications commonly use SQL databases as their persistent storage layer. A typical application receives an HTTP request, validates the input, executes a database operation, and returns the resulting data to the client.

This creates an important security boundary between [[HTTP]], application code, and the database. SQL should normally be constructed through parameterized queries or equivalent safe database interfaces rather than by directly concatenating untrusted user input into SQL statements.

## SQL Injection

SQL injection occurs when attacker-controlled input is incorporated into a database query in a way that changes the intended SQL syntax or semantics.

The vulnerability generally results from insufficient separation between data and executable query structure. Depending on the application's database privileges and behaviour, SQL injection can allow unauthorized data access, modification of database contents, authentication bypass, or other unintended operations.

Parameterized queries, prepared statements, appropriate input handling, least-privilege database accounts, and carefully designed application interfaces are important defensive measures.

SQL injection is closely related to the principles covered by [[OWASP-Top-10]] and should be understood as an application-layer vulnerability rather than simply a database problem.

## Security Relevance

Security professionals need to understand SQL both to assess applications and to investigate systems that depend on relational databases. Knowledge of schemas, relationships, queries, permissions, transactions, and query construction makes it possible to distinguish normal database behaviour from potentially malicious activity.

SQL knowledge also provides the foundation for understanding database-focused security tools such as [[SQLMap]].

## Related Concepts

- [[Data-Representation]]
- [[Data-Encoding]]
- [[HTTP]]
- [[Web-Architecture]]
- [[OWASP-Top-10]]
- [[SQLMap]]