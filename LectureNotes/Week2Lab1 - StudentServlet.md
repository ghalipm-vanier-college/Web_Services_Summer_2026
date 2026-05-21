# Week2 Lab1: Handling HTTP GET and POST Requests with Java Servlets
## Objective
* Install Postman and use it to test JavaServlet API application.  
* To understand how a Java Servlet processes client-side data by implementing and distinguishing between the two most fundamental 
	HTTP methods: GET and POST.

## By the end of this lab, you will be able to:

* Capture user inputs from an HTML front-end form.

* Read URL parameters using doGet().

* Process secure form payloads using doPost().

* Deploy and run the interactive application on your local Apache Tomcat server.

# Lab 1: Handling HTTP GET and POST Requests

## Objective

* Learn how a Java Servlet handles `GET` and `POST` methods using a simple form with only **Student ID** and **Name**.

---

## 1. Project Structure

Create these two files in your Dynamic Web Project:

```text
YourProject/
├── src/main/java/com/college/servlet/StudentServlet.java
└── src/main/webapp/index.html

```

---

## 2. Code Implementation

### Step 1: The Front-End (`index.html`)

* This file contains two simple forms that send data to the same servlet path (`/submitStudent`).

```html
<!DOCTYPE html>
<html>
<head>
    <title>Servlet GET vs POST</title>
</head>
<body>

    <h3>Form 1: Submit via GET (Visible in URL)</h3>
    <form action="submitStudent" method="GET">
        ID: <input type="text" name="studentId"><br>
        Name: <input type="text" name="studentName"><br>
        <input type="submit" value="Submit GET">
    </form>

    <hr>

    <h3>Form 2: Submit via POST (Hidden payload)</h3>
    <form action="submitStudent" method="POST">
        ID: <input type="text" name="studentId"><br>
        Name: <input type="text" name="studentName"><br>
        <input type="submit" value="Submit POST">
    </form>

</body>
</html>

```

### Step 2: The Backend Servlet (`StudentServlet.java`)

```java
package com.college.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/submitStudent")
public class StudentServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        
        String id = request.getParameter("studentId");
        String name = request.getParameter("studentName");
        
        out.println("<h2>Response from HTTP GET</h2>");
        out.println("<p>Student ID: " + id + "</p>");
        out.println("<p>Student Name: " + name + "</p>");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        
        String id = request.getParameter("studentId");
        String name = request.getParameter("studentName");
        
        out.println("<h2>Response from HTTP POST</h2>");
        out.println("<p>Student ID: " + id + "</p>");
        out.println("<p>Student Name: " + name + "</p>");
    }
}

```

---

## 3. What to Observe

1. **Submit Form 1 (GET):** Look at your browser's address bar. The data is appended to the URL:
`.../submitStudent?studentId=123&studentName=Alex`
2. **Submit Form 2 (POST):** Look at the address bar. The URL stays clean because the data is sent hidden inside the request body:
`.../submitStudent`
