#  Web Services

# Week 6 — Introduction to Spring Boot and Spring MVC

**Course:** Web Services

**Week:** 6

**Sessions:** 3

**Duration per Session:** 3 Hours

- Theory: 20–30 minutes
-  Guided Lab: ~2 hours
- 💬 Questions, troubleshooting and demonstrations: Remaining time

---

#  Week 6 Learning Outcomes

✔ Explain the purpose of Spring Boot.

✔ Compare Java Servlets, Spring MVC, and Spring Boot.

✔ Create a simple Spring Boot application.

✔ Run Spring Boot applications from IntelliJ IDEA.

✔ Explain the MVC architecture.

✔ Create a simple Spring MVC application.

✔ Display hard-coded student data in a web page.

✔ Connect Spring Boot to SQL Server.

✔ Retrieve, insert, update and delete database records.

✔ Build the foundation for RESTful APIs using Spring Boot.

---

#  Session 1 — Introduction to Spring Boot

---

#  Learning Objectives

- Explain why Spring Boot was created.
- Compare Java Servlet and Spring Boot.
- Create a simple Spring Boot application.
- Run a Spring Boot application.
- Access a Spring Boot endpoint from a browser.

---

#  Theory Notes (20–30 min)

# 1️⃣ What is Spring Boot?

Spring Boot is a Java framework that simplifies the development of modern web applications.

Spring Boot automatically configures many components that previously required manual setup.

Spring Boot helps developers create applications faster with less code.

---

# Why was Spring Boot created?

Traditional Java web development required configuring:

- Tomcat
- web.xml
- Servlets
- Maven dependencies
- Application servers

Spring Boot reduces this complexity.

---

# Traditional Java Servlet Architecture

```text
Browser
   ↓
Tomcat
   ↓
Servlet
   ↓
Java Code
```

---

# Spring Boot Architecture

```text
Browser
   ↓
Spring Boot
   ↓
Controller
   ↓
Business Logic
```

---

# Servlet vs Spring Boot

| Java Servlet             | Spring Boot |
|--------------            |-------------|
| More configuration       | Minimal configuration |
| Requires external Tomcat | Embedded Tomcat |
| Manual setup             | Automatic setup |
| More boilerplate code    | Less code |
| Older approach           | Modern approach |

---

# Why Learn Spring Boot?

Spring Boot is the industry-standard framework for 'enterprise Java development', 
widely adopted for building scalable microservices and robust production backends.

Companies use it to build:

- REST APIs
- Web applications
- Enterprise systems
- Microservices

---

# Spring Boot Terminology

## Starter

Preconfigured dependencies.

Example:

```text
spring-boot-starter-web
```

Includes:

- Spring MVC
- Jackson JSON
- Embedded Tomcat

---

## Embedded Tomcat

Tomcat is included inside the application.

No separate installation is required.

Run:

```text
Run Application
```

instead of:

```text
startup.bat
```

---

# Spring Boot Request Flow

```text
Browser
   ↓
Controller
   ↓
Response
```

---

#  Lab 1 — Create Your First Spring Boot Application

---

# Goal

Display:

```text
Hello Spring Boot
```

in a browser.

---

# Method 1 — Using IntelliJ IDEA

---

## Step 1

File

→ New

→ Project

---

## Step 2

Choose:

```text
Spring Initializr
```

---

## Step 3

Configure:

```text
Name: HelloSpringBoot

Language: Java

Build: Maven

JDK: 21

Packaging: Jar
```

---

## Step 4

Add dependency:

```text
Spring Web
```

---

## Step 5

Click:

```text
Create
```

---

# Method 2 — Using Spring Initializr Website

Visit:

```text
https://start.spring.io
```

Select:

```text
Project: Maven

Language: Java

Spring Boot: latest stable version

Java: 21

Dependency:
Spring Web
```

Download the ZIP file.

Open it in IntelliJ.

---

