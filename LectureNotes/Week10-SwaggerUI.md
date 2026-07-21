````markdown
# Spring MVC, REST API, Swagger UI, and API Testing

## 1. Spring MVC vs REST API

Spring MVC is a framework for building web applications.  
A REST API is a web service that allows applications to communicate using HTTP and exchange data (usually JSON).

| Spring MVC | REST API |
|------------|----------|
| `@Controller` | `@RestController` |
| Returns HTML pages | Returns JSON/XML data |
| Uses Thymeleaf/JSP views | Used by Postman, React, Angular, Flutter |
| `return "students";` | `return List<Student>;` |
| Displays pages in a browser | Provides data to applications |

### Spring MVC Example

```java
@Controller
public class StudentController {

    @GetMapping("/students")
    public String students(Model model) {
        return "students";
    }
}
````

Response:

```
HTML page
```

---

### REST API Example

```java
@RestController
public class StudentRestController {

    @GetMapping("/api/students")
    public List<Student> getStudents() {
        return students;
    }
}
```

Response:

```json
[
  {
    "id": 1,
    "name": "Alice"
  }
]
```

---

# 2. Spring Boot REST Application Components

| Component         | Purpose                                       |
| ----------------- | --------------------------------------------- |
| Spring Boot       | Builds and runs the application               |
| Spring MVC        | Handles HTTP requests and responses           |
| Spring Data JPA   | Communicates with SQL Server/database         |
| SQL Server        | Stores application data                       |
| `@RestController` | Creates REST endpoints                        |
| Swagger/OpenAPI   | Describes and documents REST APIs             |
| Swagger UI        | Provides interactive API testing in a browser |

---

# 3. REST API and HTTP Methods

REST APIs use HTTP methods to perform operations:

| HTTP Method | Purpose       | Example           |
| ----------- | ------------- | ----------------- |
| GET         | Retrieve data | Get all students  |
| POST        | Create data   | Add a new student |
| PUT         | Update data   | Modify a student  |
| DELETE      | Remove data   | Delete a student  |

Example endpoints:

```
GET     /api/students
GET     /api/students/1
POST    /api/students
PUT     /api/students/1
DELETE  /api/students/1
```

---

# 4. What is Swagger/OpenAPI?

Swagger is a tool based on the **OpenAPI Specification**.

OpenAPI describes a REST API contract:

* Available endpoints
* HTTP methods
* Request parameters
* Request body format
* Response format
* Error responses

Example:

```
GET /api/students
```

OpenAPI describes:

```json
Response:
[
  {
    "id": 1,
    "name": "Alice"
  }
]
```

---

# 5. Relationship Between WSDL and Swagger

Both WSDL and Swagger describe web services.

| SOAP Web Service        | REST Web Service                |
| ----------------------- | ------------------------------- |
| WSDL                    | OpenAPI / Swagger               |
| XML-based contract      | JSON/YAML-based description     |
| Defines SOAP operations | Defines REST endpoints          |
| Tested using SoapUI     | Tested using Swagger UI/Postman |
| Uses `@Endpoint`        | Uses `@RestController`          |

Relationship:

```
SOAP Web Service
        |
        |
       WSDL
        |
        |
  XML Service Contract


REST Web Service
        |
        |
 OpenAPI / Swagger
        |
        |
 REST API Contract
        |
        |
    Swagger UI
```

---

# 6. Swagger UI for API Testing

Swagger UI is a browser-based interface generated from the OpenAPI description.

It allows developers to:

* View all REST endpoints
* Understand request and response formats
* Enter parameters
* Send HTTP requests
* Test APIs without Postman
* View API responses immediately

Example:

Open browser:

```
http://localhost:8080/swagger-ui.html
```

Swagger UI displays:

```
GET /api/students

[ Try it out ]

Execute
```

After clicking **Try it out**:

1. Swagger UI creates an HTTP request.
2. The request is sent to the REST controller.
3. Spring Boot processes the request.
4. The controller returns JSON.
5. Swagger UI displays the response.

Example:

### Request

```
GET /api/students
```

### Response

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

# 7. Testing POST API with Swagger UI

Example REST endpoint:

```java
@PostMapping("/api/students")
public Student addStudent(@RequestBody Student student) {
    return repository.save(student);
}
```

Swagger UI displays:

```
POST /api/students

Request body:

{
  "name": "Charlie",
  "city": "Montreal"
}

[ Try it out ]

[ Execute ]
```

Swagger sends:

```
POST http://localhost:8080/api/students
Content-Type: application/json
```

Spring Boot receives the JSON:

```json
{
  "name": "Charlie",
  "city": "Montreal"
}
```

and returns:

```json
{
  "id": 3,
  "name": "Charlie",
  "city": "Montreal"
}
```

---

# 8. Adding Swagger UI to Spring Boot

Add this dependency in `pom.xml`:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>
        springdoc-openapi-starter-webmvc-ui
    </artifactId>
    <version>2.8.9</version>
</dependency>
```

Start Spring Boot and open:

```
http://localhost:8080/swagger-ui.html
```

Swagger UI automatically discovers:

* `@RestController`
* `@GetMapping`
* `@PostMapping`
* `@PutMapping`
* `@DeleteMapping`

---

# Summary

```
Spring Boot
      |
      |
  Spring MVC
      |
      |
@RestController
      |
      |
  REST API
      |
      |
 OpenAPI / Swagger
      |
      |
 Swagger UI
      |
      |
 API Documentation
      |
      |
 Interactive API Testing
```

**WSDL is the contract and documentation standard for SOAP services.**

**OpenAPI/Swagger is the contract and documentation standard for REST services.**

**Swagger UI is the interactive browser tool that reads the OpenAPI description and allows developers to test REST APIs directly.**

```
```
