
# Web Services — Lecture Notes
## HTTP Request/Response and REST vs SOAP

---

# Course Topics

- HTTP Request/Response
- REST vs SOAP
- Using CURL Tool
- Using Postman Tool
- Display HTTP Request/Response when fetching Servlet resources
- Consuming Public SOAP Services

---

# Learning Objectives

- Understand the HTTP request/response model
- Explain the difference between REST and SOAP
- Use CURL and Postman to test APIs
- Inspect HTTP headers and status codes
- Consume public SOAP services

---

# 1. Introduction to HTTP Communication

## What is HTTP?

HTTP stands for:

> HyperText Transfer Protocol

HTTP is the communication protocol used between:

- Web browsers
- Clients
- Web servers
- APIs

HTTP is the foundation of communication on the Web.

---

# 2. Client–Server Communication Model

## Basic Architecture

```text
Client  --->  HTTP Request  --->  Server
Client  <--- HTTP Response <---  Server
```

Examples of clients:

- Browser
- Mobile App
- Postman
- CURL
- Java Application

Examples of servers:

- Tomcat
- GlassFish
- Spring Boot Server

---

# 3. HTTP Request and Response Cycle

## Step 1 — Client Sends Request

Example HTTP Request:

```http
GET /students HTTP/1.1
Host: localhost:8080
```

### Explanation

| Part | Description |
|---|---|
| GET | HTTP Method |
| /students | Requested resource |
| HTTP/1.1 | HTTP version |
| Host | Server address |

---

## Step 2 — Server Processes Request

The server:

- receives request
- executes business logic
- accesses database if needed
- prepares response

---

## Step 3 — Server Sends Response

Example HTTP Response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

Response body:

```json
[
  {
    "id": 1,
    "name": "Alice"
  }
]
```

---

# 4. HTTP Methods

HTTP methods define the type of operation requested by the client.

---

## GET Method

Used to retrieve data.

Example:

```http
GET /students
```

---

## POST Method

Used to create data.

Example:

```http
POST /students
```

---

## PUT Method

Used to update existing data.

Example:

```http
PUT /students/1
```

---

## DELETE Method

Used to remove data.

Example:

```http
DELETE /students/1
```

---

# 5. HTTP Status Codes

Status codes indicate the result of the request.

| Code | Meaning |
|---|---|
| 200 | Success |
| 201 | Resource Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Resource Not Found |
| 500 | Internal Server Error |

---

# 6. REST vs SOAP

---

# REST (Representational State Transfer)

REST is a lightweight architectural style used for building Web APIs.

## Characteristics of REST

- Uses HTTP directly
- Usually returns JSON
- Lightweight and simple
- Resource-oriented
- Faster communication

---

## REST Example

Request:

```http
GET /students/1
```

Response:

```json
{
  "id": 1,
  "name": "Alice"
}
```

---

# SOAP (Simple Object Access Protocol)

SOAP is a protocol used for exchanging structured information between applications.

## Characteristics of SOAP

- Uses XML only
- Strict message format
- Operation-oriented
- Uses SOAP Envelope
- More secure and formal

---

## SOAP Request Example

```xml
<soap:Envelope>
   <soap:Body>
      <getStudent>
         <id>1</id>
      </getStudent>
   </soap:Body>
</soap:Envelope>
```

---

# REST vs SOAP Comparison

| Feature | REST | SOAP |
|---|---|---|
| Format | JSON | XML |
| Complexity | Simple | Complex |
| Speed | Faster | Slower |
| Style | Resource-based | Operation-based |
| Common Use | Modern APIs | Enterprise Systems |

---

# 7. Using CURL Tool

## What is CURL?

CURL is a command-line tool used to:

- send HTTP requests
- test APIs
- inspect server responses

---

# CURL GET Request Example

```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

Expected Output:

```json
{
  "userId": 1,
  "id": 1,
  "title": "...",
  "body": "..."
}
```

---

# CURL POST Request Example

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts ^
-H "Content-Type: application/json" ^
-d "{\"title\":\"Test\"}"
```

---

# 8. Using Postman Tool

## What is Postman?

Postman is a graphical tool used for:

- testing APIs
- sending requests
- viewing responses
- analyzing headers and status codes

---

# Steps for Using Postman

1. Select HTTP method
2. Enter URL
3. Click Send
4. Analyze response

---

# Example

## URL

```text
https://jsonplaceholder.typicode.com/posts/1
```

## Method

```text
GET
```

---

# 9. Displaying HTTP Request/Response Using Servlet

## Simple Servlet Example

```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request,
                         HttpServletResponse response)
            throws IOException {

        response.setContentType("text/plain");

        response.getWriter().write("Hello Web Services");
    }
}
```

---

# Running the Servlet

Open browser:

```text
http://localhost:8080/project-name/hello
```

Expected Output:

```text
Hello Web Services
```

---

# Inspecting the Response Using Postman

To inspect:

- HTTP status code
- Response headers
- Response body
- Content-Type

---

# 10. Consuming Public SOAP Services

## Example SOAP Service

Public Calculator SOAP Service:

http://www.dneonline.com/calculator.asmx

---

# SOAP Request Example

```xml
<?xml version="1.0" encoding="utf-8"?>

<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">

<soap:Body>
<Add xmlns="http://tempuri.org/">
<intA>5</intA>
<intB>7</intB>
</Add>

</soap:Body>
</soap:Envelope>
```

---

# SOAP Response Example

```xml
<?xml version="1.0" encoding="utf-8"?>

<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">

<soap:Body>
<AddResponse xmlns="http://tempuri.org/">
<AddResult>12</AddResult>
</AddResponse>

</soap:Body>
</soap:Envelope>
```

---

# Suggested Lab Activities

## Activity 1 — CURL Practice

Tasks:

- Send GET request
- Send POST request
- Analyze JSON response

---

## Activity 2 — Postman Practice

Tasks:

- Send GET request
- Inspect headers
- Analyze status codes
- Test invalid URLs

---

## Activity 3 — Servlet Testing

Tasks:

- Run servlet
- Access servlet from browser
- Test servlet using Postman

---

## Activity 4 — SOAP Service Testing

Tasks:

- Send SOAP request
- Analyze SOAP XML response
- Compare SOAP vs REST output

---


---

