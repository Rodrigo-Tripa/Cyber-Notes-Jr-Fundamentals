#tools #sqlmap #sql-injection #web-security #databases

# SQLMap

SQLMap is an automated penetration-testing tool designed to detect and exploit SQL injection vulnerabilities in web applications. It automates many of the repetitive tasks involved in identifying injectable parameters and interacting with vulnerable database systems.

SQLMap is built around an important distinction: the tool does not create an SQL injection vulnerability. The application must already contain an input that can influence a database query in an unsafe way. SQLMap automates the process of detecting and exploiting that underlying weakness.

## SQL Injection

SQL injection occurs when untrusted user input is incorporated into an SQL query in a way that allows the input to alter the query's intended structure.

A vulnerable application might conceptually construct a query using externally supplied data:

`SELECT * FROM users WHERE username = '<input>';`

If the application treats the input as part of the SQL syntax instead of strictly as data, an attacker may be able to manipulate the resulting query.

This can potentially allow unauthorized access to database information, modification of data, authentication bypass, or other database-level actions depending on the application's privileges and the underlying database system.

Understanding [[SQL]] is therefore essential before using SQLMap. The tool automates the exploitation process, but understanding the database query and application behaviour is necessary to interpret its results correctly.

## Injectable Parameters

SQLMap tests parameters that influence application requests. These parameters can occur in different parts of an HTTP request, depending on the application.

Potential injection points can include:

* URL query parameters
* Form parameters
* HTTP POST data
* Cookies
* HTTP headers
* Other application-controlled input

The important property is that the parameter must eventually influence an SQL query executed by the backend.

This means that identifying an interesting parameter does not automatically mean it is vulnerable. The application must process that parameter in a way that permits manipulation of the underlying SQL statement.

## Detection and Exploitation

SQLMap can automate the detection of SQL injection by sending specially constructed requests and analysing how the application's responses change.

Depending on the injection technique and target database, SQLMap can identify whether a parameter appears injectable and determine characteristics of the underlying database interaction.

Once an injection is confirmed, SQLMap can automate subsequent enumeration and extraction activities.

The general progression is:

`Identify Parameter → Test Injection → Identify Database → Enumerate Structure → Retrieve Data`

This automation is valuable because manually performing each stage of SQL injection testing can require a large number of carefully constructed requests.

## Database Enumeration

SQLMap can interact with vulnerable database systems to enumerate their structure.

Depending on the privileges available through the injection, this can include discovering:

* Database management system
* Database names
* Tables
* Columns
* Stored records
* Database users
* Database privileges

The amount of information available is determined by the vulnerability, database configuration, privileges of the application's database account, and the injection technique.

A SQL injection does not automatically provide unrestricted access to the entire database server. The application's database privileges remain an important security boundary.

## Injection Techniques

SQL injection can be exploited through multiple techniques. SQLMap can automatically select or test techniques depending on the behaviour of the target.

Important categories include:

**Boolean-based blind SQL injection** relies on differences in application behaviour between true and false conditions. The application may not directly return database information, but its responses can reveal whether a condition was evaluated as true.

**Time-based blind SQL injection** uses measurable response delays to infer information. When the application does not reveal query results or meaningful response differences, timing behaviour can sometimes provide a side channel.

**Error-based SQL injection** uses database error messages to extract information or infer query behaviour. It depends on the application exposing useful database errors.

**UNION-based SQL injection** attempts to combine an attacker-controlled query with the application's original query using SQL `UNION` operations. When the conditions are suitable, this can allow additional database information to be returned through the normal application response.

The practical applicability of each technique depends on the database, query structure, application behaviour, and defensive controls.

## Request Context

SQLMap operates against web applications, so understanding [[HTTP]] is important. An HTTP request contains information such as the method, URL, parameters, headers, cookies, and potentially request bodies. SQLMap can use this request context when testing an application.

This is particularly important for authenticated applications. A vulnerable parameter may only be accessible after authentication, meaning that the relevant session information must be available to the testing process.

Tools such as [[Burp Suite]] can also be useful for inspecting and understanding HTTP requests before automated SQL injection testing.

## Defensive Perspective

The primary defence against SQL injection is to prevent untrusted input from being interpreted as executable SQL syntax.

Parameterized queries and prepared statements provide a strong defence because SQL structure and user-supplied data are handled separately.

Additional defensive measures include:

* Applying least privilege to database accounts
* Validating input appropriately
* Avoiding dynamically constructed SQL where possible
* Suppressing unnecessary database error information
* Monitoring suspicious database activity
* Keeping database systems and applications maintained

Input validation alone should not be treated as the primary defence. Proper query parameterization addresses the underlying problem by separating data from SQL instructions.

## SQLMap in a Penetration Test

SQLMap is generally used after reconnaissance and vulnerability identification have established a potentially injectable application parameter.

A simplified workflow is:

`Reconnaissance → Web Enumeration → Parameter Identification → SQL Injection Testing → Database Enumeration → Impact Assessment`

[[Gobuster]] can help discover additional web resources, while [[Burp Suite]] can be used to inspect application requests. SQLMap then provides automation for the SQL injection testing and enumeration stages.

The result is a good example of how individual offensive-security tools complement one another rather than functioning independently.

## Related Notes

* [[SQL]]
* [[HTTP]]
* [[HTTPS]]
* [[Burp Suite]]
* [[Gobuster]]
* [[Web-Architecture]]
* [[Offensive-Security]]
* [[Defensive-Security]]
