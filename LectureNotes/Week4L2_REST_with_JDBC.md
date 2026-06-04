# Web Services

# Week 4 — JDBC and Database-Driven Web Services

**Course:** Web Services
**Week:** 4
**Sessions:** 3

---

# Week 4 Learning Outcomes

By the end of this week, students will be able to:

* Explain the purpose and architecture of JDBC.
* Connect a Java application to SQL Server.
* Execute SQL queries from Java.
* Use JDBC to perform CRUD operations.
* Prevent SQL Injection using PreparedStatement.
* Connect a Servlet to a SQL Server database.
* Generate dynamic JSON responses from database data.
* Build a database-driven web service.

---

# Session 1 — JDBC Fundamentals

---

# Learning Objectives

* Describe the role of JDBC.
* Explain JDBC architecture.
* Connect Java applications to SQL Server.
* Execute SELECT statements.
* Process query results using ResultSet.

---

# Theory Notes:

## What is JDBC?

JDBC (Java Database Connectivity) is a Java API that enables Java applications to communicate with relational databases.

JDBC allows applications to:

* Connect to a database
* Execute SQL statements
* Retrieve data
* Insert data
* Update data
* Delete data

---

## Why Do We Need JDBC?

Without JDBC:

```text
Java Application
```

With JDBC:

```text
Java Application
        ↓
      JDBC
        ↓
   SQL Server
```

JDBC acts as a bridge between Java applications and databases.

---

## JDBC Architecture

```text
Java Application
        ↓
      JDBC API
        ↓
    JDBC Driver
        ↓
    SQL Server
```

### Main Components

#### DriverManager

Responsible for establishing database connections.

```java
Connection conn =
    DriverManager.getConnection(url, user, password);
```

---

#### Connection

Represents an active connection to the database.

```java
Connection conn;
```

---

#### Statement

Used to execute SQL statements.

```java
Statement stmt =
    conn.createStatement();
```

---

#### ResultSet

Stores records returned by a query.

```java
ResultSet rs =
    stmt.executeQuery(sql);
```

---

## SQL Server JDBC Driver

The SQL Server JDBC Driver allows Java applications to communicate with SQL Server.

### Maven Dependency

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>12.8.1.jre11</version>
</dependency>
```

---

## JDBC Workflow

A typical JDBC program follows these steps:

```text
1. Open Connection
2. Create Statement
3. Execute SQL Query
4. Process Results
5. Close Resources
```

---

# Lab 1 — Connecting Java to SQL Server

## Database Setup

Create the following database:

```sql
CREATE DATABASE CollegeDB;
GO

USE CollegeDB;
GO

