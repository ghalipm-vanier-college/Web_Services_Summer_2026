
# Web Services
## Project Blueprint: Developing REST Web Services Using the SDLC

**Project Development**

---

# Learning Outcomes

- Apply Software Development Life Cycle (SDLC) phases to a REST Web Service project.
- Design and implement a complete REST API.
- Use a database to store and retrieve data.
- Demonstrate problem-solving skills using Web Services.
- Produce a project report following Agile SDLC principles.
- Present a working business-oriented Web Service solution.

---

# Part 1 

---

# 1. Why Do We Need SDLC?

Developing a Web Service is more than writing code.

A successful application must:

- Solve a real business problem
- Meet user requirements
- Be tested
- Be documented
- Be maintainable

To achieve this, developers follow the:

> Software Development Life Cycle (SDLC)

---

# 2. SDLC Phases

## Phase 1 — Requirements Analysis

Questions:

- What problem are we solving?
- Who will use the system?
- What information should be stored?

### Example

Student Registration API

Requirements:

- Add students
- View students
- Update student information
- Delete students

---

## Phase 2 — System Design

Design the API resources.

### Resources

```text
/students
/courses
/instructors
```

### API Endpoints

```http
GET     /students
GET     /students/{id}
POST    /students
PUT     /students/{id}
DELETE  /students/{id}
```

---

## Phase 3 — Implementation

Write the application code.

Examples:

- Spring Boot
- REST Controllers
- JPA
- SQL Server

---

## Phase 4 — Testing

Verify that:

- Requests work correctly
- Responses are correct
- Database operations work

Tools:

- Postman
- CURL

Example:

```http
GET /students/1
```

Expected:

```json
{
  "id":1,
  "name":"Alice"
}
```

---

## Phase 5 — Deployment

Deploy the application to:

- Local server
- Cloud server
- Docker container

---

## Phase 6 — Maintenance

Activities:

- Bug fixing
- Performance improvements
- Feature enhancements

---

# 3. Agile Development

Modern projects commonly use Agile.

Characteristics:

- Iterative development
- Small releases
- Frequent feedback
- Continuous improvement

---

## Agile Sprint Example

### Sprint 1

Create:

```http
GET /students
```

---

### Sprint 2

Create:

```http
POST /students
PUT /students
DELETE /students
```

---

### Sprint 3

Add:

- Validation
- Error handling
- Documentation

---

# 4. Business Value of Web Services

Web Services allow systems to communicate.

Examples:

| Industry | Web Service Usage |
|-----------|------------------|
| Banking | Account Management |
| Education | Student Registration |
| Healthcare | Patient Records |
| E-Commerce | Product Catalog |
| Transportation | Ticket Booking |

---

# Example Business Case

Library Management API

Features:

- Manage books
- Manage members
- Borrow books
- Return books

Business Benefit:

- Reduced manual work
- Faster access to information
- Better reporting

---

# 5. Project Requirements

Build a complete REST API.

Requirements:

### Must Include

- Spring Boot
- REST Controllers
- SQL Server Database
- JPA Repository

---

### Required Operations

```http
GET
POST
PUT
DELETE
```

---

### Required Database

Minimum:

- Two related tables

Example:

```text
Student
Course
```

---

### Required Documentation

Students must document:

- Requirements
- Design
- API Endpoints
- Database Schema
- Testing Results

---

# Part 2 

## Project Theme

College Course Registration System

---

# Task 1 — Create Database/Tables

---

# Task 2 — Create Spring Boot Project

Dependencies:

- Spring Web
- Spring Data JPA
- SQL Server

---

# Task 3 — Configure Database

application.properties

```properties
spring.datasource.url=jdbc:sqlserver://localhost:3306/college_db
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.hibernate.ddl-auto=update
```

---

# Task 4 — Create Student Entity

```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    private String name;

    private String email;

}
```

---

# Task 5 — Create Repository

```java
public interface StudentRepository
        extends JpaRepository<Student,Integer> {
}
```

---

# Task 6 — Create REST Controller

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @Autowired
    private StudentRepository repository;

    @GetMapping
    public List<Student> getAllStudents() {
        return repository.findAll();
    }
}
```

---

# Task 7 — Test API Using Postman

### Retrieve All Students

```http
GET
http://localhost:8080/students
```

---

### Add Student

```http
POST
http://localhost:8080/students
```

Body:

```json
{
  "name":"Alice",
  "email":"alice@college.ca"
}
```

---

# Task 8 — Implement Remaining CRUD Operations

Students must implement:

```http
GET /students/{id}

POST /students

PUT /students/{id}

DELETE /students/{id}
```

---

# Task 9 — API Testing

Verify:

- Successful operations
- Invalid requests
- Missing records
- Database updates

---

# Task 10 — Prepare Project Report

Report Sections:

1. Introduction
2. Problem Statement
3. Requirements Analysis
4. System Design
5. Database Design
6. API Design
7. Testing Results
8. Screenshots
9. Conclusion

---

# Deliverables

Students must submit:

## 1. Source Code

Complete Spring Boot project.

---

## 2. Database Script

SQL file containing:

```sql
CREATE TABLE
INSERT
```

statements.

---

## 3. Project Report

Agile SDLC-based report.

---

## 4. Demonstration

Project must demonstrate:

- API functionality
- Database operations
- CRUD operations
- Postman testing

---


# Project: College Event Management System