# Create Controller

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")

    public String hello() {

        return "Hello Spring Boot";
    }
}
```

---

# Run Application

Run:

```java
DemoApplication.java
```

---

# Test

Open browser:

```text
http://localhost:6060/hello
```

Expected output:

```text
Hello Spring Boot
```

---

# Deliverables

Show the instructor:

✔ Project running

✔ Browser displaying:

```text
Hello Spring Boot
```

---

#  Session 2 — Spring MVC

---

# Learning Objectives

- Explain MVC architecture.
- Compare Spring MVC and Spring Boot.
- Create a simple Spring MVC application.
- Display hardcoded student data.

---

#  Theory Notes (20–30 min)

# What is MVC?

MVC stands for:

```text
Model
View
Controller
```

---

# MVC Responsibilities

## Model

Stores data.

Example:

```text
Student
```

---

## View

Displays data.

Example:

```text
HTML page
```

---

## Controller

Receives requests.

Processes data.

Sends data to the View.

---

# MVC Diagram

```text
Browser
   ↓
Controller
   ↓
Model
   ↓
View
   ↓
Browser
```

---

# Spring MVC vs Spring Boot

| Spring MVC             | Spring Boot |
|------------            |-------------|
| Framework              | Framework + Auto Configuration |
| Requires setup         | Automatic setup |
| More configuration     | Less configuration |
| No embedded server     | Embedded Tomcat |
| Used inside Spring Boot| Modern development |

---

#  Lab 2 — Create Student MVC Application

---

# Goal

Display a list of students.

---

# Student Model

```java
public class Student {

    private int id;

    private String name;

    private String major;

    // constructors

    // getters

    // setters
}
```

---

# Student Controller

```java
@Controller

public class StudentController {

    @GetMapping("/students")

    public String getStudents(Model model) {

        List<Student> students =
                new ArrayList<>();

        students.add(
                new Student(
                        1,
                        "Alice",
                        "Computer Science"));

        students.add(
                new Student(
                        2,
                        "Bob",
                        "Software Engineering"));

        students.add(
                new Student(
                        3,
                        "Charlie",
                        "Computer Science"));

        model.addAttribute(
                "students",
                students);

        return "students";
    }
}
```

---

# students.html

```html
<!DOCTYPE html>

<html xmlns:th=
"http://www.thymeleaf.org">

<body>

<h1>Students</h1>

<table border="1">

<tr>

<th>ID</th>

<th>Name</th>

<th>Major</th>

</tr>

<tr th:each="s : ${students}">

<td th:text="${s.id}"></td>

<td th:text="${s.name}"></td>

<td th:text="${s.major}"></td>

</tr>

</table>

</body>

</html>
```

---

# Test

```text
http://localhost:6060/students
```

Expected:

```text
1 Alice Computer Science

2 Bob Software Engineering

3 Charlie Cyber Security
```

---

# Deliverables

Show the instructor:

✔ Student.java

✔ StudentController.java

✔ students.html

✔ Browser output

---

#  Session 3 — Spring Boot + SQL Server

---

#  Learning Objectives


- Connect Spring Boot to SQL Server.
- Retrieve database data.
- Insert records.
- Update records.
- Delete records.

---

#  Theory Notes 

# Architecture

```text
Browser
   ↓
Controller
   ↓
Repository
   ↓
SQL Server
```

---

# Spring Data JPA

Spring Data JPA simplifies database access.

Instead of writing JDBC code manually:

```java
Connection

Statement

PreparedStatement

ResultSet
```

Spring Data JPA automates these tasks.

---

# CRUD Operations

| Operation | SQL |
|-----------|-----|
| Create | INSERT |
| Read | SELECT |
| Update | UPDATE |
| Delete | DELETE |

---

#  Lab 3 — Connect to Existing SQL Server Database

---

# Step 1

Use the existing database:

```text
CollegeDB
```

Table:

```text
Student
```

---

# Step 2

Add Dependencies

```xml
<dependency>

<groupId>
org.springframework.boot
</groupId>

<artifactId>
spring-boot-starter-data-jpa
</artifactId>

</dependency>

<dependency>

<groupId>
com.microsoft.sqlserver
</groupId>

<artifactId>
mssql-jdbc
</artifactId>

</dependency>
```

---

# Step 3

Configure application.properties

```properties
spring.datasource.url=
jdbc:sqlserver://localhost:1433;
databaseName=CollegeDB;
encrypt=false;
trustServerCertificate=true