CREATE TABLE Student (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

INSERT INTO Student VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Charlie');
```

---

## Task 1 — Create Project

Create a Java project named:

```text
JDBCDemo
```

Add the SQL Server JDBC Driver dependency.

---

## Task 2 — Create Database Connection

```java
 String url = "jdbc:sqlserver://localhost:1433;databaseName=CollegeDB;encrypt=false;trustServerCertificate=true;";

        String user = "sa";
        String password = "password"; //admin

Connection conn =
    DriverManager.getConnection(url, user, password);

System.out.println("Connected Successfully");
```

---

## Task 3 — Execute SELECT Query

```java
Statement stmt =
    conn.createStatement();

ResultSet rs =
    stmt.executeQuery("SELECT * FROM Student");
```

---

## Task 4 — Display Results

```java
while(rs.next()) {

    System.out.println(
        rs.getInt("id") + " " +
        rs.getString("name")
    );
}
```

---

## Expected Output

```text
1 Alice
2 Bob
3 Charlie
```

---

## Deliverables

Show the instructor:

* Successful database connection
* Student records displayed in the console

---

# Session 2 — JDBC CRUD Operations

---

# Learning Objectives

By the end of this session, students will be able to:

* Use PreparedStatement.
* Explain SQL Injection risks.
* Implement CRUD operations using JDBC.

---

# Theory Notes 

## SQL Injection

SQL Injection occurs when user input is directly combined with SQL statements.

### Unsafe Example

```java
String sql =
    "SELECT * FROM Student WHERE id=" + userInput;
```

If the user enters:

```text
1 OR 1=1
```

Generated SQL:

```sql
SELECT * FROM Student
WHERE id = 1 OR 1 = 1
```

This may return all records.

---

## PreparedStatement

PreparedStatement prevents SQL Injection by separating SQL code from user input.

### Example

```java
PreparedStatement ps =
    conn.prepareStatement(
        "SELECT * FROM Student WHERE id=?");
```

Assign value:

```java
ps.setInt(1, id);
```

Execute query:

```java
ResultSet rs = ps.executeQuery();
```

---

# CRUD Operations

| Operation | SQL Command |
| --------- | ----------- |
| Create    | INSERT      |
| Read      | SELECT      |
| Update    | UPDATE      |
| Delete    | DELETE      |

---

# Lab 2 — Implementing CRUD Operations

## Task 1 — Create StudentDAO Class

Create the following methods:

```java
addStudent()
getStudentById()
updateStudent()
deleteStudent()
```

---

## Task 2 — Add Student

```java
public void addStudent(int id, String name)
        throws SQLException {

    String sql =
        "INSERT INTO Student VALUES(?, ?)";

    PreparedStatement ps =
        conn.prepareStatement(sql);

    ps.setInt(1, id);
    ps.setString(2, name);

    ps.executeUpdate();
}
```

---

## Task 3 — Retrieve Student by ID

```java
public void getStudentById(int id)
        throws SQLException {

    String sql =
        "SELECT * FROM Student WHERE id=?";

    PreparedStatement ps =
        conn.prepareStatement(sql);

    ps.setInt(1, id);

    ResultSet rs = ps.executeQuery();

    while(rs.next()) {

        System.out.println(
            rs.getInt("id") + " " +
            rs.getString("name")
        );
    }
}
```

---

## Task 4 — Update Student

SQL:

```sql
UPDATE Student
SET name = ?
WHERE id = ?
```

Create method:

```java
updateStudent(int id, String name)
```

---

## Task 5 — Delete Student

SQL:

```sql
DELETE FROM Student
WHERE id = ?
```

Create method:

```java
deleteStudent(int id)
```

---

## Deliverables

Demonstrate:

* Insert Student
* Retrieve Student
* Update Student
* Delete Student

using Java code.

---

# Session 3 — Servlets + JDBC

---

# Learning Objectives

* Connect a Servlet to SQL Server.
* Execute database queries from a Servlet.
* Generate JSON dynamically.
* Return database records through a Web Service.

---

# Theory Notes 

## Current Application Architecture

Currently, the servlet returns hardcoded data.

```text
Postman
   ↓
Servlet
   ↓
Hardcoded JSON
```

Example:

```json
[
  {
    "id": 1,
    "name": "Alice"
  },
  {
    "id": 2,
    "name": "Bob"
  }
]
```

### Problem

* Data cannot be updated easily.
* Data is not stored in a database.
* Not suitable for real applications.

---

## New Architecture

```text
Postman
    ↓
 Servlet
    ↓
   JDBC
    ↓
SQL Server
```

### Benefits

* Dynamic data
* Real-time updates
* Scalable architecture
* Foundation for REST APIs

---

## Request Processing Flow

```text
Client Request
      ↓
Servlet
      ↓
Database Query
      ↓
Build JSON
      ↓
Send Response
```

---

# Lab 3 — Database-Driven Servlet

## Existing Servlet

Current implementation:

```java
String json =
"[{\"id\":1,\"name\":\"Alice\"}," +
 "{\"id\":2,\"name\":\"Bob\"}]";

response.getWriter().write(json);
```

---

## Goal

Replace hardcoded JSON with records retrieved from SQL Server.

---

## Task 1 — Connect to Database

Inside the servlet:

```java
Connection conn =
DriverManager.getConnection(
    url,
    user,
    password
);
```

---

## Task 2 — Execute Query

```java
SELECT * FROM Student
```

Retrieve all student records.

---

## Task 3 — Build JSON Response

Generate JSON dynamically.

Example:

```json
[
  {
    "id": 1,
    "name": "Alice"
  },
  {
    "id": 2,
    "name": "Bob"
  }
]
```

---

## Task 4 — Return JSON Response

Set content type:

```java
response.setContentType("application/json");
```

Send JSON:

```java
response.getWriter().write(json);
```

---

## Task 5 — Test Using Postman

Request:

```http
GET
http://localhost:7070/StudentServlet_war_exploded/students
```

Expected Response:

```json
[
  {
    "id": 1,
    "name": "Alice"
  },
  {
    "id": 2,
    "name": "Bob"
  }
]
```

Data must come from SQL Server.

---

# Bonus Challenge

Implement:

```http
GET /students?id=1
```

Expected Response:

```json
{
  "id": 1,
  "name": "Alice"
}
```

Use:

* request.getParameter()
* PreparedStatement
* ResultSet

to retrieve a specific student.

---

# Week 4 Summary


* JDBC Architecture
* SQL Server Connectivity
* Connection, Statement, ResultSet
* PreparedStatement
* SQL Injection Prevention
* CRUD Operations Using JDBC
* Servlets and Database Integration
* Dynamic JSON Generation
* Building Database-Driven Web Services

These concepts form the foundation for building complete RESTful Web Services and will lead the road to Spring Boot and JPA later in the course.
