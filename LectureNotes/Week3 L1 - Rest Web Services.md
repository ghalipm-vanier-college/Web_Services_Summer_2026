# Web Services — Lecture Notes
## Week 3 — Session 1
# Creating REST Web Services Using Maven and Servlets

---

# Course Topics

- Creating Dynamic Web Project and converting it into Maven Project
- Maven project dependencies
- Implementation of REST Web Services
- JSON media type
- URL mapping

---

# Learning Objectives To Do List

- Create a Dynamic Web Project
- Convert a project into a Maven project
- Understand Maven dependencies
- Implement simple REST Web Services
- Return JSON responses
- Configure URL mapping using Servlets

---

# 1. Introduction to REST Web Services

## What is a REST Web Service?

REST stands for:

> Representational State Transfer

REST Web Services allow applications to communicate using HTTP.

REST APIs usually:

- use HTTP methods
- exchange JSON data
- use URLs to identify resources

---

# Example REST API

## Request

```http
GET /students
```

## Response

```json
[
  {
    "id": 1,
    "name": "Alice"
  }
]
```

---

# 2. Creating Dynamic Web Project

## Step 1 — Open IntelliJ IDEA

Select:

```text
New Project
```

Choose:

```text
Jakarta EE
```

Enable:

```text
Servlet
```

---

# Step 2 — Configure Project

Example:

| Setting | Value |
|---|---|
| Project Name | WebServicesDemo |
| Build Tool | Maven |
| JDK | Java 21 |
| Server | Tomcat |

---

# Project Structure

```text
WebServicesDemo
│
├── src
├── pom.xml
├── webapp
└── WEB-INF
```

---

# 3. What is Maven?

## Definition

Maven is a build and dependency management tool for Java projects.

Maven helps developers:

- manage libraries
- compile projects
- package applications
- manage dependencies automatically

---

# Maven Advantages

- Simplifies project management
- Downloads required libraries automatically
- Standard project structure
- Easy dependency management

---

# 4. Converting Project to Maven

## Maven Project Structure

```text
src/main/java
src/main/webapp
src/test/java
pom.xml
```

---

# The pom.xml File

The main Maven configuration file is:

```text
pom.xml
```

---

# Example pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>webservicesdemo</artifactId>
    <version>1.0</version>

    <dependencies>

        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.0.0</version>
            <scope>provided</scope>
        </dependency>

    </dependencies>

</project>
```

---

# 5. Maven Dependencies

## What is a Dependency?

A dependency is an external library used by the application.

Examples:

- Servlet API
- JSON libraries
- JDBC drivers

---

# Example Dependency

```xml
<dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>6.0.0</version>
    <scope>provided</scope>
</dependency>
```

---

# 6. Creating First REST Web Service

## Create Servlet

```java
@WebServlet("/students")
public class StudentServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request,
                         HttpServletResponse response)
            throws IOException {

        response.setContentType("application/json");

        String json =
                "[{\"id\":1,\"name\":\"Alice\"}," +
                "{\"id\":2,\"name\":\"Bob\"}]";

        response.getWriter().write(json);
    }
}
```

---

# Explanation

| Code | Description |
|---|---|
| @WebServlet | Maps URL to servlet |
| doGet() | Handles GET requests |
| setContentType() | Defines response type |
| getWriter() | Sends response to client |

---

# 7. JSON Media Type

## What is JSON?

JSON stands for:

> JavaScript Object Notation

JSON is commonly used in REST APIs.

---

# JSON Example

```json
{
  "id": 1,
  "name": "Alice"
}
```

---

# JSON Array Example

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

# Content Type for JSON

```java
response.setContentType("application/json");
```

---

# Common Media Types

| Media Type | Description |
|---|---|
| text/plain | Plain text |
| text/html | HTML |
| application/json | JSON |
| application/xml | XML |

---

# 8. URL Mapping

## What is URL Mapping?

URL mapping connects a URL to a specific servlet.

---

# Example

```java
@WebServlet("/students")
```

This means:

```text
http://localhost:8080/project-name/students
```

will call:

```text
StudentServlet
```

---

# Additional URL Examples

| URL | Purpose |
|---|---|
| /students | Get all students |
| /students/1 | Get student by ID |
| /courses | Get courses |
| /teachers | Get teachers |

---

# 9. Testing REST Web Services

## Using Browser

Open:

```text
http://localhost:8080/project-name/students
```

---

# Using Postman

Steps:

1. Select GET
2. Enter URL
3. Click Send
4. Analyze response

---

# Expected JSON Response

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

# 10. Problem Solving Using REST Services

REST services can solve many business problems.

Examples:

- Student Management System
- Online Shopping System
- Banking Applications
- Mobile Applications

---

# Different Media Types

REST services may return:

| Media Type | Example |
|---|---|
| JSON | Modern REST APIs |
| XML | Legacy systems |
| Plain Text | Simple responses |

---

# Example XML Response

```xml
<student>
    <id>1</id>
    <name>Alice</name>
</student>
```

---

# Lab Practice

## Lab Activity 1 — Create Maven Project

Tasks:

- Create Dynamic Web Project
- Convert to Maven project
- Configure pom.xml

### Converting Dynamic Web Project to Maven Project Using IntelliJ IDEA
  - Right-click on your project folder in the Project tool window.
  - Select Add Framework Support....
  - Choose Maven from the list and click OK.

---

## Lab Activity 2 — Create REST Servlet

Tasks:

- Create StudentServlet
- Return JSON response
- Configure URL mapping

---

## Lab Activity 3 — Test Using Postman

Tasks:

- Send GET request
- Analyze response
- Verify JSON output


---