spring.datasource.username=sa

spring.datasource.password=admin

spring.jpa.hibernate.ddl-auto=none
```

---

# Step 4

Create Entity

```java
@Entity

public class Student {

    @Id

    private int id;

    private String name;

    private String major;

}
```

---

# Step 5

Create Repository

```java
@Repository

public interface StudentRepository

extends JpaRepository<Student,Integer> {

}
```

---

# Step 6

Create Controller

```java
@RestController

@RequestMapping("/students")

public class StudentController {

    @Autowired

    StudentRepository repository;

    @GetMapping

    public List<Student> getAll() {

        return repository.findAll();
    }

    @PostMapping

    public Student add(

            @RequestBody

            Student student) {

        return repository.save(student);
    }

    @PutMapping("/{id}")

    public Student update(

            @PathVariable int id,

            @RequestBody Student student) {

        student.setId(id);

        return repository.save(student);
    }

    @DeleteMapping("/{id}")

    public void delete(

            @PathVariable int id) {

        repository.deleteById(id);
    }
}
```

---

# Test Using Postman

---

# Get All Students

```http
GET

http://localhost:6060/students
```

---

# Add Student

```http
POST

http://localhost:8080/students
```

Body:

```json
{
  "id":4,
  "name":"David",
  "major":"AI"
}
```

---

# Update Student

```http
PUT

http://localhost:8080/students/4
```

Body:

```json
{
  "name":"David Updated",
  "major":"Data Science"
}
```

---

# Delete Student

```http
DELETE

http://localhost:6060/students/4
```

---

# Deliverables

Show:

✔ SQL Server connection working

✔ GET works

✔ POST works

✔ PUT works

✔ DELETE works

✔ Postman screenshots

---

#  Week 6 Summary

What is covered:

✔ Introduction to Spring Boot

✔ Java Servlet vs Spring Boot

✔ Spring MVC architecture

✔ MVC application development

✔ Thymeleaf views

✔ Spring Data JPA

✔ SQL Server integration

✔ CRUD operations

✔ Building modern database-driven applications

---

#  Looking Ahead

These concepts will prepare students for:

- Building complete REST APIs

- REST Controllers

- JSON serialization

- JPA repositories

- Layered architecture

- Enterprise application development

### If DB connection attempts kept being created without connecting:  
A Connection reset error in IntelliJ with SQL Server usually comes down to: 
 * disabled TCP/IP protocols, encryption/SSL mismatches, or using the wrong port.
 * Here is how to fix it step-by-step:1.
    * Enable TCP/IP in SQL Server Configuration ManagerBy default, SQL Server developer and express editions have network protocols turned off.
    * Press Win + R, type sqlservermanager17.msc (for SQL Server 2025) or search your Start menu for SQL Server Configuration Manager.
    * Expand SQL Server Network Configuration $\rightarrow$
    * Click on Protocols for MSSQLSERVER (or your specific instance name).
    * Look at TCP/IP. If it says Disabled, right-click it and choose Enable.
    * Double-click TCP/IP, go to the IP Addresses tab, scroll all the way to the bottom to IPAll, and ensure the TCP Port is set to 1433.
    * Click Apply/OK, then restart the SQL Server service via the "SQL Server Services" tab on the left.
    * 2. Fix the IntelliJ Connection String (Trust Certificate)Modern JDBC drivers used by IntelliJ enforce strict encryption by default. Because SQL Server 2025 uses self-signed certificates out of the box, IntelliJ will often instantly drop ("reset") the connection.
     * 3. In your IntelliJ Database tool window:Open your Data Source settings for this connection. Look for the URL or connection string. It should look like this (notice the port is 1433, not 1434):
    
'jdbc:sqlserver://localhost:1433;databaseName=CollegeDB;trustServerCertificate=true;encrypt=false;'

Alternatively, go to the Advanced tab in the IntelliJ data source properties window, find the following properties, and set them manually:encrypt: Set to false (or true if you want encryption).trustServerCertificate: Set to true (This tells IntelliJ to trust your local SQL Server certificate).
